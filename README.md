<div align="center">
  <img src="assets/Icons/OlliteRT_Logo_Icon_Stable.png" alt="OlliteRT Icon" width="120" />

  <h1>OlliteRT</h1>

  [**Quick Start**](#quick-start) | [**Screenshots**](#screenshots) | 
  [**Features**](#features) | [**Models**](#available-models) | [**Integrations**](#integrations) | [**API**](#api-endpoints) | [**FAQ**](#faq--troubleshooting) | 
  [**Report a bug**](https://github.com/NightMean/ollitert/issues/new?template=01_bug_report.yml) 

  <p><strong>Turn your Android phone into an OpenAI-compatible API LLM server — fully local, private, and open source</strong></p>

  <div>
    <a href="https://github.com/NightMean/ollitert/releases/latest"><img src="https://img.shields.io/github/v/release/NightMean/ollitert?include_prereleases&style=flat" alt="GitHub Release" /></a>
    <a href="https://github.com/NightMean/ollitert/releases"><img src="https://img.shields.io/github/downloads/NightMean/ollitert/total?style=flat" alt="Downloads" /></a>
    <a href="https://www.buymeacoffee.com/nightmean"><img src="https://img.shields.io/badge/Buy_Me_a_Coffee-FFDD00?logo=buymeacoffee&logoColor=black" alt="Buy Me a Coffee" /></a>
    <br />
    <img src="https://img.shields.io/badge/OpenAI_Compatible-412991?logo=openai&logoColor=white" alt="OpenAI Compatible" />
    <img src="https://img.shields.io/badge/Anthropic_Compatible-D97757?logo=anthropic&logoColor=white" alt="Anthropic Compatible" />
    <br />  
    <img src="https://img.shields.io/badge/Android_12+-34A853?logo=android&logoColor=white" alt="Android 12+" />
    <a href="LICENSE"><img src="https://img.shields.io/github/license/NightMean/ollitert?style=flat" alt="License" /></a>
  </div>

</div>
<h1></h1>


## What is OlliteRT?

**Think of it as [Ollama](https://ollama.com) for Android.** Pick a model, tap Start, and your phone becomes an LLM server — runs LLMs on your mobile GPU/CPU via Google's [LiteRT-LM](https://github.com/google-ai-edge/LiteRT-LM) runtime and serves them as a standard [OpenAI-compatible HTTP API](https://platform.openai.com/docs/api-reference) on your local network.

**No cloud. No API keys. No subscriptions. Just your phone.**

## Features
- **Multi-model Support** — One-tap download from HuggingFace, import `.litertlm` files or model lists from local storage, or add custom model sources via JSON file or URL
- **Multimodal & Reasoning** — Vision, audio, thinking, streaming support, and tool calling (experimental) for capable models
- **Benchmark Built-in** — Test and compare models on your device to find the best fit for your hardware
- **Activity Logs** — Detailed request/response logs with search, filtering, and JSON highlighting
- **Always On, Low Power** — Configurable auto-start on boot, sips ~5-10W vs 300W+ for a GPU server — perfect for that old phone in your drawer*
- **Highly Configurable** — Per-model inference settings, GPU/CPU accelerator, idle model unload, listener scope, client IP access rules, bearer token auth, and more
- **Model & Server Monitoring** — Live stats dashboard, optional movable floating monitor for live background metrics, [Prometheus metrics](docs/integrations/PROMETHEUS.md) for Grafana, and [Home Assistant REST API](docs/integrations/HOME_ASSISTANT.md) for remote server control
- **Broad Compatibility** — Home Assistant, Open WebUI, OpenClaw, Python, curl — if it talks to OpenAI, it works

> [!NOTE]
> Home Assistant currently requires a custom integration such as [Extended OpenAI Conversation](https://github.com/jekalmin/extended_openai_conversation) or [Local OpenAI LLM](https://github.com/skye-harris/hass_local_openai_llm) and [OpenAI STT](https://github.com/NightMean/OpenAI_STT_HASS) for voice commands — see the [Home Assistant client setup](docs/CLIENT_SETUP.md#home-assistant)

<sub>* I am not responsible for any swollen batteries, crispy phones, or spontaneous pocket warmers. Please don't run your LLM on your phone while it's under your pillow. You've been warned.</sub>


## Screenshots

<p align="center">
  <img src="assets/Screenshots/OlliteRT_Screen_Models.png" width="23%" alt="Models" />
  <img src="assets/Screenshots/OlliteRT_Screen_Models_Inference.png" width="23%" alt="Inference" />  
  <img src="assets/Screenshots/OlliteRT_Screen_Status.png" width="23%" alt="Status" />
  <img src="assets/Screenshots/OlliteRT_Screen_Logs.png" width="23%" alt="Logs" />
</p>

## Quick Start

1. **Download & install** the APK
   <br><a href="https://github.com/NightMean/ollitert/releases/latest"><img src="assets/Github/Download_Get_it_on_Github.png" alt="Get it on GitHub" height="45" /></a>
2. **Download a model** — **Gemma 4 E2B** is recommended for most devices (2.4 GB, runs on 8 GB RAM)
3. **Start the server** — Tap the Start Server button on the downloaded model card
4. **Configure your client** — Use the endpoint shown on the Status screen (e.g. `http://PHONE_IP:8000/v1`) with any OpenAI-compatible client — Open WebUI, OpenClaw, Home Assistant, Python, etc. See **[Client Setup](docs/CLIENT_SETUP.md)** for detailed guides.

> [!IMPORTANT]
> Requires: Android 12+ · **arm64-v8a** device · 6 GB RAM minimum · 8 GB+ recommended for multimodal models (see [model table](#available-models))

## 中文说明 · 国内下载与云端打包

- **中文界面**：已内置简体中文（`zh-CN`）资源，系统语言为中文时自动显示中文界面。
- **应用下载支持断点续传**：请从 [GitHub Releases](https://github.com/ssmhdssmhd/OlliteRT/releases) 下载 APK。Release 资产支持 HTTP Range，可用 IDM、aria2 或多线程下载器断点续传；Actions 页面里的 Artifact（zip）**不支持断点续传**，仅建议临时测试使用。
- **国内加速**：在 Release 直链前加上镜像前缀即可，例如：

  ```text
  https://ghproxy.net/https://github.com/ssmhdssmhd/OlliteRT/releases/download/<tag>/<apk>
  https://ghfast.top/https://github.com/ssmhdssmhd/OlliteRT/releases/download/<tag>/<apk>
  ```

  第三方镜像可能失效，失效时请改用直链或更换镜像。
- **模型下载**：应用内模型下载已支持断点续传（自动使用 HTTP Range 从已下载位置继续），网络中断后重新点击下载即可续传。
- **国内模型下载**：无法直连 `huggingface.co` 时会自动回退到 `hf-mirror.com`，可在 **设置 → Hugging Face Token → 国内加速镜像** 关闭。下载受限（gated）模型时，已配置的 Hugging Face 令牌会发送给该第三方镜像；如不希望共享令牌，请关闭该开关（关闭后国内网络将无法下载受限模型）。

### 使用 GitHub Actions 云端打包

1. 打开仓库 **Actions** → 选择 **“云端打包并发布 APK（稳定版/测试版/开发版）”** → **Run workflow**。
2. 勾选 **“仅云端打包”**（默认开启），选择渠道 `stable` / `beta` / `dev`，点击运行即可，无需创建标签。
3. 构建完成后在该次运行的 **Artifacts** 中下载 zip，或在运行摘要中查看 APK 信息。
4. 如需正式发布：取消“仅云端打包”，填写版本标签（如 `v0.9.8`），勾选“创建 GitHub Release”，构建完成后会自动生成中文 Release 说明并上传 APK 与 SHA256。

产物命名规则：`OlliteRT.<渠道>.<版本号>.<yyyyMMddHHmm>.apk`（例如 `OlliteRT.stable.0.9.8.202611042130.apk`），全部使用点号分隔，不使用连字符。

### 签名

CI 使用仓库 Secrets 中的固定签名（`KEYSTORE_BASE64` / `STORE_PASSWORD` / `KEY_ALIAS` / `KEY_PASSWORD`），所有版本签名一致，可覆盖安装，不会出现签名冲突。

## Available Models

| Model | Size | Min RAM | Context | Capabilities |
|:------|-----:|--------:|--------:|:-------------|
| **Gemma 4 E2B** ⭐ | 2.4 GB | 8 GB | 32K | Text · Vision · Audio · Thinking · Tools · MTP |
| **Gemma 4 E4B** ⭐ | 3.4 GB | 12 GB | 32K | Text · Vision · Audio · Thinking · Tools · MTP |
| **Gemma 3n E2B** | 3.4 GB | 8 GB | 4K | Text · Vision · Audio |
| **Gemma 3n E4B** | 4.6 GB | 12 GB | 4K | Text · Vision · Audio |
| **Gemma 3 1B** | 0.5 GB | 6 GB | 1K | Text |
| **Qwen 2.5 1.5B** | 1.5 GB | 6 GB | 4K | Text |
| **DeepSeek-R1 1.5B** | 1.7 GB | 6 GB | 4K | Text |

⭐ Recommended — E2B for most devices, E4B for high-end

> [!NOTE]
> Tool calling is experimental and may not always be reliable due to model limitations.

See the **[Model Guide](docs/MODELS.md)** for recommendations, capability details, and import instructions.

## Integrations

- **[Prometheus metrics](docs/integrations/PROMETHEUS.md)** — `/metrics` endpoint with 29 metrics for Grafana, Datadog, etc.
- **[Home Assistant REST API](docs/integrations/HOME_ASSISTANT.md)** — monitor server status, control model, update settings remotely

## API Endpoints

<details>
<summary><strong>Available endpoints — click to expand</strong></summary>

| Method | Endpoint | Description |
|:-------|:---------|:------------|
| `POST` | `/v1/chat/completions` | OpenAI Chat Completions API (streaming + non-streaming) |
| `POST` | `/v1/completions` | OpenAI Completions API |
| `POST` | `/v1/responses` | OpenAI Responses API |
| `POST` | `/v1/messages` | Anthropic Messages API (streaming + non-streaming) |
| `POST` | `/v1/messages/count_tokens` | Anthropic input-token estimator |
| `POST` | `/v1/audio/transcriptions` | Audio transcription |
| `GET`  | `/v1/models` | List available models |
| `GET`  | `/v1/models/{id}` | Get detail for a specific model |
| `GET`  | `/` or `/v1` | Server info (version, status, endpoints) |
| `GET`  | `/health` | Health check (with optional `?metrics=true`) |
| `GET`  | `/metrics` | Prometheus metrics |
| `GET`  | `/ping` | Simple liveness check |
| `GET`  | `/v1/server/config` | Read model and server configuration |
| `POST` | `/v1/server/config` | Update model and server configuration |

</details>

Full API docs and examples: **[docs/api/API.md](docs/api/API.md)**

## Limitations

<details>
<summary><strong>Known limitations — click to expand</strong></summary>

- **arm64-v8a only** — other architectures (armeabi-v7a, x86, x86_64) are not supported. The LiteRT runtime ships native libraries for x86_64 but they crash on Android emulators due to unsupported CPU instructions. Nearly all Android devices from 2017+ are arm64-v8a.
- **Single model, single request** — one model loaded at a time, requests queue sequentially (LiteRT SDK limitation). On-demand model loading via client requests is planned for a future release.
- **Tool calling is model-dependent** — Native tool calling requires models trained for function calling (such as Gemma 4). For models that don't support native tool calling, you can disable **Tool Schema Injection** in settings to use prompt-based fallback parsing instead.
- **Token counts are estimated** — the LiteRT runtime doesn't expose a tokenizer API, so counts are approximated using character length ÷ 4. Reasonably accurate for English text, less so for code or multilingual content.
- **Imported models are copied to app storage** — when importing a model from your device, the file is copied rather than moved. You can delete the original after import to reclaim space.
- **No GGUF support** — only `.litertlm` models are supported (LiteRT runtime limitation). Models are available from the [LiteRT Community on HuggingFace](https://huggingface.co/litert-community). Advanced users can convert HuggingFace models to `.litertlm` using Google's [`litert-torch`](https://github.com/google-ai-edge/litert-torch) tooling (Linux, 32GB+ RAM required).
- **LiteRT runtime constraints** — OlliteRT is built on Google's [LiteRT-LM](https://github.com/google-ai-edge/LiteRT-LM) runtime, optimized for mobile. Features like logprobs, grammar-based output constraints, repetition penalties, and LoRA adapters are not available.

</details>

## FAQ & Troubleshooting

- **[FAQ](docs/FAQ.md)** — Model support, privacy, battery, architecture, tool calling
- **[Troubleshooting](docs/TROUBLESHOOTING.md)** — Connection issues, performance, crashes, auto-start, storage

## Privacy & Security

- **[Privacy Policy](docs/PRIVACY_POLICY.md)** — no data is collected, no telemetry, no analytics
- **[Security Guide](docs/SECURITY.md)** — bearer token auth, network exposure, HTTPS, securing your server

## Contributing

- Found a bug? [Report it here](https://github.com/NightMean/ollitert/issues/new?template=01_bug_report.yml)
- Want to request a feature? [Open an issue](https://github.com/NightMean/ollitert/issues/new)

## Building from Source

- **[Building](docs/BUILDING.md)** — build instructions, signing setup, lint, and tests
- **[Architecture](docs/ARCHITECTURE.md)** — package structure, request flow, and dependency list

Product flavors — all installable side-by-side:

| Flavor | Icon | Purpose |
|:-------|:----:|:--------|
| `stable` | <img src="assets/Icons/OlliteRT_Logo_Icon_Stable.png" width="28" /> | Stable release |
| `beta` | <img src="assets/Icons/OlliteRT_Logo_Icon_Beta.png" width="28" /> | Beta testing |
| `dev` | <img src="assets/Icons/OlliteRT_Logo_Icon_Dev.png" width="28" /> | Local development |

## Support the Project

What happens on your phone stays on your phone. If that matters to you, consider supporting OlliteRT.

<p align="center">
  <a href="https://github.com/sponsors/NightMean"><img src="https://img.shields.io/badge/Sponsor-ea4aaa?style=for-the-badge&logo=githubsponsors&logoColor=white" /></a>&nbsp;
  <a href="https://www.buymeacoffee.com/nightmean"><img src="https://img.shields.io/badge/Buy_Me_a_Coffee-FFDD00?style=for-the-badge&logo=buymeacoffee&logoColor=black" /></a>&nbsp;
  <a href="https://ko-fi.com/nightmean"><img src="https://img.shields.io/badge/Ko--fi-FF5E5B?style=for-the-badge&logo=kofi&logoColor=white" /></a>
</p>

## Credits

- **[Google AI Edge Gallery](https://github.com/google-ai-edge/gallery)** — Original project this was built upon
- **[LiteRT-LM](https://github.com/google-ai-edge/LiteRT-LM)** — Google's on-device AI runtime
- **[Ktor](https://ktor.io/)** — Coroutine-based HTTP server framework

## License

Licensed under the [Apache License 2.0](LICENSE).

