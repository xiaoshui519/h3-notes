# MiniMax H3 生态笔记

> 跟踪 MiniMax H3 开源生态：官方仓库、ComfyUI 节点、显存实测与许可要点。
> 星数为 2026-11-08 快照，后续按需更新。

## 1. 一手来源

| 仓库 | 星 | 说明 |
|---|---|---|
| [MiniMax-AI/MiniMax-H3](https://github.com/MiniMax-AI/MiniMax-H3) | 11.6k | 官方开源主仓，权重、推理脚本、文档 |
| [MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | — | 模型权重（HuggingFace） |
| [platform.minimax.io](https://platform.minimax.io) | — | 官方 API 与额度 |

## 2. ComfyUI 生态

| 仓库 | 星 | 干什么 |
|---|---|---|
| [ComfyUI-MiniMaxH3-Director](https://github.com/seesee75-commits/ComfyUI-MiniMaxH3-Director) | 345 | 时间线式分镜编辑器：逐镜提示词、首尾帧、参考图/视频/音频、联合音画 |
| [ComfyUI-MiniMaxH3-PrefixStream](https://github.com/knoic/ComfyUI-MiniMaxH3-PrefixStream) | 216 | 长视频续写：Prefix KV 缓存 + 落盘流式，显存只跟单段长度挂钩 |
| [H3-Optimizations](https://github.com/Zironic/H3-Optimizations) | 183 | 显存优化 + 稀疏注意力，速度/质量折中开关 |
| [ComfyUI-MiniMax-H3-TaoMate-C3](https://github.com/sepiablue-ai/ComfyUI-MiniMax-H3-TaoMate-C3) | 41 | 小显存档的三步加速包（W4A4 FFN + 稀疏注意力） |
| [Combined Image And Reference to Video](https://github.com/entropicnoise/MiniMax-H3-Combined-Image-And-Reference-to-Video) | 11 | 首帧 + 参考图/视频/音频的组合输入节点 |
| [MotionCache-FastVAE](https://github.com/Mozer/ComfyUI-MiniMax-H3-MotionCache-FastVAE) | 13 | 批量 Fast VAE 解码 |

## 3. 显存与硬件现实

社区实测口径（864×480 / 5 秒）：

- **25–32 GB 峰值显存**即可跑通，配置为 pruned INT8 + NVFP4 权重组合；
- 24 GB 卡（3090/4090）能跑，但要开流式，且系统内存往往先成为瓶颈；
- 32 GB 卡贴着上限，几乎没有余量；
- **48 GB 及以上属于宽裕档**，可不上流式分片直接出原生分辨率；
- 模型文件整体约 60 GB 量级（33B DiT + 32B 文本编码器 + 视频/音频双 VAE），磁盘和内存比显存更容易先卡住。

长视频拼接的原生方案内存随总时长线性上升，PrefixStream 改为按段落盘后，峰值只取决于单段长度——这是能不能用一张卡堆出十分钟片子的分水岭。

## 4. 许可要点

H3 用的是**社区许可**，不是 Apache 2.0：

- 商业产品或服务年收入 **2000 万美元以下**，且在界面显著标注 MiniMax H3 → 可免费商用；
- 超过该线，或在**美国 / 欧盟 / 英国 / 韩国**部署 → 需事先取得 MiniMax 书面授权。

个人创作、内容账号运营不受影响；做成对外售卖的产品前再回来看这条。

## 5. 怎么持续跟踪

1. `github.com/trending` → 周期选 `This month`，扫标题含 video / comfyui 的项目；
2. 站内搜索关键词：`MiniMax H3`、`H3 comfyui`、`h3 lora`、`h3 inference`；
3. 官方仓 Watch → Custom → Releases，只在发版时收通知；
4. 看到好项目点 Star，Stars 页就是一张可按时间回看的技术雷达。

## 6. 更新记录

- 2026-11-09 建仓，收录 9 个仓库，星数与显存数据为 11-08 快照。
