# 30 篇论文使用的眼动特征频率统计

## 编码口径

- 频率单位：按论文计数。同一篇论文多次提到同一特征，只计 1 次。
- 特征归一化：将同义表达合并，例如 `gaze point / point-of-gaze / fixation location` 统一为“注视点 / 凝视坐标”。
- 正向/负向：不是统计回归系数，而是按论文中的使用角色编码。`正向` 表示该特征被用作支持预测、识别、分类或解释的有效信号；`负向` 表示该特征主要指向异常、风险、遮挡、中断或负类线索；方向不稳定时标为 `混合/任务相关`。
- 来源：每篇论文的 `summary.txt` + 本地 PDF 全文关键词查漏。

## 频率表

| 排名 | 眼动特征 | 归一化/同义表达 | 出现频率 | 涉及论文 | 正向/负向特征 | 判定依据 |
|---:|---|---|---:|---|---|---|
| 1 | 注视点 / 凝视坐标 | gaze point, point-of-gaze, fixation point/location, gaze location | 13/30 | Fuhl-2021; Huang-2021; Jin-2024; Lin(GazeHTA)-2024; Liu(GEM)-2024; Mathew-2025; Ryan-2024; Seraj-2024; Shi-2024; Tonini-2023; Tonini-2024; Tu-2022; Wu-2023 | 正向为主 | 多数论文把注视点/坐标作为定位、回归、聚类或热力图监督的核心有效信号；在 ASD 论文中也可作为异常差异线索。 |
| 2 | 注视目标 / 被注视对象 | gaze target, gaze object, gazed object, attended object | 12/30 | Dai-2025; Jin-2024; Lin(GazeHTA)-2024; Mathew-2025; Ryan-2024; Seraj-2024; Song-2024; Toaiari-2024; Tonini-2022; Tonini-2023; Tonini-2024; Tu-2022 | 正向 | 通常是模型要检测/预测的目标或监督信号，出现代表对 gaze target 判断有直接贡献。 |
| 3 | 显著图 / 热力图 / 注意图 | saliency map, gaze heatmap, attention map, gaze map | 12/30 | Jin-2024; Lin(GazeHTA)-2024; Martin-2022; Mathew-2025; Moroto-2023; Rong-2021; Ryan-2024; Song-2024; Tonini-2022; Tonini-2023; Tonini-2024; Wang-2021 | 正向 | 作为空间注意、显著性或 gaze supervision 表示，论文一般用其提高分类、目标检测或 scanpath 预测。 |
| 4 | 扫视路径 / 凝视序列 | scanpath, visual scanpath, fixation sequence, gaze sequence | 8/30 | Abawi-2024; Chen(GazeXplain)-2024; Chen(Individualized)-2024; Fang-2024; Kerkouri-2021; Martin-2022; Wang-2021; Xue-2025 | 正向 | 被用来刻画动态视觉注意过程，是 scanpath prediction 和个体化预测的主要建模对象。 |
| 5 | 凝视方向 / 凝视角度 | gaze direction, gaze angle, pitch/yaw gaze angles, 3D gaze direction | 7/30 | Abdelrahman-2022; Dai-2025; Huang-2021; Mathew-2025; Ryan-2024; Toaiari-2024; Tonini-2022 | 正向 | 通常作为 gaze estimation 的预测目标或 gaze target 推理的空间方向线索。 |
| 6 | AOI / ROI / 对象区域 | AOI, ROI, object region, object-level region, gazed-object region | 7/30 | Fang-2024; Jin-2024; Mathew-2025; Shi-2024; Song-2024; Tonini-2022; Tonini-2023 | 正向为主 | 多数论文用区域/对象级表示帮助定位被注视对象；在 ASD 或行为差异分析中区域分布也可能作为负向/异常线索。 |
| 7 | 眼跳 / 凝视转移 | saccade, gaze shift, transition, fixation transition | 6/30 | Chen(GazeXplain)-2024; Chen(Individualized)-2024; Fuhl-2021; Kerkouri-2021; Martin-2022; Wang-2021 | 混合/任务相关 | 在 scanpath 中是有用的时序转移信号；但过大、异常或不稳定的转移在部分任务中可能代表偏差或噪声。 |
| 8 | 凝视历史 / 时间上下文 | fixation history, previous fixation, temporal gaze context, time-evolving scanpath | 4/30 | Abawi-2024; Chen(Individualized)-2024; Fang-2024; Martin-2022 | 正向 | 用于递归预测后续 fixation/scanpath，论文中通常证明历史上下文能提升个体化或动态预测。 |
| 9 | 个体化观察者 / 被试特征 | observer feature, subject embedding, personalized gaze pattern, interpersonal gaze pattern | 4/30 | Abawi-2024; Chen(Individualized)-2024; Moroto-2023; Xue-2025 | 正向 | 作为个体差异建模信号，帮助个性化 saliency 或 scanpath 预测。 |
| 10 | 瞳孔中心 / 瞳孔位置 / 分割 | pupil center, pupil position/location, pupil segmentation | 3/30 | Fuhl-2021; Lin(FAPNet)-2024; Sen-2024 | 正向 | 事件相机或眼动分割论文将其作为眼动追踪的核心几何信号。 |
| 11 | 视觉搜索行为图 / 高阶关系 | visual search behavior, gaze graph, behavior graph, higher-order gaze relation | 2/30 | Fang-2024; Liu(GEM)-2024 | 正向 | 用于表达视觉搜索过程或 gaze points 之间的关系，帮助预测/匹配专家搜索行为。 |
| 12 | 事件相机眼动信号 | event stream, event slicing, event point cloud, event-based eye signal | 2/30 | Lin(FAPNet)-2024; Sen-2024 | 正向 | 用于低延迟、细粒度眼动追踪，作为 RGB 信号的高时间分辨率替代。 |
| 13 | 瞳孔速度 / 加速度 / 短时运动 | pupil velocity, pupil acceleration, short-term pupil motion, kinematics | 2/30 | Lin(FAPNet)-2024; Sen-2024 | 正向 | 用于自适应追踪频率或用户认证，论文将其作为有效的运动学特征。 |
| 14 | 深度层级 / 3D 凝视 | depth-level gaze, depth estimation, 3D gaze target/direction | 2/30 | Seraj-2024; Toaiari-2024 | 正向 | 用于区分注视目标的空间深度层级或 3D 目标位置，直接支持 3D gaze target detection。 |
| 15 | 眼睑闭合 / 眨眼 | blink, eyelid closure, lid closure | 1/30 | Fuhl-2021 | 混合/偏负向 | 可作为眼动分割类别或多模态信号；在追踪任务中常表示遮挡/中断，因此方向偏负向但不宜简单归为坏特征。 |
| 16 | 聚类有效性 / gaze pattern 差异指标 | cluster validity indices, gaze pattern clustering, ASD-vs-TD gaze pattern difference | 1/30 | Shi-2024 | 负向/异常线索 | 用于识别 ASD 与典型发育儿童的 gaze pattern 差异，主要指向诊断风险或异常模式。 |
| 17 | 眼神接触状态 | eye contact, eye-contact detector | 1/30 | Dai-2025 | 正向 | 作为机器人感知中判断人是否与系统/场景建立 gaze interaction 的条件信号。 |

## 简要结论

- 最高频的是空间定位类特征：注视点/凝视坐标、注视目标/被注视对象、显著图/热力图。说明这 30 篇论文的主线集中在 gaze target、gaze following、scanpath prediction 和 saliency/gaze supervision。
- 时序动态类特征次之：scanpath、fixation history、saccade/gaze shift 主要出现在 scanpath prediction、个体化注意建模和可解释 scanpath 论文中。
- 生理/传感器类特征较少：瞳孔中心、瞳孔速度/加速度、event camera signal 主要集中在 FAPNet 和 EyeTrAES 这类低延迟眼动追踪论文。
- 明确负向或偏负向的特征较少，主要是 ASD gaze pattern 差异、眨眼/眼睑闭合这类异常、遮挡或中断线索；多数特征在论文中是预测目标或有效输入，因此方向为正向或任务相关。
