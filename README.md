# qqbot-music-maibot

[qqbot-music](https://github.com/aa1805370178-dot/qqbot-music) 的 MaiBot 插件：给麦麦一个 `sing` 工具，有人让她唱歌时，用你配置的音色唱副歌（或整首），以语音发出来。

插件本身不跑模型，只通过 HTTP 调 qqbot-music 的唱歌服务，所以**要先装好 qqbot-music**（换声、分离都在那边，需要显卡）。

## 安装

1. 按 [qqbot-music 的 README](https://github.com/aa1805370178-dot/qqbot-music#快速开始) 装好，确认 `python -m qqbot_music serve` 能起来。
2. 在 MaiBot 插件市场安装本插件，或者把本仓库克隆到 MaiBot 的 `plugins/` 下。
3. 复制 `config.example.toml` 为 `config.toml`（或在 WebUI 里配置），把 `[plugin] enabled` 设为 `true`。
4. 重启 MaiBot。

## 配置

```toml
[service]
url = "http://127.0.0.1:8766"   # 唱歌服务地址
# 服务没开时自动拉起来；留空就要你自己先开服务
start_command = "D:/xxx/seed-vc/env/Scripts/python.exe -m qqbot_music serve"
start_cwd = "D:/xxx/qqbot-music"
start_seconds = 120

[sing]
allow_full = true        # 是否允许唱整首（整首要好几分钟）
chorus_timeout = 600
full_timeout = 3600
voice_rate = 24000       # 发出去的语音采样率
```

## 用起来是什么样

- 有人让麦麦唱某首歌：会唱就开始唱，一两分钟后发语音；不会就去 B 站学（几分钟到十几分钟，看显卡），学会后再点一次。
- 没指定唱哪首：从会唱的歌里随机挑；只说了歌手就在这个歌手的歌里挑。
- 唱失败时会在群里发一句原因。

依赖：MaiBot 自带的 `httpx`、`numpy`；装了 `scipy` 会用它做降采样（没有也能用）。

## 许可证

GPL-3.0-or-later
