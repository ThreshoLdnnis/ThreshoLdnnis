# 维护这张个人主页卡片

主页位于 [github.com/ThreshoLdnnis](https://github.com/ThreshoLdnnis)。公开的同名仓库根目录 `README.md` 会显示在个人主页。

- 修改 `profile.json` 可以调整姓名、介绍、关注方向和精选项目；提交后会自动重新生成卡片。
- 头像来自当前公开的 GitHub 头像，并转成 ASCII 字符画。
- 桌面和手机卡片会按屏幕和 GitHub 主题选择图片；字符采用粉白配色，深色背景让白色头发与文字保持清楚。
- `README.md`、`assets/` 是生成结果；长期修改请编辑配置或 `scripts/generate_profile.py`。

## 自动刷新

工作流为 **Update profile card**，每天计划在北京时间 **08:17** 刷新。也可以进入仓库 **Actions → Update profile card → Run workflow** 手动运行。修改配置、脚本、依赖或工作流也会触发刷新。

只需 GitHub 自动提供的 `GITHUB_TOKEN`，无需配置个人 Token。工作流仅请求当前仓库的 `contents: write` 权限，用于提交卡片和数据。

GitHub 的定时任务可能延迟；公开仓库连续 60 天无活动时，计划任务可能被自动停用，可在 Actions 页面重新启用。[GitHub 官方说明](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule)

## 数据口径

统计只来自公开的 GitHub 用户资料与本人拥有的公开仓库。Stars 和 Forks 是这些仓库收到的合计；语言按非 Fork 公开仓库的主要语言计数，不代表熟练程度或代码行占比。`Uptime` 是账号注册至今的时间。不会读取或展示私有仓库、私人邮箱、个人年龄，也不会估算 Commits 或代码行数。

## 在本地生成

需要 Python 3.12：

```sh
python -m pip install -r requirements.txt
python scripts/fetch_stats.py
python scripts/generate_profile.py
```

已有缓存数据与字符画时，可用 `python scripts/generate_profile.py --offline` 离线检查布局。
