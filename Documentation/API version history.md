# bSDD API バージョン履歴
これは https://api.bsdd.buildingsmart.org におけるAPIのバージョン履歴である。

新しいAPIやアップデートは、常にまずbSDDのテスト環境に公開される: https://test.bsdd.buildingsmart.org

予定されている更新やその他の技術的な議論については、[bSDD tech updates forum](https://forums.buildingsmart.org/t/bsdd-tech-updates/4889) をご覧ください。

#
# バージョン管理戦略
新しいバージョンは、現在のバージョンを「壊す」場合にのみ作成される。例えば、APIの出力に新しいフィールドを追加しても、アプリは壊れない（はずだ）。一方、出力フィールドを削除することは、破壊的な変更であり、そのAPIの新しいバージョンが作成されることになる。

APIに新バージョンがある場合、新バージョンのリリース後少なくとも6ヶ月間は旧バージョンをサポートする。 

## 2025-09-17
新しいAPIメソッド：
 * api/DictionaryDownload/bsdd/v1 (HTTPGET)
    - 完全な辞書をjsonファイル（bsdd形式）としてダウンロードする。
    - 指定された日付以降に辞書が変更された場合にのみファイルをダウンロードするために、「前回のダウンロード日」（DateFrom）を指定する。
 * api/DictionaryDownload/sketchup/v2 (HTTPGET)
    - (v1として)POSTオペレーションではなくGETオペレーションである。
    - 指定された日付以降に辞書が変更された場合にのみファイルをダウンロードするために、「前回のダウンロード日」（DateFrom）を指定する。

## 2025-06-27
APIメソッドを変更しました：
 * api/Dictionary/v1/Classes：
    - オプション"RelatedIfcEntities"が追加されました。関連するIFCエンティティを複数指定できます。

以下の廃止されたAPIメソッドを削除した：
  * api/Classification/v3
  * api/ClassificationSearchOpen/v1
  * api/Domain/v2
  * api/Domain/v2/Classifications
  * api/Domain/v3
  * api/Domain/v3/Classifications
  * api/TextSearchListOpen/v5

## 2024-09-23
APIメソッドを変更しました：
 * api/Dictionary/v1/Classes：
    - オプション"RelatedIfcEntity"が追加された。
 * api/TextSearch/v2：
    - 辞書リストの出力に"code"フィールドが追加された。


## 2024-08-16
新しいAPIメソッド：
 * api/Class/Relations/v1: クラス関係または逆関係の取得 (ページ分割)
 * api/Class/Properties/v1: クラスのプロパティを取得 (ページ分割)
 * api/UploadImportFile/v2：大きなファイルのアップロードに対応。検証は非同期で行われ、結果はメールで送信される。
 * api/Dictionary/Popular/v1: 最も人気のある辞書の短いリストを取得する
 * api/Property/Relations/v1: プロパティ関係または逆関係を取得 (ページ分割)
 * api/Property/Classes/v1: プロパティを使用するクラスのリストを取得 (ページ分割)
 * api/TextSearch/v2: 新しいフィルターオプションと出力の変更

APIメソッドを変更しました：
 * api/Dictionary/v1/Classes：
    - オプション"検索テキスト"が追加された。
 * api/Dictionary/v1/Properties：
    - オプション"検索テキスト"が追加された。
 * api/DictionaryDownload/sketchup/v1：
    - ".xsdファイルの代わりに".skcファイルをダウンロードするようになった。


## 2024-03-01
- 辞書のアップロード時に、テスト目的であることを示すことができるようになった。

チャンジェンドAPI：
 * api/Class/v1：
    - オプション IncludeReverseRelations の追加
 * api/Dictionary/v1：
    - オプション IncludeTestDictionaries の追加
 * api/UploadImportFile/v1：
    - IsTestオプション追加
 * api/TextSearch/v1：
    - 複数の単語(パーツ)を含むテキスト検索で、最初の単語の一部('startswith')が一致した場合にも検索結果が得られるようになりました。以前は、最初の単語が完全に一致する場合のみ検索していました。


## 2023-11-08
名前の変更
 * 分類 ==&gt; クラス
 * ドメイン ==&gt; 辞書
 * NamespaceUri ==&gt; Uri
 * IncludeChilds ==&gt; IncludeChildren

これは、API名自体、入力契約、出力契約のいずれかにこれらの名前のいずれかを持つすべてのAPIを含む。これらすべてのAPIについて、新しいバージョン、新しい名前のAPIが作成されました。既存のAPIは本番稼動後も少なくとも6ヶ月間は存続しますが、新しいAPIを使用することをお勧めします。

その他の変更点
 * "マテリアルはもう別個に扱われることはなく、マテリアルを型とするクラスとして扱われる。
 * インポート・フィールド ClassificationProperty.ExternalPropertyUri は完全に削除されました。PropertyNamespaceUri（現在はPropertyUriと呼ばれています）フィールドが既にそれに取って代わりました。
 * 検索APIがページネーションをサポート

APIを変更した：
 * api/Class/v1: api/Classification/v4を置き換える新しいもの。
    - includeClassPropertiesオプションを追加しました。trueの場合、classPropertiesがフェッチされます。デフォルトはfalseです。
    - includeClassRelationsオプションを追加。trueを指定すると、クラス・リレーションがフェッチされます。デフォルトはfalseです。
    - 新しい出力フィールド：クラス.説明
 * api/Class/Search/v1: api/ClassificationSearchOpen/v1を置き換える新しいもの。
    - リターン契約は、常に1つの項目を含む辞書のリストの代わりに、1つの辞書だけを含むようになりました。
    - ページネーションに対応
 * api/Dictionary/v1: 新しい。api/Domain/v3 を置き換える。
    - ページネーションに対応
 * api/Dictionary/v1/Classes: 新しい、api/Domain/v3/Classifications を置き換える。
    - 材料はもう個別にリストアップされていない
    - ページネーションに対応
    - ClassTypeのオプションフィルター
 * api/Dictionary/v1/Properties: new
    - ページネーションに対応
 * api/Dictionary/v1 PUT, DELETE: new, replace api/Domain/v1
 * api/DictionaryDownload/sketchup/v1: api/RequestExportFile/preview を置き換える新しいもの。
 * api/Materialはapi/Classに置き換えられました。
 * api/Property/v4: api/Property/v3を置き換える新しいもの。
 * api/SearchInDictionary/v1: api/SearchList(Open)/v2を置き換える新しいもの。
    - ページネーションに対応
 * api/TextSearch/v1: api/TextSearchListOpen/v6 を置き換える新しいもの。
    - ページネーションに対応
  * api/UploadImportFile/v1：更新され、新旧両方のインポートjsonを受け付けるようになりました。古いインポートjsonのサポートは非推奨となります。

置き換えられたすべてのAPIは、今のところまだ機能するが、swaggerのページhttps://test.bsdd.buildingsmart.org/swagger。

## 2023-08-10
 * 追加: api/Domain/v3/{organizationCode}/{code}/{version} - put: ドメインバージョンのステータスを更新する
 * 追加: api/Domain/v3/{organizationCode}/{code}/{version} - delete: ドメインのバージョンを削除する
 * 追加: api/Domain/v3/{organizationCode}/{code} - delete: ドメインを削除する。
 * 変更: api/Classification/v4: 分類プロパティと分類リレーションの結果コントラクトに"namespaceUri"が含まれるようになった。
 * 変更: api/Property/v3: プロパティ関係の結果契約に"namespaceUri"が含まれるようになった。

## 2023-05-10
 * 変更: api/Domain/v3: 結果契約に"OrganizationCodeOwner"が含まれるようになった。
 * 修正: api/Classification/v4のswaggerドキュメントが修正されました。

## 2022-12-29
 * 新バージョン：api/Domain/v3：v2と同じ。
 * 新バージョン：api/Domain/v3/Classifications：出力契約が変更されました - 素材は別のリストで返されるようになりました。
 * 新しいバージョン: api/TestSearchListOpen/v6: 出力の契約が変更された - 素材は別のリストで返されるようになった; 入力の契約はTypeFilterで"Materials"も受け付けるようになった; TypeFilterの値は大文字と小文字を区別しないようになった
 * 変更: api/TestSearchListOpen/v5: TypeFilter の値が大文字と小文字を区別しないようになった。

新しいAPIの旧バージョンは、少なくとも2023年9月まで利用可能である。

## 2022-10-23
 * 新しいバージョン: api/Classification/v4: 属性PossibleValuesの名前がAllowedValuesに変更されました。
 * 新しいバージョン: api/Material/v2: 属性PossibleValuesの名前がAllowedValuesに変更されました。
 * 新しいバージョン: api/Property/v3: 属性 PossibleValues の名前が AllowedValues に変更された (インポート属性名と一致するようになった)。
 
新しいAPIの旧バージョンは、少なくとも2023年7月までは利用可能である。

## 2022-09-08
注意：セキュリティで保護されたAPIにアクセスするには、"URL1"の代わりに"URL0"を使用する必要があります！

## 2022-09-05
 * 新規: api/ClassificationSearchOpen/v1、分類検索のための最適化されたAPI
 * 更新：api/Domain/v2およびapi/Domain/v2/Classificationsは、bSDDのデータが最後に更新された日時をLastUpdatedUtcとして返す。
 * 更新しました：DQ0は"へ、"は"へ自動マッチングされます。

## 2022-08-23
 * 更新: api/Domain/v2/ClassificationsがAccept-Languageヘッダーに対応しました。
 * 更新: api/Domain/v2およびapi/Domain/v2/Classificationsの出力フィールドにReleaseDate、MoreInfoUrl、Statusが追加されました。
 * 更新：api/Classification/v3の出力フィールドFractionが追加されました（ClassificationRelation型内）。

## 2022-07-01
 * 更新：api/Classification/v3は、異なる言語のデータを要求するためのAccept-Languageヘッダーに対応しました。
 * 更新: api/Property/v2が、異なる言語のデータを要求するためのAccept-Languageヘッダーに対応しました。
 * 更新：api/Property/v2およびapi/Classification/v3は、ユニットのQUDTコードも返すようになりました。
 * 更新: api/RequestExportfile/preview, SketchUpの出力ファイルがキャッシュされるようになりました。

## 2022-04-30
* 新規: マテリアルの詳細を取得するためのapi/Material/v1
* 新規: マテリアルを検索するための api/Material/SearchOpen/preview
* 更新: api/Classification/v3はRDF-XML、Turtle、Html形式のデータを返せるようになりました：

| <nobr>Accept</nobr> ヘッダー | <nobr>出力フォーマット</nobr> |
|--|--|
| [デフォルト］ | json |
| application/rdf+xml | RDF XML |
| アプリケーション/エックスタートル | turtle |
| テキスト/html | html |
| テキスト/タートル | turtle |

## 2021-11-01
* 新規: api/Domain/v2/Classificationsでドメインの分類リストを取得

## 2021-09-01
* オフィシャル・ファースト・リリース
