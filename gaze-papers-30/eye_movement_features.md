# 50 篇论文使用的眼动特征频率统计

## 编码口径

- 频率单位：按论文计数。同一篇论文多次提到同一特征，只计 1 次。
- 特征归一化：将同义表达合并，例如 `fixation duration / dwell duration / gaze duration` 统一为“注视持续时间 / 停留时间”。
- 正向/负向：不是统计回归系数，而是按论文中的使用角色编码。`正向` 表示该特征被用作支持预测、识别、分类或解释的有效信号；`负向` 表示该特征主要指向异常、风险、遮挡、中断、负类或高负荷线索；方向不稳定时标为 `混合/任务相关`。
- 来源：每篇论文的 `summary.txt` + 本地 PDF 关键词查漏。新加入的 20 篇优先围绕可由眼动仪得到、可作为 TCN 额外输入的特征编码。

## 频率表

| 排名 | 眼动特征 | 归一化/同义表达 | 出现频率 | 涉及论文 | 正向/负向特征 | 判定依据 |
|---:|---|---|---:|---|---|---|
| 1 | 注视点 / 凝视坐标 | gaze point, point-of-gaze, fixation point/location, gaze location | 20/50 | Fuhl-2021; Huang-2021; Jin-2024; Lin(GazeHTA)-2024; Liu(GEM)-2024; Mathew-2025; Ryan-2024; Seraj-2024; Shi-2024; Tonini-2023; Tonini-2024; Tu-2022; Wu-2023; Wang(MambaPupil)-2024; Krakowczyk(pymovements)-2023; Uribarri-2023; Koch-2022; Klotzl-2024; Chen(Gazealytics)-2023; Joseph-2021 | 正向为主 | 原始坐标仍是多数 gaze estimation、scanpath、可视分析和时序模型的基础，但在新加入文献中更多被当作派生速度、事件和 AOI 特征的输入。 |
| 2 | 注视持续时间 / 停留时间 | fixation duration, dwell time, AOI duration, gaze duration, FFD | 17/50 | Sabic-2020; Wang(hearing aids)-2017; Sandgren-2013; de Leon-Martinez-2023; Hakiminejad-2025; Friedman-2024; Nasri-2024; Joseph-2021; Cogan-2025; Shojaeizadeh-2022; Chen(Gazealytics)-2023; Shi-2024; Liu(GEM)-2024; Moroto-2023; Rong-2021; Wang(scanpath)-2021; Chavant-2022 | 混合/任务相关 | 停留时间可正向表示兴趣、注意或任务相关处理；在听噪声、高负荷、阅读障碍等场景中，过长注视常是负向/困难线索。 |
| 3 | AOI / ROI / 对象或面部区域 | AOI, ROI, object region, face/mouth/eyes region, partner/task region | 17/50 | Fang-2024; Jin-2024; Mathew-2025; Shi-2024; Song-2024; Tonini-2022; Tonini-2023; Wang(hearing aids)-2017; Sandgren-2013; Skoglund-2022; de Leon-Martinez-2023; Hakiminejad-2025; Chen(Gazealytics)-2023; Klotzl-2024; Koch-2022; Qu-2025; Sabic-2020 | 正向为主 | AOI 把连续 gaze-x/y 转换成任务语义区域；对听障任务特别有用，可形成口部、眼部、说话者、任务对象等输入通道。 |
| 4 | 眼跳 / 凝视转移 | saccade, gaze shift, transition, fixation transition, intertalker saccade | 16/50 | Chen(GazeXplain)-2024; Chen(Individualized)-2024; Fuhl-2021; Kerkouri-2021; Martin-2022; Wang(scanpath)-2021; Wang(hearing aids)-2017; Chavant-2022; Skoglund-2022; Krakowczyk(gaze events)-2023; Friedman-2024; Wang(MambaPupil)-2024; Qu-2025; Joseph-2021; Cogan-2025; Shojaeizadeh-2022 | 混合/任务相关 | 眼跳/转移是序列预测核心信号；但延迟、异常或过多眼跳可表示疲劳、障碍或高负荷。 |
| 5 | 扫视路径 / 凝视序列 | scanpath, visual scanpath, fixation sequence, gaze sequence | 14/50 | Abawi-2024; Chen(GazeXplain)-2024; Chen(Individualized)-2024; Fang-2024; Kerkouri-2021; Martin-2022; Wang(scanpath)-2021; Xue-2025; Krakowczyk(gaze events)-2023; Uribarri-2023; Koch-2022; Chen(Gazealytics)-2023; Klotzl-2024; Wang(MambaPupil)-2024 | 正向 | 对 TCN 最直接：保留时间顺序，可从原始 gaze 序列进一步编码事件、区域和窗口统计。 |
| 6 | 注视目标 / 被注视对象 | gaze target, gaze object, gazed object, attended object/speaker | 14/50 | Dai-2025; Jin-2024; Lin(GazeHTA)-2024; Mathew-2025; Ryan-2024; Seraj-2024; Song-2024; Toaiari-2024; Tonini-2022; Tonini-2023; Tonini-2024; Tu-2022; Skoglund-2022; Qu-2025 | 正向 | 作为目标检测或注意对象监督信号；在听障场景可扩展为 active speaker / attended speaker。 |
| 7 | 显著图 / 热力图 / 注意图 | saliency map, gaze heatmap, attention map, gaze map | 12/50 | Jin-2024; Lin(GazeHTA)-2024; Martin-2022; Mathew-2025; Moroto-2023; Rong-2021; Ryan-2024; Song-2024; Tonini-2022; Tonini-2023; Tonini-2024; Wang(scanpath)-2021 | 正向 | 多用于空间注意监督或输出表示；可作为模型标签或辅助输入，但对普通眼动仪特征工程不如 AOI/事件直接。 |
| 8 | 凝视方向 / 凝视角度 | gaze direction, gaze angle, pitch/yaw gaze angles, horizontal eye direction | 10/50 | Abdelrahman-2022; Dai-2025; Huang-2021; Mathew-2025; Ryan-2024; Toaiari-2024; Tonini-2022; Skoglund-2022; Chavant-2022; Qu-2025 | 正向 | 方向特征可由相邻坐标或眼动仪输出得到，适合补充 x/y 的运动方向信息。 |
| 9 | 眼跳幅度 / 速度 / 峰值速度 | saccade amplitude, saccade velocity, peak velocity, saccadic rate | 10/50 | Krakowczyk(gaze events)-2023; Krakowczyk(pymovements)-2023; Qu-2025; Joseph-2021; Shojaeizadeh-2022; Chavant-2022; Friedman-2024; Cogan-2025; Wang(MambaPupil)-2024; Fuhl-2021 | 混合/任务相关 | 对深度序列模型、负荷检测和异常检测有较强贡献；异常幅度/速度或不规则眼跳可作为负向线索。 |
| 10 | 瞳孔直径 / 瞳孔扩张 | pupil diameter, pupil dilation, pupil size, pupil variability | 9/50 | Fuhl-2021; Lin(FAPNet)-2024; Sen-2024; Nasri-2024; Joseph-2021; Shojaeizadeh-2022; Wang(MambaPupil)-2024; Ryan-2024; Abdelrahman-2022 | 混合/任务相关 | 可反映认知负荷、努力程度或眼动追踪几何；高负荷下常为负向/努力线索，但在建模中是有效输入。 |
| 11 | 眨眼 / 眼睑闭合 | blink, eyelid closure, blink duration/count | 7/50 | Fuhl-2021; Wang(MambaPupil)-2024; Shojaeizadeh-2022; Krakowczyk(pymovements)-2023; Nasri-2024; Lin(FAPNet)-2024; Sen-2024 | 混合/偏负向 | 眨眼可作为眼动事件和负荷特征，但也会造成遮挡/追踪中断，适合单独建通道或 mask。 |
| 12 | 凝视历史 / 时间上下文 | fixation history, previous fixation, temporal gaze context, time-windowed features | 7/50 | Abawi-2024; Chen(Individualized)-2024; Fang-2024; Martin-2022; Wang(MambaPupil)-2024; Uribarri-2023; Chen(Gazealytics)-2023 | 正向 | TCN 直接利用局部历史；新论文进一步支持将窗口化事件、统计量和上下文状态作为输入。 |
| 13 | 注视次数 / 注视频率 | fixation count, fixation frequency/rate, normalized fixation number | 7/50 | Hakiminejad-2025; Qu-2025; Joseph-2021; Shojaeizadeh-2022; Chen(Gazealytics)-2023; de Leon-Martinez-2023; Shi-2024 | 混合/任务相关 | 可表示注意分配、兴趣或负荷；次数过高/过低需按任务解释。 |
| 14 | 凝视熵 / 分散度 | gaze entropy, gaze dispersion, stationary gaze entropy, transition entropy, fixational dispersion | 6/50 | Hakiminejad-2025; Krakowczyk(gaze events)-2023; Krakowczyk(pymovements)-2023; Sabic-2020; Friedman-2024; Shi-2024 | 混合/任务相关 | 低分散可能表示集中注意，也可能表示高听觉努力；高熵可能表示探索或混乱，需结合任务标签。 |
| 15 | 面部/口部/说话者社会凝视线索 | mouth/eye/face AOI, gaze-to-partner, attended speaker, active talker | 6/50 | Sabic-2020; Wang(hearing aids)-2017; Sandgren-2013; Skoglund-2022; Chavant-2022; de Leon-Martinez-2023 | 正向为主 | 对听障研究最贴近：可直接编码为口部比例、眼部比例、看向说话者概率、说话者切换前后眼动。 |
| 16 | 反应潜伏期 / 时间到首次注视 | saccade latency, time to first fixation, reaction time | 5/50 | Chavant-2022; Friedman-2024; Hakiminejad-2025; Skoglund-2022; Qu-2025 | 混合/任务相关 | 潜伏期可表示注意反应速度；延迟常是疲劳、听觉困难或加工负荷增加的负向线索。 |
| 17 | 事件相机 / 高时间分辨率眼动信号 | event stream, event slicing, event point cloud, event-based eye signal | 4/50 | Lin(FAPNet)-2024; Sen-2024; Wang(MambaPupil)-2024; Fuhl-2021 | 正向 | 主要说明高时间分辨率事件信号能支持细粒度追踪；普通眼动仪可借鉴事件化思想而非硬件本身。 |
| 18 | 平滑追踪 / 微眼跳 | smooth pursuit, microsaccade, small eye movement | 4/50 | Wang(MambaPupil)-2024; Sabic-2020; Chavant-2022; Friedman-2024 | 混合/任务相关 | 可刻画连续目标跟随或听觉努力下微小眼动变化；普通眼动仪是否可靠取决于采样率。 |
| 19 | 个体化观察者 / 被试特征 | observer feature, subject embedding, personalized gaze pattern, interpersonal gaze pattern | 4/50 | Abawi-2024; Chen(Individualized)-2024; Moroto-2023; Xue-2025 | 正向 | 个体差异建模对听障人群尤其重要，可作为被试嵌入或个体基线特征。 |
| 20 | 瞳孔中心 / 瞳孔位置 / 分割 | pupil center, pupil position/location, pupil segmentation | 4/50 | Fuhl-2021; Lin(FAPNet)-2024; Sen-2024; Wang(MambaPupil)-2024 | 正向 | 更偏追踪底层几何，但可用于数据质量控制和事件相机/低延迟任务。 |
| 21 | 聚散 / 双眼协同 | vergence, convergence, binocular coordination | 2/50 | Chavant-2022; Skoglund-2022 | 混合/任务相关 | 与多感官整合和视听目标反应相关；若眼动仪提供双眼数据，可作为听障辅助研究的补充特征。 |
| 22 | 信号质量 / 校准误差 | calibration error, signal quality, spatial/temporal precision | 2/50 | Skoglund-2022; Toaiari-2024 | 混合/偏负向 | 更像质量控制特征；高误差通常是负向噪声，但对模型可作为置信度输入。 |
| 23 | 聚类有效性 / 异常模式指标 | cluster validity, gaze pattern clustering, dyslexia/ASD difference | 2/50 | Shi-2024; Cogan-2025 | 负向/异常线索 | 用于识别 ASD、阅读障碍等异常眼动模式，可启发听障人群差异检测。 |

## 简要结论

- 对你的 TCN 输入最直接的新增特征是：`fixation duration/count/rate（注视持续时间/注视次数/注视频率）`、`saccade amplitude/velocity/latency/rate（眼跳幅度/眼跳速度/眼跳潜伏期/眼跳频率）`、`AOI dwell time（兴趣区停留时间）`、`gaze transition entropy（凝视转移熵）`、`pupil dilation（瞳孔扩张）`、`blink count/duration（眨眼次数/眨眼持续时间）`、`time-windowed event labels（时间窗口化事件标签）`。
- 听障相关论文提示应重点加入社会交流特征：看向说话者/交流伙伴概率、口部/眼部/上脸/下脸 AOI 比例、说话者切换或视听目标后的眼跳潜伏期。
- 正负方向不能脱离任务解释：长注视既可能表示兴趣/处理，也可能表示听觉噪声下努力增加；低 gaze dispersion 既可能表示注意集中，也可能表示努力听辨导致的视觉搜索减少。
- 实作建议：保留 `gaze-x/gaze-y` 作为基础通道，同时在每个时间窗加入速度、加速度、事件标签、AOI one-hot/比例、瞳孔/眨眼、熵和潜伏期类特征，再用消融实验验证有效性。
