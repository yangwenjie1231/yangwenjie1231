<div align="center">

<img src="https://readme-typing-svg.demolab.com/?font=Fira+Code&weight=600&size=22&pause=1000&color=2ECC71&center=true&vCenter=true&lines=RISC-V+Vector+Acceleration;Edge+AI+%26+Embedded+Vision;Full-Stack+Systems+Engineering" alt="Typing SVG" />

<h1>Wenjie Yang</h1>

<p>
  <a href="https://github.com/yangwenjie1231"><img src="https://img.shields.io/badge/GitHub-yangwenjie1231-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" /></a>
  <a href="mailto:yangwenjie1231@qq.com"><img src="https://img.shields.io/badge/Email-yangwenjie1231%40qq.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <img src="https://komarev.com/ghpvc/?username=yangwenjie1231&color=2ECC71&style=flat-square&label=visitors" alt="visitors" />
</p>

**高二｜RISC-V 向量加速 · 端侧视觉 · 全栈工程**

</div>

---

## ⚡ sg2002_rvv · RISC-V RVV 向量加速库

> 原创 · LGPL-3.0 · [仓库](https://github.com/yangwenjie1231/sg2002_rvv)

面向 **RVV 0.7.1**（SG2002 / C906FDV）的 NumPy 兼容向量加速库。目标平台是嵌入式 Linux ——
这类环境通常**装不了 NumPy**，所以整条链路的设计都绕着这件事做。

| 设计点 | 为什么这么做 |
|--------|--------------|
| **wheel 不依赖 NumPy**（`install_requires=[]`） | 嵌入式 Linux 上 NumPy 常常编译不出来；库本身要能独立装上 |
| **双输入路径** | 有 NumPy 时收 `ndarray` 并返回 `ndarray`（pybind11 `py::array_t<float>`）；没有时走裸 buffer，校验 `format=='f'` 且 `itemsize==4` |
| **自动规整** | 传入非 float32 或非连续数组时，内部 `as_f32_buffer()` 先转换/拷贝成连续 float32 再算 |
| **可复现基准** | 自带基准脚本与示例数据，性能结论不是口头声明 |

做它是因为我另一个项目需要向量加速，做完把实现抽成独立库开了源。

---

## 🔧 工程实现细节

### dsh-zhuang-fangyi-pet · 把窗口真正放到桌面上

一个 DSH 插件生态里的桌面宠物。「浮在桌面上」这件事，常规候选方案是窗口内 overlay / 自带 Electron / Tauri / 借主进程开窗，都各有代价。

选的是第四种：**由插件宿主用官方 `ctx.subprocess` 接缝，拉起一个自编译的 .NET Framework 4.8 小 exe**，由它自建无边框 + 透明 + 置顶 + **alpha 点击穿透**窗口，再经 HTTP/SSE 连回宿主拿 agent 状态。

| 维度 | 窗口内 overlay | 自带 Electron | 本方案 |
|---|---|---|---|
| 真浮于桌面 | ❌ | ✅ | ✅ |
| 额外内存 | 0 | +80~150 MB | ~50 MB |
| 交付体积 | 0 | 一整个 Electron | **~12 KB 空壳** |

安全上是三道围栏：原生 exe 带一次性令牌（每次启动随机、经 argv 传递、不落盘、常量时间比较）；浏览器半边带不了请求头，走同源信任围栏（仅 loopback Host、拒 cross-site、校验 Origin/Referer）；素材走 `pet.json` 派生的白名单并二次校验 `path.resolve` 仍在 `art/pet` 内。

### dsh-zhuang-fangyi-voice · 双后端推理

同一套音色推理，两个后端按场景选：

| 后端 | 依赖 | RTF | 适用 |
|------|------|-----|------|
| **onnx**（默认） | 仅 onnxruntime | ≈ 6 | 分发、无显卡机器、跨平台 |
| **torch** | torch + GPT-SoVITS 源码 | **≈ 0.45 @GPU** | 自己机器、批量生成 |

配套 `tools/diagnose_voice.py` 逐项检查音频电平（削顶最常被误判成气声）、6–10kHz 能量与谱平坦度、SoVITS/GPT 权重版本头、参考音频、推理环境、采样参数、缓存 —— 把「声音不对」定位到具体某一环，而不是猜。

### dsh-zhuang-fangyi · 8 套预设 × 双明暗

接入官方 `ctx.theme` 体系，8 套风格预设（明度 / 色度 / 边框 / 材质 / 排版）× 浅色深色 = 16 个主题。两个值得一提的约束：

- **强调色任意色相 0–359°**，明度按对比度自动校正，配 672 项色相扫描兜底
- **桌面端与网页端是两套类名完全不同的壳**，插件用「语义锚点 → 哈希反查 → 后缀兜底」三层定位同时兼容

### zfy-v5 · GPT-SoVITS v5 微调工作区

脚本、结论与参考音频。三种语气（正常 / 强硬 / 娇）均经盲听确认可用，差异在语气而非质量。

---

## 🌟 开源贡献

累计 **97 个已合并 PR**：

| 项目 | 规模 | 我的贡献 |
|------|------|----------|
| [sipeed **picoclaw**](https://github.com/sipeed/picoclaw) | 30.0K ⭐ · Go | 2 个已合并 PR · 飞书卡片解析、卡片/文件回复上下文补全 |
| [**MaaEnd**](https://github.com/MaaEnd/MaaEnd) | 4.3K ⭐ · C++ | 3 个已合并 PR · 修复送货任务重试无上限导致的无限刷新循环 |
| [sipeed **MaixPy**](https://github.com/sipeed/MaixPy) | 867 ⭐ · Python | 5 个已合并 PR · RVV 加速文档（中英双语 + 侧边栏注册）、camera / linux_basic / llm_deepseek 文档维护 |
| [**huangshifu-wiki**](https://github.com/huangshifu-wiki/huangshifu-wiki) | 团队项目 · TypeScript | 82 个已合并 PR · 前后端、S3 存储、Blurhash 占位图、Service Worker 与 CSP、UI 组件重构 |
| [sipeed **sipeed_wiki**](https://github.com/sipeed/sipeed_wiki) | 189 ⭐ · JavaScript | 1 个已合并 PR · 文档维护 |

[**黄诗扶 Wiki**](https://huangshifu.wiki/) —— 团队全栈社区平台（Wiki / 帖子 / 图库 / 音乐资料 / 语义搜索），已上线，早期核心开发。
技术栈：React · Express · PostgreSQL · Qdrant。

---

## 🛠 技术栈

<table>
<tr>
  <th align="center">语言</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-C%2FC%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white" />
    <img src="https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white" />
    <img src="https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white" />
    <img src="https://img.shields.io/badge/-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
    <img src="https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black" />
    <img src="https://img.shields.io/badge/-C%23-512BD4?style=flat-square&logo=dotnet&logoColor=white" />
  </td>
</tr>
<tr>
  <th align="center">AI / ML</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" />
    <img src="https://img.shields.io/badge/-ONNX-005CED?style=flat-square&logo=onnx&logoColor=white" />
    <img src="https://img.shields.io/badge/-YOLO-00FFFF?style=flat-square&logo=yolo&logoColor=black" />
    <img src="https://img.shields.io/badge/-MediaPipe-0097A7?style=flat-square&logo=google&logoColor=white" />
  </td>
</tr>
<tr>
  <th align="center">底层 / 嵌入式</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-RISC--V-283272?style=flat-square&logo=riscv&logoColor=white" />
    <img src="https://img.shields.io/badge/-RVV%20%2F%20Vector-2ECC71?style=flat-square&logo=ri&logoColor=white" />
    <img src="https://img.shields.io/badge/-pybind11-3776AB?style=flat-square&logo=python&logoColor=white" />
    <img src="https://img.shields.io/badge/-Linux-FCC624?style=flat-square&logo=linux&logoColor=black" />
    <img src="https://img.shields.io/badge/-MaixCAM%20%2F%20SG2002-2ECC71?style=flat-square&logo=ri&logoColor=white" />
  </td>
</tr>
<tr>
  <th align="center">全栈 / 桌面</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-Electron-47848F?style=flat-square&logo=electron&logoColor=white" />
    <img src="https://img.shields.io/badge/-.NET%20WPF-512BD4?style=flat-square&logo=dotnet&logoColor=white" />
    <img src="https://img.shields.io/badge/-React-61DAFB?style=flat-square&logo=react&logoColor=black" />
    <img src="https://img.shields.io/badge/-NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white" />
    <img src="https://img.shields.io/badge/-PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" />
  </td>
</tr>
</table>

---

<sub>另外做过一个端侧活细胞成像方向的项目（Cell Vision Pro，产品负责人 + 全栈），未公开。</sub>

---

## 📊 GitHub

<sub>卡片由本仓库的 <a href=".github/workflows/metrics.yml">Metrics Action</a> 每小时生成并提交进仓库 —— 自托管，不依赖第三方服务。</sub>

<div align="center">

<img src="./github-metrics.svg" alt="GitHub Metrics" />

[![GitHub Streak](https://streak-stats.demolab.com/?user=yangwenjie1231&theme=vue-dark&hide_border=true&locale=zh_Hans)](https://github.com/yangwenjie1231)

</div>

---

<div align="center">
  <sub>也做一些端侧视觉与产品化的活</sub>
</div>
