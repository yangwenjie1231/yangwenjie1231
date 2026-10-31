<div align="center">

<!-- Typing SVG -->
<img src="https://readme-typing-svg.demolab.com/?font=Fira+Code&weight=600&size=22&pause=1000&color=2ECC71&center=true&vCenter=true&lines=Live-Cell+Imaging+%C2%B7+Edge+AI;Full-Stack+Product+Engineer;RISC-V+Vector+Acceleration;Tooling+%26+Agent+Plugin+Author" alt="Typing SVG" />

<h1>Wenjie Yang</h1>

<p>
  <a href="https://github.com/yangwenjie1231"><img src="https://img.shields.io/badge/GitHub-yangwenjie1231-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" /></a>
  <a href="mailto:yangwenjie1231@qq.com"><img src="https://img.shields.io/badge/Email-yangwenjie1231%40qq.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <img src="https://komarev.com/ghpvc/?username=yangwenjie1231&color=2ECC71&style=flat-square&label=visitors" alt="visitors" />
</p>

**高二｜智能活细胞成像 · 端侧视觉 · RISC-V 加速**

<sub>主线是把实验室设备做成产品，副线折腾工具链，顺手把有用的东西开源出来</sub>

</div>

---

## 🚀 主线：Cell Vision Pro · 千元级智能活细胞成像系统

> 产品负责人 + 全栈开发 · 私有仓库

把一套原本只在实验室里、动辄十几万的活细胞成像方案，压到**千元级**并做成能直接用的产品：从相机取流、培养状态分析、AI 推理，到桌面端与服务端的一整条链路。

| 维度 | 做了什么 |
|------|----------|
| **硬件与端侧** | MaixPy / MaixCAM 取流与设备侧推理，图像增强走 Real-ESRGAN x2（ONNX） |
| **桌面端** | Electron + React + TypeScript，插件化架构（V5 重构），自动化 CI / e2e |
| **服务端** | NestJS 服务、设备与告警链路、SSRF 防御与安全加固 |
| **工程化** | 模型权重与安装包解耦 —— 权重按需下载、可自替换、可镜像 |

配套的模型分发仓库是公开的：[**Cell-Vision-Models**](https://github.com/yangwenjie1231/Cell-Vision-Models) ——
推理权重（ONNX）以 Release 附件形式提供，应用按需下载到 `<userData>/models/`，
用户可自带权重覆盖；下载地址支持多源回退（Gitee 优先、GitHub 兜底）。

<details>
<summary><b>为什么权重不放进安装包</b></summary>

三个理由，都是踩过坑之后才定下来的：

1. **安装包体积** —— 单个模型可达数十 MB，塞进去每次 clone 都很重
2. **可替换** —— asar 是只读的，模型放里面用户就没法换自己的权重
3. **便于镜像** —— 单仓库 + 固定文件名，方便同步到国内镜像

</details>

---

## 🧪 最近在做（2026 Q3–Q4）

兴趣驱动的副线，但工程标准按产品线来要求。都在 DeepSeek Harness（DSH）插件生态里。

<table>
<tr><th align="center">项目</th><th align="center">一句话</th><th align="center">几个实现细节</th></tr>
<tr>
<td><b><a href="https://github.com/yangwenjie1231/dsh-zhuang-fangyi">dsh-zhuang-fangyi</a></b><br/><sub>主题插件 · v0.12.1</sub></td>
<td>8 套风格预设 × 浅色/深色 = 16 个主题，接入官方 <code>ctx.theme</code> 体系</td>
<td>壁纸竖图自动 <code>contain</code> + 模糊垫底（不裁人）；强调色任意色相 0–359° 且明度按对比度自动校正；观测台作为官方右栏标签页而非浮层</td>
</tr>
<tr>
<td><b><a href="https://github.com/yangwenjie1231/dsh-zhuang-fangyi-pet">dsh-zhuang-fangyi-pet</a></b><br/><sub>桌宠</sub></td>
<td>真的浮在桌面上，不是窗口内悬浮层</td>
<td>由插件宿主 <code>ctx.subprocess</code> 拉起自编译的 .NET Framework 4.8 小 exe，自建无边框 + 透明 + 置顶 + <b>alpha 点击穿透</b>窗口，SSE 回传状态；交付体积 ~12 KB 空壳</td>
</tr>
<tr>
<td><b><a href="https://github.com/yangwenjie1231/dsh-zhuang-fangyi-voice-v2">dsh-zhuang-fangyi-voice</a></b><br/><sub>音色合成 · v0.2.0</sub></td>
<td>任意中文台词用指定音色念出来，ONNX / torch 双后端</td>
<td>ONNX 后端 RTF ≈ 6（无需 CUDA / torch），torch 后端 RTF ≈ 0.45 @GPU；三种语气可切；带诊断脚本逐项定位「声音不对」是哪一环</td>
</tr>
<tr>
<td><b><a href="https://github.com/yangwenjie1231/zfy-v5">zfy-v5</a></b><br/><sub>微调工作区</sub></td>
<td>GPT-SoVITS v5 全量微调的脚本、结论与参考音频</td>
<td>三种语气（正常 / 强硬 / 娇）均为盲听确认可用，差异在语气而非质量；切换脚本同步更新参考音频与参考文本</td>
</tr>
<tr>
<td><b><a href="https://github.com/yangwenjie1231/AgentHub">AgentHub</a></b><br/><sub>fork · 独立维护分支</sub></td>
<td>基于上游 v1.82.2 自维护「反代网关」板块</td>
<td>上游自 v1.83.0 起停更该模块，本分支回退并自行维护协议适配；非官方、非商业用途</td>
</tr>
</table>

---

## 🌟 开源贡献

累计 **97 个已合并 PR**，主要集中在这几个上游仓库：

| 项目 | 规模 | 我的贡献 |
|------|------|----------|
| [sipeed **picoclaw**](https://github.com/sipeed/picoclaw) | 30.0K ⭐ · Go | 2 个已合并 PR · 飞书卡片解析、卡片/文件回复上下文补全 |
| [**MaaEnd**](https://github.com/MaaEnd/MaaEnd) | 4.3K ⭐ · C++ | 3 个已合并 PR · 修复送货任务重试无上限导致的无限刷新循环 |
| [sipeed **MaixPy**](https://github.com/sipeed/MaixPy) | 867 ⭐ · Python | 5 个已合并 PR · RVV 加速文档（中英双语 + 侧边栏注册）、camera / linux_basic / llm_deepseek 文档维护 |
| [**huangshifu-wiki**](https://github.com/huangshifu-wiki/huangshifu-wiki) | 团队项目 · TypeScript | 82 个已合并 PR · 前后端、S3 存储、Blurhash 占位图、Service Worker 与 CSP、UI 组件重构 |
| [sipeed **sipeed_wiki**](https://github.com/sipeed/sipeed_wiki) | 189 ⭐ · JavaScript | 1 个已合并 PR · 文档维护 |

[**黄诗扶 Wiki**](https://huangshifu.wiki/) —— 团队全栈社区平台（Wiki / 帖子 / 图库 / 音乐资料 / 语义搜索），已上线，我是早期核心开发。
技术栈：React · Express · PostgreSQL · Qdrant。

<details>
<summary><b>顺手开源的一个库</b></summary>

[**sg2002_rvv**](https://github.com/yangwenjie1231/sg2002_rvv) —— 面向 RISC-V RVV 0.7.1（SG2002 / C906FDV）的 NumPy 兼容加速库，LGPL-3.0。

当时是自己另一个项目需要向量加速，就把实现整理成了独立库放出来。
提供 `add` / `sub` / `dot` / `norm_l2` 等算子，接受 `numpy.ndarray` 并返回 `numpy.ndarray`，
wheel 本身**不依赖 NumPy**（嵌入式 Linux 上通常装不了），附可复现的基准脚本与示例数据。

</details>

---

## 🛠 技术栈

<table>
<tr>
  <th align="center">语言</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white" />
    <img src="https://img.shields.io/badge/-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
    <img src="https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black" />
    <img src="https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white" />
    <img src="https://img.shields.io/badge/-C%2FC%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white" />
  </td>
</tr>
<tr>
  <th align="center">AI / ML</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" />
    <img src="https://img.shields.io/badge/-ONNX-005CED?style=flat-square&logo=onnx&logoColor=white" />
    <img src="https://img.shields.io/badge/-YOLO-00FFFF?style=flat-square&logo=yolo&logoColor=black" />
    <img src="https://img.shields.io/badge/-MediaPipe-0097A7?style=flat-square&logo=google&logoColor=white" />
    <img src="https://img.shields.io/badge/-scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" />
  </td>
</tr>
<tr>
  <th align="center">嵌入式</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-MaixCAM%20%2F%20SG2002-2ECC71?style=flat-square&logo=ri&logoColor=white" />
    <img src="https://img.shields.io/badge/-RISC--V-283272?style=flat-square&logo=riscv&logoColor=white" />
    <img src="https://img.shields.io/badge/-ESP32-E7352C?style=flat-square&logo=espressif&logoColor=white" />
    <img src="https://img.shields.io/badge/-Linux-FCC624?style=flat-square&logo=linux&logoColor=black" />
  </td>
</tr>
<tr>
  <th align="center">全栈</th>
  <td align="center">
    <img src="https://img.shields.io/badge/-Electron-47848F?style=flat-square&logo=electron&logoColor=white" />
    <img src="https://img.shields.io/badge/-React-61DAFB?style=flat-square&logo=react&logoColor=black" />
    <img src="https://img.shields.io/badge/-NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white" />
    <img src="https://img.shields.io/badge/-Node.js-339933?style=flat-square&logo=node.js&logoColor=white" />
    <img src="https://img.shields.io/badge/-PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" />
    <img src="https://img.shields.io/badge/-Docker-2496ED?style=flat-square&logo=docker&logoColor=white" />
  </td>
</tr>
</table>

### 也在做

- **端侧 / 边缘 AI 部署**：模型训练 → 量化 → 边缘硬件落地 → 产品化 的完整链路
- **大模型底层架构与多智能体系统（MAS）**：多引擎协作一致性评估、成本与效应量拆解
- **桌面端原生能力**：WPF / .NET Framework、透明置顶窗、进程间 SSE 状态同步

---

## 📊 GitHub

<sub>下面的卡片由本仓库的 <a href=".github/workflows/metrics.yml">Metrics Action</a> 每小时生成并提交进仓库 —— 自托管，不依赖任何第三方卡片服务。</sub>

<div align="center">

[![GitHub Streak](https://streak-stats.demolab.com/?user=yangwenjie1231&theme=vue-dark&hide_border=true&locale=zh_Hans)](https://github.com/yangwenjie1231)

<img src="./github-metrics.svg" alt="GitHub Metrics" />

</div>

---

<div align="center">
  <sub>这个仓库的 README 就是 <a href="https://github.com/yangwenjie1231">yangwenjie1231</a> 的 GitHub 主页</sub>
</div>
