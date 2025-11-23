

## ファイル形式

このリポで扱う「データ形式」はざっくり2レイヤーあります。

  - cosmos.gl ライブラリ: ファイルを直接読む機能はなく、Float32Array などの配列で点座標・リンクを渡す API です。どんなファイルでも、アプリ側で読み込んで配列に変換できれば利用できます。
  - Cosmograph のビューワ (cosmograph.app の「run」リンクと同様): 入力は CSV のエッジリストを想定しています。最低限 source,target 列があれば動きます（ID は数値/文字列どちらも可）。任意で weight やノード属性の列を増やせますが、ビジュアルで使うなら色やサイズをどう反映するかをアプリ側で決める必要があります。

 つまり、GraphML/GEXF/JSON など既存フォーマットはそのまま「受け付ける」わけではなく、1) CSVエッジリストに変換するか、2) 独自パーサで配列にしてライブラリ API に渡す、のどちらかで対応します。どのフォーマットから変換したいか教えてもらえれば、変換手順を具体的に書きます。


## リポのざっくり構成

  - ルート: package.json (ビルド/Storybook/lint 用スクリプト), rollup.config.js と vite.config.ts (ライブラリ bundling), tsconfig.json, 各種ポリシー/README 類。
  - src/index.ts: 公開エントリ。下記モジュールを束ねる。
  - src/graph/: グラフ本体の実装 (シミュレーション・描画の中核)。
  - src/modules/: 点/リンク/ラベル/シェーダーなどの機能別モジュール群。
  - src/stories/: Storybook 用のデモと設定。
  - src/config.ts, src/variables.ts, src/helper.ts など: 設定値やユーティリティ。
  - ビルド成果物は npm run build で dist/ に生成、Storybook は npm run build:storybook で storybook-static/ が生成される。