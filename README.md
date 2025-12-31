# fusite3

[hfu/fusite2](https://github.com/hfu/fusite2) の fusion 版。標高タイル可視化サイトです。

## 概要

`fusite3` は `fusite2` を極めて忠実に踏襲した GitHub Pages サイトですが、次の１点のみが異なります：

**Terrarium tiles のソースを唯一 [https://tiles.mapterhorn.com/tilejson.json](https://tiles.mapterhorn.com/tilejson.json) とします。**

このため、`fusite2` にあった「地形:」ドロップダウンメニューは消滅しています。

## fusion について

`fusite2` から `fusite3` にアップグレードする理由は、[https://github.com/hfu/fusi](https://github.com/hfu/fusi) の仕事が [mapterhorn.com](https://mapterhorn.com) に upstream contribute されたことです。この統合を **fusion** と呼んでいます。

## オマージュ

この実装は [Mapterhorn](https://mapterhorn.com/) と [Oliver Wipfli](https://github.com/wipfli) 氏による素晴らしい Terrarium タイルサービスの上に成り立っています。Mapterhorn プロジェクトへの敬意と感謝を表します。

## サポートされているテーマ

`docs/index.html` の実装で利用できる主なテーマ（`theme` パラメータ）:

- `osm` — OpenStreetMap のラスタタイルを背景に表示します。
- `gsi` — 国土地理院の最適化ベクトルタイル（bvmap-overdrive / MLT）を読み込み、行政区画や道路等のベクトル情報を重ねます。
- `gsi-ortho` — 国土地理院のシームレス航空写真タイル（seamlessphoto）を背景に使用します。
- `contour` — `maplibre-contour` を使って Terrarium 標高タイルから動的に等高線を生成します。
- `multidirectional` — 複数光源を用いた hillshade 表示（ハイライト/シャドウ色配列、光源方向、高度、強調度を調整可能）。

## URL フラグメントでの操作

ページの状態は URL のフラグメントで表現できます。形式:

```
#map=<zoom>/<lat>/<lng>/<pitch>/<bearing>&theme=<theme>&exag=<exaggeration>
```

例:

- デフォルト: `https://<your-host>/fusite3/`（UI から操作）
- 東京を GSI テーマで: `...#map=14/35.6812/139.7671/45/0&theme=gsi`
- 島原を等高線テーマで: `...#map=14/32.75/129.87/20/0&theme=contour&exag=2.0`

UI の `テーマ` ドロップダウンで選択すると、ページの再読み込みなしに地図が更新され、URL フラグメントは `history.replaceState` によって更新されます。

## コントロールと操作

- 右上: ナビゲーション（ズーム/回転/ピッチ） / フルスクリーン / 現在地 / GlobeControl
- 左下: 地形強調（Terrain Exaggeration）のスライダー（0〜3）
- 左上: 情報パネル（`テーマ` の選択、説明、出典表示）

## データソースとライセンス

- 標高タイル: Terrarium 形式（tileSize 512）を [Mapterhorn](https://mapterhorn.com/) から取得
- GSI ベクトルタイル（bvmap-overdrive）は `https://tunnel.optgeo.org/martin/bvmap-overdrive/{z}/{x}/{y}` を利用
- 国土地理院データ利用に関する承認表示: R 7JHs 542

## ローカルでの実行

静的ファイルなので簡単にローカルサーバで確認できます:

```bash
cd docs
python3 -m http.server 8000
# ブラウザで http://localhost:8000 を開く
```

または:

```bash
npx http-server docs -p 8000
```

## 技術スタック

- Map rendering: `maplibre-gl` (loaded from `https://unpkg.com/maplibre-gl@^5.13.0` in `docs/index.html`)
- Contour generation: `maplibre-contour` (v0.0.5, loaded from unpkg in `docs/index.html`)

## 貢献について

小さな修正（ドキュメント、スタイル調整、プリセット追加など）はプルリクエスト歓迎です。大きな機能追加や API 変更は Issue で事前に相談してください。

## ライセンス

測量法に基づく国土地理院長承認（使用）R 7JHs 542
