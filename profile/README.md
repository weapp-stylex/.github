<p align="center">
  <a href="https://stylex.weapp.dev/">
    <img src="https://raw.githubusercontent.com/weapp-stylex/weapp-stylex/main/assets/brand/logo.svg" width="128" height="128" alt="weapp-stylex logo" />
  </a>
</p>

<h1 align="center">weapp-stylex</h1>

<p align="center">
  <strong>StyleX for WeChat mini-programs · 让 StyleX 走进微信小程序</strong>
</p>

<p align="center">
  <a href="https://stylex.weapp.dev/zh/">中文文档</a> ·
  <a href="https://stylex.weapp.dev/en/">English Docs</a> ·
  <a href="https://github.com/weapp-stylex/weapp-stylex">源码 / Source</a> ·
  <a href="https://www.npmjs.com/package/weapp-stylex">npm</a> ·
  <a href="https://github.com/weapp-stylex/weapp-stylex/issues">反馈 / Issues</a>
</p>

## 用 TypeScript 写样式，在微信小程序中复用

weapp-stylex 基于官方 StyleX runtime 与编译器，把 JavaScript / TypeScript 中的样式编译为微信小程序 WXSS。保留 `create()`、`attrs()`、`props()` 和主题 API，让同一份样式在不同页面、组件和普通分包中复用。

- **共享样式**：在普通 `styles.ts` 中定义，通过具名导出、默认导出、barrel、路径别名或 workspace 源码模块复用。
- **条件与动态样式**：使用官方 runtime 合并样式、覆盖属性和传入动态值；通过 `defineVars()` / `createTheme()` 管理主题。
- **微信产物**：构建时生成并去重原子 WXSS，自动处理页面、组件的样式入口与导入。
- **单位清晰**：数值 `16` 保持 `16px`；需要小程序响应式单位时显式写 `'16rpx'`。

### 选择你的框架

| 框架 / Framework | 接入方式 / Integration | 示例 / Example |
| --- | --- | --- |
| 原生微信 / Native WeChat | weapp-vite + `stylexCompiler()` | [wechat-native](https://github.com/weapp-stylex/weapp-stylex/tree/main/examples/wechat-native) |
| Wevu | weapp-vite + `createStylex()`，支持 Vue SFC / JSX | [wechat-wevu](https://github.com/weapp-stylex/weapp-stylex/tree/main/examples/wechat-wevu) |
| Taro React | Taro 插件，Vite / Webpack 5 | [taro-react](https://github.com/weapp-stylex/weapp-stylex/tree/main/examples/taro-react) |
| Taro Vue 3 | Taro 插件，Vite / Webpack 5 | [taro-vue3](https://github.com/weapp-stylex/weapp-stylex/tree/main/examples/taro-vue3) |
| uni-app Vue 3 | `stylexUniApp()`，mp-weixin | [uni-vue3](https://github.com/weapp-stylex/weapp-stylex/tree/main/examples/uni-vue3) |

### 开始使用

```bash
pnpm add weapp-stylex
```

根入口提供 StyleX runtime；构建适配器从对应子路径接入：

```ts
import * as stylex from 'weapp-stylex'
import { stylexCompiler } from 'weapp-stylex/weapp-vite'
// Wevu: createStylex from 'weapp-stylex/weapp-vite'
// Taro: require.resolve('weapp-stylex/taro')
// uni-app: stylexUniApp from 'weapp-stylex/uni-app'
```

按框架完成构建配置后，就可以定义共享样式：

```ts
// styles.ts
import * as stylex from 'weapp-stylex'

export const styles = stylex.create({
  root: {
    padding: 16,
    borderRadius: '12rpx',
    backgroundColor: 'white',
  },
  active: { opacity: 0.6 },
})
```

原生 WXML 把 `attrs()` 结果绑定到 data；Wevu / Vue 使用 `computed` 与显式 `:class`、`:style`；Taro React 在 `View` 上使用 `props()`。

完整步骤见[中文文档](https://stylex.weapp.dev/zh/)。也可按需安装 [`@weapp-stylex/*` 拆分包](https://github.com/weapp-stylex/weapp-stylex#包与接入方式)。

## Write styles in TypeScript. Share them across your mini-program.

weapp-stylex compiles JavaScript / TypeScript styles to WeChat WXSS using the official StyleX runtime and compiler. Keep the familiar `create()`, `attrs()`, `props()` and theme APIs while sharing styles across pages, components and regular subpackages.

- Export styles from ordinary modules, including named/default exports, barrels, aliases and workspace source packages.
- Compose conditional styles, dynamic values and themes with the official runtime.
- Generate deduplicated atomic WXSS and connect it to page and component style entries at build time.
- Preserve StyleX units: numeric `16` means `16px`; use `'16rpx'` explicitly when needed.

Install `weapp-stylex`, then choose an adapter from the framework table above. The root entry exposes runtime APIs; explicit subpaths expose build integrations. For native WXML, bind `attrs()` through data. For Wevu / Vue, use `computed` with `:class` and `:style`. For Taro React, spread `props()` onto `View`.

Read the [English documentation](https://stylex.weapp.dev/en/) for framework setup, shared styles and themes.

## 项目与参与 / Projects & contributing

| 入口 / Link | 内容 / What you will find |
| --- | --- |
| [weapp-stylex](https://github.com/weapp-stylex/weapp-stylex) | 核心、编译器、适配器与示例 / Runtime, compiler, adapters and examples |
| [stylex.weapp.dev](https://stylex.weapp.dev/) | 中英文文档 / Chinese and English documentation |
| [Issues](https://github.com/weapp-stylex/weapp-stylex/issues) | 问题反馈与功能建议 / Bug reports and feature requests |
| [Pull requests](https://github.com/weapp-stylex/weapp-stylex/pulls) | 代码、文档与示例贡献 / Code, documentation and example contributions |

当前支持微信主包、页面、组件和普通分包。其他平台、独立分包、Vue 2、uni-app x 与 stateful HMR 尚未纳入支持范围。

Current scope: WeChat main packages, pages, components and regular subpackages. Other platforms, independent subpackages, Vue 2, uni-app x and stateful HMR are outside the current support scope.

[MIT License](https://github.com/weapp-stylex/weapp-stylex/blob/main/LICENSE) · Built on [StyleX](https://stylexjs.com/).
