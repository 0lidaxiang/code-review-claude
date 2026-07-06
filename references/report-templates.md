# 审查报告模板（Claude-inspired 风格）

按用户在第 0 步选定的格式，二选一套用。占位符用 `〔〕` 标注，填充后删除说明性注释。

---

## A. Markdown 模板（默认）

```markdown
# 代码审查报告 · 〔项目/改动名〕

> 审查对象：〔git diff / PR#123 / 路径〕　审查重点：〔正确性/安全/…〕　日期：〔YYYY-MM-DD〕
> 审查风格：Claude-inspired（对抗式验证 · 少而准）

## 总体判断
〔一句话：可合并 / 修完 P0 再合并 / 有阻断性问题。附一句理由。〕

| 严重度 | 数量 |
|---|---|
| 🔴 阻断 (blocker) | 〔n〕 |
| 🟠 高 (high) | 〔n〕 |
| 🟡 中 (medium) | 〔n〕 |
| ⚪ 低/可选 | 〔n〕 |

## 发现（按严重度降序）

### 1. 🔴 〔一句话结论〕
- **位置**：`src/foo.ts:42`
- **类别 / 置信度**：correctness · `CONFIRMED`
- **失败场景**：〔具体输入/状态 → 具体错误结果，如 items 为空时 items[0].id 抛 TypeError → 接口 500〕
- **建议修复**：〔一句话 + 必要时贴最小 diff〕

### 2. 🟠 〔……〕
（同上结构）

## 可选优化（不阻断，供参考）
- 〔与本次重点无关但顺手可改的项，避免混进主发现〕
```

---

## B. HTML 模板（单文件 · 零依赖 · 可打印 PDF · 明暗自适应）

> 用户选 HTML 时，把发现填进 `<article class="finding">` 卡片，复制成多份即可。整份保存为 `代码审查报告.html`，双击用浏览器打开。

```html
<!doctype html><html lang="zh-CN"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>代码审查报告 · 〔项目名〕</title>
<style>
  :root{--bg:#faf9f7;--fg:#1a1a1a;--muted:#6b6b6b;--card:#fff;--line:#e6e3dd;
        --blocker:#c0392b;--high:#e67e22;--medium:#e0a800;--low:#7f8c8d;--code:#f0eee9;--brand:#c15f3c}
  @media (prefers-color-scheme:dark){:root{--bg:#1c1b19;--fg:#eceae6;--muted:#9a968e;--card:#26241f;--line:#38352f;--code:#2f2c26}}
  *{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--fg);
    font:16px/1.6 -apple-system,"PingFang SC","Microsoft YaHei",system-ui,sans-serif;padding:2.4rem 1.2rem}
  .wrap{max-width:860px;margin:0 auto}
  h1{font-size:1.7rem;margin:0 0 .2rem;border-left:5px solid var(--brand);padding-left:.6rem}
  .meta{color:var(--muted);font-size:.86rem;margin:.4rem 0 1.6rem}
  .verdict{background:var(--card);border:1px solid var(--line);border-radius:12px;padding:1rem 1.2rem;margin-bottom:1.4rem}
  .tally{display:flex;gap:.6rem;flex-wrap:wrap;margin-top:.8rem}
  .pill{font-size:.8rem;padding:.2rem .7rem;border-radius:999px;color:#fff}
  .finding{background:var(--card);border:1px solid var(--line);border-left-width:5px;border-radius:12px;padding:1rem 1.2rem;margin:1rem 0}
  .finding.blocker{border-left-color:var(--blocker)} .finding.high{border-left-color:var(--high)}
  .finding.medium{border-left-color:var(--medium)} .finding.low{border-left-color:var(--low)}
  .finding h3{margin:.1rem 0 .5rem;font-size:1.08rem}
  .tags{display:flex;gap:.5rem;flex-wrap:wrap;font-size:.76rem;color:var(--muted);margin-bottom:.6rem}
  .tags code{background:var(--code);padding:.05rem .45rem;border-radius:5px}
  .finding p{margin:.35rem 0} .finding .k{color:var(--muted);font-weight:600}
  pre{background:var(--code);padding:.7rem .9rem;border-radius:8px;overflow:auto;font-size:.85rem}
  @media print{body{padding:0}.finding,.verdict{break-inside:avoid}}
</style></head><body><div class="wrap">
  <h1>代码审查报告 · 〔项目名〕</h1>
  <div class="meta">审查对象：〔…〕 · 审查重点：〔…〕 · 日期：〔YYYY-MM-DD〕 · 风格：Claude-inspired（对抗式验证）</div>

  <div class="verdict">
    <strong>总体判断：</strong>〔可合并 / 修完 P0 再合并 / 有阻断性问题——一句理由〕
    <div class="tally">
      <span class="pill" style="background:var(--blocker)">阻断 〔n〕</span>
      <span class="pill" style="background:var(--high)">高 〔n〕</span>
      <span class="pill" style="background:var(--medium)">中 〔n〕</span>
      <span class="pill" style="background:var(--low)">低 〔n〕</span>
    </div>
  </div>

  <!-- 每条发现复制一份此卡片；class 换成 blocker/high/medium/low -->
  <article class="finding blocker">
    <div class="tags"><code>correctness</code><code>CONFIRMED</code><span>src/foo.ts:42</span></div>
    <h3>1. 〔一句话结论〕</h3>
    <p><span class="k">失败场景：</span>〔具体输入/状态 → 具体错误结果〕</p>
    <p><span class="k">建议修复：</span>〔一句话〕</p>
    <pre>〔可选：最小修复 diff〕</pre>
  </article>

</div></body></html>
```
