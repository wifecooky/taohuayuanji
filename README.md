# 桃源 · 豁然开朗

沿溪、舍舟、入山，在一片真正连续的三维田园中，走进陶渊明的《桃花源记》。

全文二十幕，可跟着朗诵一路游历；也可以只在五境之间自由走看。四季、天时、天气都按真实时间渲染，也可以手动切换。

## 线上地址

| | |
|---|---|
| 正式站 | <https://taohuayuanji.thewang.net/> |
| GitHub Pages 镜像 | <https://wifecooky.github.io/taohuayuanji/> |

两处都跟随 `main` 分支：

- 正式站由 **Cloudflare Pages** 的 git 集成托管，push 到 `main` 即自动构建上线。**配置在 Cloudflare 那一侧，仓库里没有对应文件**——别因为找不到 workflow 就以为没有部署。
- 镜像是 GitHub Pages，直接发 `main` 的根目录（legacy build，无构建步骤）。

## 本地运行

站点会 `fetch` `models/` 下的 glb，所以不能用 `file://` 直接打开，必须起一个静态服务器：

```sh
python3 -m http.server 8765 --bind 127.0.0.1
# 然后打开 http://127.0.0.1:8765/index.html
```

没有依赖、没有构建、没有 `npm install`。

## URL 参数

| 参数 | 取值 | 缺省 |
|---|---|---|
| `season` | `spring` `summer` `autumn` `winter` | 按当前真实季节 |
| `hour` | `0`–`24` 的小数，如 `17.5` | 按当前真实时刻 |
| `sky` | `clear` `fog` `rain` `snow`（`snow` 只在落雪的季节生效，否则退回 `clear`） | `clear` |
| `shot` | `0`–`4`，对应缘溪行 / 桃林尽处 / 豁然开朗 / 阡陌人家 / 桑竹远山 | `2` |

例：`?season=winter&hour=6.5&sky=snow&shot=1`

## 目录

```
index.html   整个站点——HTML、CSS、three.js r140、全部场景代码
vendor/      GLTFLoader.js、ez-tree.umd.js
models/      33 个 glb 植被与道具
audio/       溪水、林间鸟鸣、全文朗诵
```

## 第三方

- [three.js](https://threejs.org/) r140（MIT）——压缩后内联在 `index.html` 里；`GLTFLoader` 单独放在 `vendor/`
- [ez-tree](https://github.com/dgreenheck/ez-tree) — MIT，© 2024 Daniel Greenheck，见 `vendor/ez-tree.LICENSE`
- [Kenney Nature Kit](https://kenney.nl/assets/nature-kit) — CC0。glb 在运行时被重新着色成本页配色的平面着色几何体；文件缺失时道具会退化成体素占位，不会崩。
