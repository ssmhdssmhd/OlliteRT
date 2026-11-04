# Changelog

All notable changes to OlliteRT are documented in [GitHub Releases](https://github.com/NightMean/ollitert/releases).

> [!TIP]
> Each release includes a signed arm64-v8a APK download and a full summary of changes.

## 版本更新记录（中文）

### v0.9.8 — 简体中文界面与云端打包

- **新增**：完整简体中文（`zh-CN`）界面，系统语言为中文时自动切换。
- **新增**：GitHub Actions 手动云端打包，勾选“仅云端打包”即可构建，无需创建标签。
- **新增**：Release 页面自动生成中文更新说明与 SHA256 校验值。
- **优化**：APK 产物命名统一为 `OlliteRT.<渠道>.<版本号>.<yyyyMMddHHmm>.apk`，使用点号分隔。
- **优化**：Release 资产支持 HTTP Range 断点续传，并附带国内加速镜像地址。
- **修复**：CI 使用固定签名，确保各版本签名一致，可覆盖安装、无签名冲突。

## Release Tag Convention

| Channel | Tag Format | GitHub Flag | Example |
|:--------|:-----------|:------------|:--------|
| **Stable** | `vX.Y.Z` | Release | `v1.3.0` |
| **Beta** | `vX.Y.Z-beta.N` | Pre-release | `v1.3.0-beta.2` |
| **Dev** | `vX.Y.Z-dev.N` | Pre-release | `v1.3.0-dev.5` |

## Update Channels

OlliteRT checks for updates automatically (configurable in Settings → App Updates):

- **Stable** builds check `/releases/latest` — auto-skips pre-releases
- **Beta** builds check all releases, filtering for `-beta.N` or newer stable
- **Dev** builds take the most recent non-draft release

### Cross-Channel Notifications

Users can opt-in to notifications about releases from other channels (Settings → App Updates → "Notify about other channels"). When enabled:

- The update check fetches all recent releases and notifies about versions outside the installed channel
- Separate Android notification channels for beta and dev releases allow granular muting
- Tapping the notification opens the GitHub release page directly

## Format

Releases follow [Keep a Changelog](https://keepachangelog.com/) conventions:

| Category | Usage |
|:---------|:------|
| **Added** | New features |
| **Changed** | Enhancements to existing features |
| **Fixed** | Bug fixes |
| **Removed** | Removed features or deprecated items |
| **Security** | Security-related changes |

## Checking Your Version

The current version and build hash are shown at the bottom of the Settings screen (e.g. `OlliteRT v1.0.0 (abc123)`). You can also check for updates manually via the "Check Now" button in Settings → App Updates.

## For Developers

### Creating a Release

1. Update `APP_VERSION_NAME` in `gradle.properties`
2. Push a tag matching the [Release Tag Convention](#release-tag-convention) — CI builds the correct flavor automatically based on the tag pattern
3. The GitHub Release body must follow the [Keep a Changelog](#format) format above — write in user-facing language, not code-level details

### Fastlane Changelog Metadata

For each stable release, a changelog file is automatically generated at:

```
fastlane/metadata/android/en-US/changelogs/{versionCode}.txt
```

The CI workflow summarizes the GitHub Release notes to ≤500 characters using GPT-4o-mini (via GitHub Models). If the AI is unavailable, it falls back to stripping Markdown and truncating.

- **Maximum 500 characters** (characters, not bytes), plain text (no Markdown)
- The file name must match the `versionCode` exactly (not `versionName`)
- Only generated for stable releases (not beta/dev)
- To generate manually: `echo "release notes" | python3 .github/scripts/generate_fastlane_changelog.py`
