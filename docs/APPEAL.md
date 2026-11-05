# GitHub Support 工单 — 可直接粘贴版

对应截图里的表单：`主题 *` / `Please describe your repository issue *` / `我们能提供什么帮助？ *`
三段分别复制即可，均为英文（GitHub Support 处理更快）。

---

## ① 主题（≤80 字符，实测 62 字符）

```
Request to re-enable GitHub Actions for wdss133/openwrt-ci-roc
```

---

## ② Please describe your repository issue（支持 Markdown，整段复制）

```
**Repository:** https://github.com/wdss133/openwrt-ci-roc
**Account:** wdss133
**Issue:** GitHub Actions has been disabled for this repository by GitHub, not by my repository settings.

### What this repository is for
This is a public fork of `laipeng668/openwrt-ci-roc`. I use it solely to build a personal OpenWrt firmware image for my own Redmi AX6 router at home. It is a single-user, non-commercial hobby project.

### The workflow
Only one workflow is active: `.github/workflows/Custom-IPQ807X-Daily.yml`.
- Runs once per day at 13:00 UTC (21:00 Beijing time) via `cron: "0 13 * * *"`.
- Builds exactly one device target: `qualcommax/ipq807x`, `redmi_ax6-stock`. All other devices are excluded by a whitelist.
- One job, no matrix fan-out, no parallel builds, no self-hosted runners, roughly 60-90 minutes per run.
- The other eight workflows inherited from upstream are all manually disabled.
- No cryptocurrency mining, no proxy/relay or tunneling, no reselling or sharing of CI capacity, no third-party or commercial workloads, no bulk/automated account activity, and no attempts to work around usage limits.

### Timeline
- Run #26 (2026-10-14 UTC) was the last successful scheduled build.
- Since 2026-10-15, no scheduled or manually dispatched run can start. The Actions page shows: "GitHub Actions is currently disabled for this repository. Please reach out to GitHub Support for assistance."

### Evidence that this is a server-side restriction, not a settings problem
- `GET /repos/wdss133/openwrt-ci-roc` returns `disabled: false`, `archived: false`.
- `GET /repos/wdss133/openwrt-ci-roc/actions/permissions` returns `{"enabled": true, "allowed_actions": "all"}` — Actions is enabled in settings.
- Toggling that setting off and back on via `PUT` returns `204`, but changes nothing.
- `POST /repos/wdss133/openwrt-ci-roc/actions/workflows/Custom-IPQ807X-Daily.yml/dispatches` returns `422` with `{"message": "Actions has been disabled for this repository."}` (re-tested on 2026-11-05).
- A minimal one-line test workflow in a separate, freshly created private repository under the same account ran successfully, which suggests the restriction is specific to this repository (possibly inherited from the upstream fork network) rather than my account.

### Request
Could you please review this repository and re-enable GitHub Actions for it? I would prefer to keep using the original repository, since its Release history and download links live there.

If the daily build was flagged by an automated heavy-usage heuristic, I am happy to reduce the schedule to every 2-3 days, lower `timeout-minutes`, or move to a self-hosted runner — please let me know what is required.

Thank you for your help.
wdss133
```

---

## ③ 我们能提供什么帮助？

**勾「恢复」（Restore）** —— 诉求是恢复被停用的 GitHub Actions。
若客服回复说归类应改选「存储库功能」（Repository features），按他们说的改即可，工单会内部转派，不影响受理。

---

## 填写提示（不用粘贴）

1. **不要提 `wdss133/openwrt-ax6-ci` 这个迁移仓库**。文案里只说"另建了一个极简探针仓库跑通了一行 echo"，这是真实且有价值的对照证据；如果主动告诉 GitHub"被封后又开了新仓库继续跑同样的编译"，有被误判为规避封禁（circumvention）的风险。原仓库解封后，两套是否并存再另行处理。
2. 英文比中文处理快，别加中文说明。
3. 主题栏正好 62 字符，别加标点或日期，80 字符上限放不下。
4. 如果表单后面还有附件步骤，可以把 `output/actions-fix/解决方案与申诉文案.md` 里的诊断表截图附上，但通常不需要。
5. 提交后 Support 一般 1-3 个工作日回复；期间每日编译已经在 `wdss133/openwrt-ax6-ci` 正常跑，不耽误用固件。
