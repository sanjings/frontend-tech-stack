# 大前端技术选型策略（2026–2027）

> 原则：评估当前时间线各形态下**主流且合适**的方案；按 **Vue 线 / React 线** 分列。  
> 范围：应用与网站主航道。不含穿戴、车机IVI、小游戏、XR、浏览器扩展等（见文末）。

## 总览对照

| 产品形态 | Vue 线 | React 线 |
|----------|--------|----------|
| App 为主，小程序 / H5 为辅 | **uni-app x** + 官方 / 内置组件 | **优先 Expo / React Native**；若必须与小程序强复用 → **Taro → RN** |
| 小程序 / H5 为主，App 为辅 | **传统 uni-app** + **wot-ui** | **Taro（React）** → 小程序 + H5 + RN App |
| 纯移动 H5 | **Vue 3** + **Vant** | **React** + **Ant Design Mobile** |
| 数据可视化大屏 | **Vue 3** + **ECharts** + DataV 类装饰 | **React** + **ECharts** + DataV-React |
| B 端后台 / 中台 Web | **Vue 3** + **Element Plus** | **React** + **Ant Design Pro** |
| PC 营销 / 内容站（SEO/SSR） | **Nuxt** | **Next.js** |
| 桌面跨端客户端 | **Electron** + Vue 3（轻量工具可评估 Tauri） | **Electron** + React（轻量工具可评估 Tauri） |

## Vue 线

| # | 产品形态 | 技术选型 | 说明 |
|---|----------|----------|------|
| 1 | App 为主，小程序 / H5 为辅 | uni-app x + 官方 / 内置 UI | App 性能优先；小程序目前仅支持微信小程序 / 支付宝小程序|
| 2 | 小程序 / H5 为主，App 为辅 | 传统 uni-app + wot-ui | App性能有上限；国内 ToC 默认最优解之一|
| 3 | 纯移动 H5 | Vue 3 + Vant | 仅 H5 时直用 Vue，无需跨端框架进行抽象 |
| 4 | 数据可视化大屏 | Vue 3 + ECharts + DataV 装饰层 | 无特别主流的「大屏业务 UI 库」，多以自研为主；图表默认 ECharts |
| 5 | B 端后台 | Vue 3 + Element Plus 等 | 团队全 Vue 时比 React 后台更省人效 |
| 6 | PC 官网 / 内容站 | Nuxt | SSR / SEO 全栈 |
| 7 | 桌面客户端 | Electron + Vue 3 | 默认 Electron；包体积 / 安全敏感再评 Tauri |

## React 线

| # | 产品形态 | 技术选型 | 说明 |
|---|----------|----------|------|
| 1 | App 为主，小程序 / H5 为辅 | 优先 Expo / RN；强复用则 Taro | Taro App 端是「小程序语义 → RN」，不是完整 RN 生态 |
| 2 | 小程序 / H5 为主，App 为辅 | **Taro（React）** 一体打包小程序 + H5 + RN | React 团队做国内 ToC 多端的默认方案 |
| 3 | 纯移动 H5 | React + Ant Design Mobile | 勿与 PC 版 Ant Design 混用 |
| 4 | 数据可视化大屏 | React + ECharts + DataV-React | 与 Vue 线同构，换框架即可 |
| 5 | B 端后台 | React + Ant Design（Pro/Umi） | 国内 B 端生态最稳之一 |
| 6 | PC 官网/内容站 | Next.js | SSR / SEO 营销站、内容站 |
| 7 | 桌面客户端 | Electron + React | 壳层与 Vue 线一致，UI 框架跟随团队 |

## 选型决策（按主端）

| 主端判断 | 优先选型 |
|----------|----------|
| 要强 App，团队 Vue，且要带小程序 | Vue #1（uni-app x） |
| 要强小程序/H5，App 配套，团队 Vue | Vue #2（传统 uni-app + wot） |
| 要强小程序，团队 React，App 配套 | React #2（Taro 一体，含 RN） |
| 要强 App，团队 React，小程序不是硬约束 | React #1（Expo/RN） |
| 要强 App，团队 React，且必须与小程序共用业务代码 | Taro 一套（接受 RN 端样式/组件子集约束） |
| 只要移动 H5 | Vue #3 或 React #3 |
| 数据看板 / 指挥中心大屏 | Vue/React #4（ECharts 为主） |
| 只要 B 端后台 | Vue #5 或 React #5（国内默认常选 React #5） |
| 只要 PC SEO 站 | Vue #6（Nuxt）或 React #6（Next） |
| 桌面工具/客户端 | 两线均为 Electron（#7） |

## 数据可视化大屏补充

数据大屏 **没有** 类似 Vant / Ant Design 的单一主流业务 UI 库，常见拼装为：

| 层级 | 作用 | 主流选择 |
|------|------|----------|
| 框架 | 页面与状态 | Vue 3 / React |
| 图表 | 柱线饼雷达地图等 | **Apache ECharts（默认首选）**；复杂地理/关系可补 AntV（G2/L7/G6） |
| 装饰控件 | 边框、翻牌器、轮播表、科技风装饰 | DataV 系开源组件或自研 |
| 图标资产 | 状态/装饰 SVG | iconfont / IconPark / 设计出海量 SVG（少用 Ant/Vant 图标风格） |
| 低代码交付 | 非研发主栈 | 可评估阿里云 DataV |

## 移动多端对照（Vue ↔ React）

| 优先级 | Vue 线 | React 线 |
|--------|--------|----------|
| 小程序/H5 为主 | 传统 uni-app + wot | **Taro**（小程序 + H5 + RN App） |
| App 为主 | uni-app x | Expo/RN（或 Taro，非性能最优叙事） |

说明：

- Taro App 底层走 **React Native**，但 API / 组件以小程序为基准映射到 RN，样式与三方库是子集。  
- uni-app x 与传统 uni-app **不可页面混写**。

## 范围外（不进默认选型）

| 形态 | 常见方向（仅认知） |
|------|-------------------|
| 穿戴 | SwiftUI / Wear Compose / 各厂鸿蒙原生 |
| 车机娱乐域 | Android Automotive / Qt / Flutter |
| 小游戏 | 微信小游戏 / Cocos / Unity |
| XR | WebXR / Unity 等 |
| 浏览器扩展 | Manifest V3 + 扩展工程 |

## 文档索引

> 中文列：优先官方中文；无官方时用社区镜像（标注「社区」）。英文列：官方英文；国内向产品若无独立英文站则标「—」。

| 技术 | 中文文档 | 英文文档 |
|------|----------|----------|
| Vue 3 | [cn.vuejs.org](https://cn.vuejs.org/) | [vuejs.org](https://vuejs.org/) |
| React | [zh-hans.react.dev](https://zh-hans.react.dev/) | [react.dev](https://react.dev/) |
| uni-app | [uniapp.dcloud.net.cn](https://uniapp.dcloud.net.cn/) | [en.uniapp.dcloud.io](https://en.uniapp.dcloud.io/) |
| uni-app x | [doc.dcloud.net.cn/uni-app-x](https://doc.dcloud.net.cn/uni-app-x/) | — |
| Wot UI | [wot-ui.cn](https://wot-ui.cn/) | [wot-ui.cn（EN）](https://wot-ui.cn/) |
| Vant | [vant 中文](https://vant-ui.github.io/vant/#/zh-CN) | [vant EN](https://vant-ui.github.io/vant/#/en-US) |
| Element Plus | [element-plus.org/zh-CN](https://element-plus.org/zh-CN/) | [element-plus.org/en-US](https://element-plus.org/en-US/) |
| Nuxt | [nuxt.com.cn](https://www.nuxt.com.cn/docs)（社区） | [nuxt.com/docs](https://nuxt.com/docs) |
| Taro | [docs.taro.zone](https://docs.taro.zone/docs/) | [docs.taro.zone（EN）](https://docs.taro.zone/en/docs/) |
| Expo | [expo.nodejs.cn](https://expo.nodejs.cn/)（社区） | [docs.expo.dev](https://docs.expo.dev/) |
| React Native | [reactnative.cn](https://reactnative.cn/)（社区） | [reactnative.dev](https://reactnative.dev/) |
| Ant Design | [ant.design 中文](https://ant.design/index-cn) | [ant.design](https://ant.design/) |
| Ant Design Mobile | [mobile.ant.design/zh](https://mobile.ant.design/zh) | [mobile.ant.design](https://mobile.ant.design/) |
| Ant Design Pro | [pro.ant.design/zh-CN](https://pro.ant.design/zh-CN) | [pro.ant.design](https://pro.ant.design/) |
| Umi | [umijs.org](https://umijs.org/) | [umijs.org/en-US](https://umijs.org/en-US) |
| Next.js | [nextjscn.org](https://nextjscn.org/)（社区） | [nextjs.org/docs](https://nextjs.org/docs) |
| Apache ECharts | [echarts 中文](https://echarts.apache.org/zh/index.html) | [echarts EN](https://echarts.apache.org/en/index.html) |
| AntV（G2/L7/G6） | [antv.antgroup.com](https://antv.antgroup.com/) | [antv.antgroup.com/en](https://antv.antgroup.com/en) |
| DataV（开源装饰） | [datav.jiaminghi.com](https://datav.jiaminghi.com/) | — |
| DataV-React | [datav-react.jiaminghi.com](http://datav-react.jiaminghi.com/) | — |
| 阿里云 DataV | [阿里云帮助中心](https://help.aliyun.com/product/27051.html) | — |
| Electron | [electronjs.org/zh](https://www.electronjs.org/zh/docs/latest/) | [electronjs.org/docs](https://www.electronjs.org/docs/latest/) |
| Tauri | [tauri.app/zh-cn](https://tauri.app/zh-cn/) | [tauri.app](https://tauri.app/) |
| iconfont | [iconfont.cn](https://www.iconfont.cn/) | — |
| IconPark | [iconpark.oceanengine.com](https://iconpark.oceanengine.com/) | [IconPark EN](https://iconpark.oceanengine.com/official) |

## 备注

1. **Vue 线**更适合「国内 ToC 多端（App + 小程序）」一条龙。  
2. **React 线**在「小程序为主」时用 **Taro 一体**；在「B 端 + PC 站 + 强 App」时用 Ant Design + Next + Expo 更顺。  
3. 桌面默认 **Electron**；Tauri 2 作为轻量 / 安全敏感场景的备选。  

