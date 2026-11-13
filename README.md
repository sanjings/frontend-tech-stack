# 大前端技术选型策略（2026–2027）

> 原则：评估当前时间线各形态下**主流且合适**的方案；按 **Vue 线 / React 线** 分列。  
> 范围：应用与网站主航道。不含穿戴、车机IVI、小游戏、XR、浏览器扩展等（见文末）。手机 App 的鸿蒙 Next 在主表内。

## 总览对照

| 产品形态 | Vue 线 | React 线 |
|----------|--------|----------|
| App 为主，小程序 / H5 为辅 | **uni-app x**（蒸汽模式）+ 官方 / 内置组件 | **优先 Expo / RN**；要鸿蒙 → **Taro Harmony**；必须与小程序强复用 → **Taro → RN** |
| 小程序 / H5 为主，App 为辅 | **传统 uni-app** + **wot-ui** | **Taro（React）** → 小程序 + H5 + RN App |
| 纯移动 H5 | **Vue 3** + **Vant** | **React** + **Ant Design Mobile** |
| 数据可视化大屏 | **Vue 3** + **ECharts** + DataV 类装饰 | **React** + **ECharts** + DataV-React |
| B 端后台 / 中台 Web | **Vue 3** + **Element Plus** | **React** + **Ant Design**（脚手架可选 Pro / Umi） |
| PC 营销 / 内容站（SEO/SSR） | **Nuxt 4** | **Next.js** |
| 桌面跨端客户端 | **Electron** + Vue 3（轻量 / 安全敏感评 Tauri 2 桌面端） | **Electron** + React（轻量 / 安全敏感评 Tauri 2 桌面端） |

## Vue 线

| # | 产品形态 | 技术选型 | 说明 |
|---|----------|----------|------|
| 1 | App 为主，小程序 / H5 为辅 | uni-app x 蒸汽模式 + 官方 / 内置 UI | 鸿蒙 Next 自 4.61 起。小程序目前仅微信 / 支付宝，抖音未完成。wot-ui 的 uni-app x 仍在筹备 |
| 2 | 小程序 / H5 为主，App 为辅 | 传统 uni-app + wot-ui | 覆盖抖音、钉钉等。App 的 vue 页面是 webview。官方将于 2027 年初停止该 App 平台维护 |
| 3 | 纯移动 H5 | Vue 3 + Vant 4 | 仅 H5 时直用 Vue，无需跨端框架进行抽象。Vant 4 是 mobile web 组件库 |
| 4 | 数据可视化大屏 | Vue 3 + ECharts + DataV 装饰层 | 无特别主流的「大屏业务 UI 库」，多以自研为主；图表默认 ECharts |
| 5 | B 端后台 | Vue 3 + Element Plus | Element Plus 是 Vue 3 组件库。跟着团队已有的 Vue 栈 |
| 6 | PC 官网 / 内容站 | Nuxt 4 | 默认 SSR |
| 7 | 桌面客户端 | Electron + Vue 3 | Electron 内嵌 Chromium 与 Node，桌面三平台。包体积 / 安全敏感再评 Tauri 2 桌面端 |

## React 线

| # | 产品形态 | 技术选型 | 说明 |
|---|----------|----------|------|
| 1 | App 为主，小程序 / H5 为辅 | 优先 Expo / RN；要鸿蒙则 Taro Harmony；强复用则 Taro → RN | RN 官方入门推荐 Expo，平台为 Android、iOS、Web（RN 另有 TV）。鸿蒙不在该列表 |
| 2 | 小程序 / H5 为主，App 为辅 | **Taro（React）** 一体打包小程序 + H5 + RN | Taro 也支持 Vue，本列固定 React。组件和 API 以微信小程序规范为基准。鸿蒙另编，不走 RN |
| 3 | 纯移动 H5 | React + Ant Design Mobile | 与 PC 版 Ant Design 是两套库 |
| 4 | 数据可视化大屏 | React + ECharts + DataV-React | 与 Vue 线同构，换框架即可 |
| 5 | B 端后台 | React + Ant Design（脚手架可选 Pro / Umi） | Ant Design 官方推荐 Umi；Pro 是脚手架选项 |
| 6 | PC 官网/内容站 | Next.js | 全栈 React，App Router 与 Pages Router |
| 7 | 桌面客户端 | Electron + React | 壳层与 Vue 线一致，UI 框架跟随团队 |

## 选型决策（按主端）

| 主端判断 | 优先选型 |
|----------|----------|
| 要强 App，团队 Vue，小程序只要微信 / 支付宝（可含鸿蒙） | Vue #1（uni-app x 蒸汽模式） |
| 要强 App，团队 Vue，还要抖音等其他小程序 | App 用 #1，小程序用 #2，不放进同一个项目 |
| 小程序 / H5 为主，App 只配套，且能接受 2027 年初前的 uni-app App 平台 | Vue #2（传统 uni-app + wot） |
| 要强小程序，团队 React，App 配套 | React #2（Taro React，含 RN） |
| 要强 App，团队 React，不要鸿蒙，小程序不是硬约束 | React #1（Expo / RN） |
| 要强 App，团队 React，要鸿蒙 | Taro Harmony（4.1+，仅 Vite） |
| 要强 App，团队 React，且必须与小程序共用业务代码 | Taro → RN（微信小程序规范；RN 样式只支持类选择器） |
| 只要移动 H5 | Vue #3 或 React #3 |
| 数据看板 / 指挥中心大屏 | Vue/React #4（ECharts；地理 L7，关系 G6） |
| 只要 B 端后台 | 跟着团队：Vue #5 或 React #5 |
| 只要 PC 站 | Vue #6（Nuxt 4）或 React #6（Next.js） |
| 桌面工具/客户端 | 两线均为 Electron（#7）；轻量 / 安全敏感评 Tauri 2 桌面端 |

## 数据可视化大屏补充

数据大屏 **没有** 类似 Vant / Ant Design 的单一主流业务 UI 库，常见拼装为：

| 层级 | 作用 | 主流选择 |
|------|------|----------|
| 框架 | 页面与状态 | Vue 3 / React |
| 图表 | 柱线饼雷达地图等 | **Apache ECharts（默认首选）**。AntV G2 是另一套图表语法 |
| 地理 | 大规模地理空间 | **AntV L7** |
| 关系 | 关系图 | **AntV G6** |
| 装饰控件 | 边框、翻牌器、轮播表、科技风装饰 | DataV 系开源组件或自研 |
| 图标资产 | 状态/装饰 SVG | iconfont / IconPark / 设计出海量 SVG（少用 Ant/Vant 图标风格） |
| 低代码交付 | 非研发主栈 | 可评估阿里云 DataV |

## 移动多端对照（Vue ↔ React）

| 优先级 | Vue 线 | React 线 |
|--------|--------|----------|
| 小程序/H5 为主 | 传统 uni-app + wot | **Taro（React）**（小程序 + H5 + RN App） |
| App 为主 | uni-app x 蒸汽模式 | Expo/RN；要鸿蒙则 Taro Harmony |
| App + 鸿蒙 Next | uni-app x（4.61+） | Taro Harmony（4.1+，仅 Vite） |

说明：

- Taro 的组件和 API 以**微信小程序规范**为基准。RN 端样式只支持类选择器，不支持组合器、伪类和 border 简写。鸿蒙是 Harmony C-API，不是这条 RN 编译。
- uni-app x 与传统 uni-app 是两种项目。蒸汽模式组件在不使用 uts 特有语法、且不使用 ucss 不支持的 CSS 时可以两边共用；VDOM 下 uvue 不能直接引 js/ts，vue 也不能直接引 uts。原生组件插件不能在老 uni-app 和 uni-app x 蒸汽模式之间复用。
- wot-ui 官方平台含微信、支付宝、钉钉、H5、APP。uni-app x 兼容仍在筹备，不配到 #1。

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

1. 多小程序仍走传统 uni-app。App 要过 2027 年初，用 uni-app x 蒸汽模式，小程序只保留微信和支付宝。  
2. React 线：小程序为主用 Taro（React）；强 App 且不要鸿蒙用 Expo；要鸿蒙用 Taro Harmony。B 端用 Ant Design，PC 用 Next.js。  
3. 桌面默认 **Electron**。Tauri 2 只评估桌面端；它官方还覆盖 Android / iOS，本策略不使用。  
