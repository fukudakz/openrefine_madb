# OpenRefine変換ファイル - RCGS個別資料データ

## 概要
このファイルは `rcgs_item_sparql_2022.csv` を対象とするOpenRefineの変換ファイルです。
RCGSの個別資料データをMADBフォーマットに変換するために使用します。

## 対象ファイル
- 原データ: `rcgs_item_sparql_2022.csv`
- マッピング仕様: `mappingspec_madb_game.csv` (通しNo: 1-6)
- 変換先クラス: ゲーム個別資料

## 変換内容

### 列の変換・追加
1. **s** → **メモ**: URIからIDを抽出 (`https://collection.rcgs.jp/resource/` を削除)
2. **exemplarOf** → **例示されたパッケージ**: パッケージIDに変換
3. **exemplarOf** → **所蔵DBリンク**: `/resource/` を `/page/` に置換
4. **spatial** → **保管場所**: 列名変更のみ
5. **holdingAgent** → **管理者**: 責任主体IDに変換
6. **identifiers** → **資料ID**: 複数値から「RCGSa」を含むIDのみ抽出

### 固定値の追加
- **サブタイプ**: `gm`
- **タイプ**: `GameItem`
- **ジャンル**: `ゲーム個別資料`

## 使用方法

### 1. OpenRefineでプロジェクトを作成
```
1. OpenRefineを起動
2. 「Create Project」→「Choose Files」
3. rcgs_item_sparql_2022.csv を選択
4. プロジェクト名を設定して「Create Project」
```

### 2. 変換ファイルの適用
```
1. 「Undo / Redo」タブをクリック
2. 「Apply...」ボタンをクリック
3. rcgs_item_transform.json の内容を貼り付け
4. 「Perform Operations」をクリック
```

### 3. 結果の確認
変換後、以下の列が生成されます：
- メモ
- 例示されたパッケージ
- 所蔵DBリンク
- 保管場所
- 管理者
- 資料ID
- サブタイプ
- タイプ
- ジャンル

## 注意事項
- `identifiers` 列の処理では、パイプ記号(|)で区切られた複数値から「RCGSa」を含むもののみを抽出します
- URI形式のデータは適切にIDに変換されます
- 元の列（s, exemplarOf, owns, holdingAgent, identifiers）は変換後に削除されます

## トラブルシューティング
- 変換が失敗する場合は、原データのフォーマットを確認してください
- 特に列名や区切り文字が仕様と異なる場合は、変換ファイルの修正が必要です

## ファイル構成
```
openrefine_madb/
├── rcgs_item_transform.json     # 変換ファイル
├── rcgs_item_sparql_2022.csv    # 原データ
├── mappingspec_madb_game.csv    # マッピング仕様書
└── README_rcgs_item_transform.md # このファイル
``` 