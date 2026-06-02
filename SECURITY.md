# AI Agent Skill 安全审核指南

> 从市场安装第三方 skill 前，请务必进行安全检查。
> 据 2026 年中的调研数据，部分市场约 7% 的 skill 存在泄露 API Key 等风险。

---

## 一、审核层级

```
Skill 安全审核 = 静态分析 + 行为审查 + 信任管理
                    │              │            │
                    ▼              ▼            ▼
              代码级检查      运行时行为     用户信任策略
              文件系统访问    网络请求       首次确认
              eval/Function  cookie 读写    永久信任
              innerHTML      数据外发       信任撤回
```

## 二、SKILL.md 静态检查

### 2.1 Frontmatter 检查清单

| 检查项 | 安全要求 | 危险信号 |
|--------|---------|---------|
| `name` | 唯一、无歧义 | 与知名 skill 同名（冒充） |
| `description` | 如实描述功能 | 描述模糊或夸大 |
| `author` | 可追溯的 GitHub ID | 匿名、新注册账号 |
| `version` | 语义化版本 | 版本跳跃过大 |
| `tags` | 与内容匹配 | 标签与功能无关 |

### 2.2 指令内容检查清单

AI 会执行的 Markdown 指令中，注意以下危险模式：

| 模式 | 风险 | 说明 |
|------|------|------|
| "忽略安全检查"/"跳过验证" | 高 | 试图绕过安全机制 |
| "把结果发送到 http://..." | 高 | 数据外发到第三方服务器 |
| "读取 ~/.ssh/ 或 ~/.aws/" | 高 | 窃取凭据/密钥 |
| "执行 curl/wget 并 pipe 到 shell" | 高 | 远程代码执行 |
| "修改 chrome.storage" | 中 | 篡改扩展数据 |
| "访问 document.cookie" | 中 | 窃取会话 |

## 三、脚本代码安全扫描

### 3.1 高危模式（❌ 禁止提交）

```javascript
eval(userInput);                          // 动态执行不可信代码
new Function('return ' + data)();         // Function 构造器
document.write(attackerControlled);       // 覆盖页面
```

### 3.2 中危模式（⚠️ 需审查）

```javascript
document.cookie                           // 读取 Cookie
element.innerHTML = data;                 // XSS 风险
fetch('https://unknown-server.com', ...)  // 外发请求
chrome.storage.local.get(...)             // 读取扩展数据
```

### 3.3 低危模式（ℹ️ 需注意）

```javascript
fetch('https://api.github.com', ...)      // 合法 API 调用
localStorage.setItem(...)                 // 页面本地存储
postMessage({...})                        // 跨窗口通信
```

### 3.4 自动化扫描（validateScript）

CrazyCodeCat 内置扫描函数（`src/agent/validator.js`）:

```javascript
function validateScript(code) {
  var risks = [];
  // 高危
  if (/\beval\s*\(/.test(code))           risks.push({ type: 'eval', severity: 'high' });
  if (/\bnew\s+Function\s*\(/.test(code)) risks.push({ type: 'Function', severity: 'high' });
  // 中危
  if (/document\.cookie/.test(code))       risks.push({ type: 'cookie', severity: 'medium' });
  if (/\.innerHTML\s*=/.test(code))       risks.push({ type: 'innerHTML', severity: 'medium' });
  if (/chrome\.\w+/.test(code))           risks.push({ type: 'chromeAPI', severity: 'medium' });
  // 低危
  if (/fetch\s*\(/.test(code))            risks.push({ type: 'fetch', severity: 'low' });
  return { safe: highCount === 0, risks };
}
```

## 四、信任模型

### 4.1 三级信任

```
Level 1 — 待确认（pending）
  首次安装后的默认状态
  脚本不自动执行，需用户手动确认
  显示安全扫描报告

Level 2 — 已信任（trusted）
  用户确认安全
  脚本可自动执行
  可随时撤销信任

Level 3 — 已拒绝（rejected）
  用户判定不安全
  脚本被禁用
  可重新评估
```

### 4.2 信任决策流程

```
安装 skill
  │
  ▼
安全扫描
  ├── 无风险 → 自动标记为 trusted
  ├── 有中危 → 显示风险列表 → 用户选择 trusted/rejected
  └── 有高危 → 标记为 rejected，禁止安装
  │
  ▼
首次执行
  ├── trusted → 直接执行
  └── pending → 弹出确认对话框
       ├── 允许本次 → 执行
       └── 永久信任 → 升级到 trusted
```

## 五、市场层面的安全措施

### 5.1 PR 自动检查（CI）

`marketplace-skills` 的 `validate.yml` 在 PR 阶段执行：

```yaml
# 安全相关检查步骤
- name: Security scan
  run: |
    for js in skills/*/scripts/*.js; do
      [ -f "$js" ] || continue
      if grep -qE 'eval\s*\(' "$js"; then
        echo "❌ $js: 包含 eval()"
        exit 1
      fi
      if grep -qE 'document\.cookie' "$js"; then
        echo "⚠️  $js: 访问 cookie"
      fi
    done
```

### 5.2 人工审核清单

PR review 时检查：

```
□ SKILL.md 描述与实际功能一致
□ 无高危代码（eval、Function 构造器）
□ 网络请求指向可信域名
□ 无隐蔽的数据外发逻辑
□ 不请求不必要的权限
□ 不模仿/冒充其他知名 skill
```

### 5.3 已知风险模式（来自市场调研）

根据 SkillsMP 等大规模市场的安全调研：

| 风险 | 发生率 | 示例 |
|------|--------|------|
| API Key 泄露 | ~7% | skill 要求用户填入 Key 然后发送到第三方 |
| 凭据窃取 | ~3% | 读取 ~/.env、AWS 凭据文件 |
| 品牌冒充 | ~2% | 模仿知名 skill 名称诱导安装 |
| 数据外发 | ~5% | 使用用户的 API Key 调用第三方服务 |

## 六、CCC 插件的安全架构

### 6.1 安装时

```
用户执行 /skill install <名称>
  │
  ▼
下载 SKILL.md
  │
  ▼
validateScript() ← 自动运行
  ├── OK → 直接安装
  └── 有风险 → 显示安全报告 → 用户决定
  │
  ▼
存入 IndexedDB（trust = pending 或 trusted）
```

### 6.2 执行时

```
AI 激活 skill
  │
  ▼
检查 trust 状态
  ├── trusted → 直接加载
  ├── pending → 弹出确认框
  │   ├── 确认 → 执行
  │   └── 拒绝 → 跳过
  └── rejected → 跳过，提示用户
```

### 6.3 可撤销

用户随时可以在 Settings → Skill 管理 中：
- 查看 skill 的安全扫描报告
- 切换信任状态
- 卸载 skill

## 七、给 skill 开发者的建议

编写安全的 skill：

```markdown
---
name: my-safe-skill
description: 安全的设计示例
---

# 安全 skill 编写指南

## ✅ 推荐做法
- 明确声明 skill 的权限需求
- 网络请求只指向可信 API
- 使用占位符而非真实数据做演示

## ❌ 避免的做法
- 不请求用户不需要的权限
- 不硬编码 API Key
- 不将用户数据发送到未声明的第三方
```

---

## 八、参考资料

- CrazyCodeCat validateScript: `src/agent/validator.js`
- CCC 信任管理: Settings → Skill 管理 → 信任状态
- OWASP 安全指南: https://owasp.org
- SkillsMP 安全警告: https://skillsmp.com/security
