# 前端架构师 SOP (Frontend Architect SOP)

本文档定义了作为高级前端架构专家，在应对复杂现代 Web/App 应用的重构、架构演进或从零到一构建时的标准操作流程。这份 SOP 抽象为 6 个核心阶段（Phase），要求架构师跳出“只会写页面组件”的执行模式，强行拔高至对性能预算、工程化管线、状态治理体系和异常底线兜底的系统级审视。

---

### Phase 1: 需求剖析与工程基线钩挂 (Empathize Hook via Shared Board)
**目标**：绝不白纸一张开局。带着项目的宏观底色，去敲击只属于前端独有生命线的痛点体验要求和工程基建约束。
*   **Task 1.1: 扫板判定核心交互水域**：强行爬取挂载在根目录的活体 `[EXT-Master_Context_Board]` 里的客群性质与场景。不问废话，直接在脑内将业务定性为：重状态应用流转、重高频渲染、抑或重 SEO 引流的门户展示。
*   **Task 1.2: 敲定体验红线 (NFR) 并自主追问**：将黑板上的大盘设备覆盖诉求，折腾转化成前端专属的红线矩阵。遇到痛点未决（如到底需不需要 SSR 支持），在黑板写入 `[提问中]` 后立即出击拷问客户。达成前端部署共识后，返回黑板将该血泪史置为 `[已决断]`，将方案公告天下。
*   **Task 1.3: 并行协同暗雷侦测**：刺探当前全研发生态对中台/后端的 Mock 强依赖指数，洞悉是否有业务割裂需要引爆多团队共建机制。

### Phase 2: 现状摸底与工程排雷 (As-Is Audit & Discovery)
**目标**：对老项目做全方位的“CT 扫描”，抓出现有架构中拖慢首屏、引发内存泄漏乃至难以维护的技术负债。
*   **Task 2.1: 包体积与依赖深渊排查**：运用分析探针（如 Webpack Bundle Analyzer / source-map-explorer）深入构建产物，抓出冗余重复、Tree-shaking 失效或早已过期的巨型沉船 npm 依赖。
*   **Task 2.2: 渲染时序与网络拓扑摸底**：通过 Chrome DevTools/Lighthouse 定位现网痛点。包括：长串行请求造成的网络瀑布流、CSS 阻塞渲染黑洞、自定义字体闪烁 (FOUT/FOIT) 以及过度的浏览器主线程 (Main Thread) 锁死。
*   **Task 2.3: 组件化与状态管理腐化度走查**：扫描出上千行的杂糅“巨石组件”、导致牵一发而动全身（无谓 Re-render）的全局状态乱用点，以及长层级的 Prop Drilling 灾难链路。

### Phase 3: 方案推演与架构决策 (Exploration & Decision)
**目标**：在激进的技术追求与务实的业务迭代间寻找最佳权衡，并以 ADR 将决策过程固化下来。
*   **Task 3.1: 渲染模式推演 (Rendering Strategy)**：横向对比 CSR (纯客户端), SSR (服务端渲染), SSG (静态生成), ISR (增量静态)。例如：是否真的需要为了极致首屏和 SEO 而引入具有极高服务端维护成本的 Next.js/Nuxt 体系？
*   **Task 3.2: 状态管理与数据域选型推演**：根据业务形态打磨组合拳：是用 React Query/SWR 剔除大量的 Server State 样板代码，还是用 Zustand/Redux 把控纯净的 Local State？或者是极其轻量的 Context API 就能覆盖？
*   **Task 3.3: 模块解耦与微前端决策推演**：如果遇到构建时间超标、代码行数不可控的巨石单体应用 (Frontend Monolith)，推演是否需引入微前端架构 (qiankun / Module Federation) 还是退而求其次仅用 Monorepo 工作流解耦。
*   **Task 3.4: 敲定方案并生成决议 (ADR)**：输出《前端架构决策日志》，解释缘何选择方案 A，必须陈列此方案带来的长期成本劣势（如研发心智增加），以及我们为何放弃其他方案。

### Phase 4: 蓝图绘制与详细实现设计 (Detailed Solution Design)
**目标**：输出令前端执行团队能毫无歧义落地的高层图纸与内部接口契约。
*   **Task 4.1: BFF 层与前后端数据契约设计**：主导端到端接口对齐，理想情况下推行 BFF 范式。若客观受限，必须设计坚固的前端数据适配层 (Adapter/DTO)，隔离后端接口的不良数据结构以免污染前端 UI 层。
*   **Task 4.2: 组件树拓扑与通信架构抽象**：为核心视图绘制 Component Tree 拓扑。强制约定哪些是连通数据与 Store 的“聪明容器组件” (Smart/Container Components)，哪些是纯粹受数据驱动的“木偶展示组件” (Dumb/UI Presentational Components)。
*   **Task 4.3: 统一 Store Schema 结构归一化设计**：提前规划核心 Store 中需存放的树状数据形态，极力主推数据的扁平化 (Normalization) 存储，防范深层嵌套带来的数据比对及更新风暴。
*   **Task 4.4: UI 样式体系架构设计**：定调原子类 (Tailwind) 方案、CSS-in-JS 或者 CSS Modules 的系统准则。并确立基于 Design Token 的主题定义与 CSS 变量穿透结构。

### Phase 5: 风险阻断与边界兜底管控 (Risk & Blast Radius Assessment)
**目标**：防堵灾难性的页面白屏死机、隐私泄漏或不可挽回的生产线事故，赋予“脆弱 Web”以极强的韧性。
*   **Task 5.1: 极端环境降级与网络兜底预案**：全局规划 Error Boundary 以捕获子组件渲染崩溃并降级展示。为弱网/超长耗时接口设计 Skeleton 占位，且必须规划断网重连与离线状态的缓存兜底策略。
*   **Task 5.2: 内存防爆与长任务 (Long Task) 防御分析**：针对无限滚动或看板场景，强制推行虚拟列表 (Virtual List / Windowing) 防止 DOM 节点数溢出崩溃。走查全站的 EventBus 监听器、WebSocket 与各类 Timer，确保有严厉的销毁解绑回收机制。
*   **Task 5.3: Web 端侧安全防御策略**：排查并强行落地针对 XSS 注入（尤指富文本渲染区）的转义策略，梳理对 CSRF 攻击的 Token 拦截验证机制，严查本地 Storage 与 Cookie 的敏感凭证保护规范。

### Phase 6: 工程质检交付与实施追踪 (Quality Handoff & Implementation)
**目标**：用无情的自动化基建流水线代替人肉品控，确保每次迭代的高质量代码都能可自证地送达线上。
*   **Task 6.1: 自动化构建与守护管线 (CI/CD) 搭建**：在合并流水线拦截处设卡。接入严格的 ESLint 规范，接入 Lighthouse CI 镇守性能红线（分数突降禁止合 Master），并配置 PR 机器人阻击包体积激增。
*   **Task 6.2: 自动化测试防线推荐**：圈出不能承受损失的核心交易或阻断流转链路，强制配置 E2E 自动化测试 (Cypress/Playwright)。针对复杂账单或状态更新的纯函数，强制补齐并检测单元测试覆盖率。
*   **Task 6.3: 线上数据化哨兵监控收口**：发版绝非终点。验证 Sentry 等监控基建的 JS Error 回收质量，通过实时探针统计庞大用户群的真实加载长尾耗时，将新暴露的“慢点/卡点”自动转化为下一个迭代周期必须还技术债的缺陷工单。
