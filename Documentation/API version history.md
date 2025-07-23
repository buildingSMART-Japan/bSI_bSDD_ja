# bSDD API バージョン履歴

これは https://api.bsdd.buildingsmart.org におけるAPIのバージョン履歴である。

新しいAPIやアップデートは、常にまずbSDDのテスト環境に公開される: https://test.bsdd.buildingsmart.org

予定されているアップデートやその他の技術的な議論については、以下を参照のこと。[bSDD技術アップデートフォーラム](https://forums.buildingsmart.org/t/bsdd-tech-updates/4889).

#
# バージョニング戦略
新しいバージョンは、それが現在のバージョンを「壊す」場合にのみ作成される。 例えば、APIの出力に新しいフィールドを追加しても、アプリは壊れない（あるいは壊すべきではない）。 一方、出力フィールドを削除することは壊す変更であり、そのAPIの新しいバージョンが作成されることになる。

APIに新バージョンがある場合、新バージョンのリリース後少なくとも6ヶ月間は旧バージョンをサポートする。 

## 2025-06-27

APIメソッドを変更しました：
 * api/Dictionary/v1/Classes：
    - オプション "RelatedIfcEntities "が追加されました。 関連する複数のIFCエンティティを指定できます。

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
    - オプション「RelatedIfcEntity」の追加
 * api/TextSearch/v2：
    - 辞書リストの出力に "code "フィールドを追加


## 2024-08-16

新しいAPIメソッド：
 * api/Class/Relations/v1: クラス関係または逆関係の取得 (ページ分割)
 * api/Class/Properties/v1: クラスのプロパティを取得 (ページ分割)
 * api/UploadImportFile/v2: 大容量ファイルのアップロードに対応。 検証は非同期で行われ、結果はメールで送信される。
 * api/Dictionary/Popular/v1: 最も人気のある辞書の短いリストを取得する
 * api/Property/Relations/v1: プロパティ関係または逆関係を取得 (ページ分割)
 * api/Property/Classes/v1: プロパティを使用するクラスのリストを取得 (ページ分割)
 * api/TextSearch/v2: 新しいフィルターオプションと出力の変更

APIメソッドを変更しました：
 * api/Dictionary/v1/Classes：
    - オプション「SearchText」追加
 * api/Dictionary/v1/Properties：
    - オプション「SearchText」追加
 * api/DictionaryDownload/sketchup/v1：
    - .xsd "の代わりに".skc "ファイルをダウンロードするようになりました。


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
    - 複数の単語(パーツ)を含むテキスト検索で、最初の単語の一部('startswith')が一致した場合にも検索結果が表示されるようになりました。 以前は最初の単語の完全一致のみが検索されていました。


## 2023-11-08

名前が変わる：
 * 分類 ==> クラス
 * ドメイン ==> 辞書
 * NamespaceUri ==> Uri
 * IncludeChilds ==> IncludeChildren

これは、API名自体、入力コントラクト、出力コントラクトのいずれかにこれらの名前のいずれかを持つすべてのAPIに関係します。 これらのすべてのAPIについて、新しいバージョン（一部は新しい名前）が作成されました。 既存のAPIは、本番稼動後少なくとも6ヶ月間は残りますが、新しいAPIを使用することをお勧めします。

その他の変更点
 * 「マテリアル」はもう別個に扱われることはなく、マテリアルを型とするクラスとして扱われる。
 * インポート・フィールドClassificationProperty.ExternalPropertyUriは完全に削除されました。 既にPropertyNamespaceUriフィールド（現在はPropertyUriと呼ばれています）がそれに取って代わりました。
 * 検索APIがページネーションをサポート

APIの変更：
 * api/Class/v1: api/Classification/v4を置き換える新しいもの。
    - includeClassPropertiesオプションが追加されました。 trueの場合、classPropertiesがフェッチされます。 デフォルトはfalseです。
    - オプション includeClassRelations が追加されました。 true の場合、classRelations が取得されます。 デフォルトは false です。
    - 新しい出力フィールド：Class.Description
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
  * api/UploadImportFile/v1：更新され、新旧両方のインポートjsonを受け付けるようになりました。 古いインポートjsonのサポートは非推奨となります。

置き換えられたすべてのAPIは、今のところまだ機能するが、swaggerのページhttps://test.bsdd.buildingsmart.org/swagger。

## 2023-08-10

 * 追加：api/Domain/v3/{organizationCode}/{code}/{version} - put: ドメインバージョンのステータスを更新する。
 * 追加: api/Domain/v3/{organizationCode}/{code}/{version} - delete: ドメインバージョンの削除
 * 追加: api/Domain/v3/{organizationCode}/{code} - delete: ドメインを削除する。
 * 変更：api/Classification/v4：分類プロパティと分類リレーションの結果コントラクトに "namespaceUri "が含まれるようになった。
 * 変更: api/Property/v3: プロパティ関係の結果コントラクトに "namespaceUri "が含まれるようになった。

## 2023-05-10

 * 変更: api/Domain/v3: 結果契約に「OrganizationCodeOwner」が含まれるようになった。
 * 修正: api/Classification/v4のswaggerドキュメントが修正されました。

## 2022-12-29

 * 新バージョン：api/Domain/v3：v2と同じ。
 * 新バージョン：api/Domain/v3/Classifications：出力契約が変更されました - 素材は別のリストで返されるようになりました。
 * 新しいバージョン: api/TestSearchListOpen/v6: 出力の契約が変更された - 材料は別のリストで返されるようになった。
 * 変更: api/TestSearchListOpen/v5: TypeFilter の値が大文字と小文字を区別しないようになった。

 新しいAPIの旧バージョンは、少なくとも2023年9月まで利用可能である。

## 2022-10-23

 * 新しいバージョン: api/Classification/v4: 属性PossibleValuesの名前がAllowedValuesに変更されました。
 * 新しいバージョン: api/Material/v2: 属性PossibleValuesの名前がAllowedValuesに変更されました。
 * 新しいバージョン: api/Property/v3: 属性 PossibleValues の名前が AllowedValues に変更された (インポート属性名と一致するようになった)。
 
 新しいAPIの旧バージョンは、少なくとも2023年7月までは利用可能である。

## 2022-09-08

注意：セキュリティで保護されたAPIにアクセスするには**https://authentication.buildingsmart.org**の代わりに https://buildingsmartservices.b2clogin.com ！

## 2022-09-05

 * 新規: api/ClassificationSearchOpen/v1、分類検索のための最適化されたAPI
 * 更新：api/Domain/v2およびapi/Domain/v2/Classificationsは、bSDDのデータが最後に更新された日時をLastUpdatedUtcとして返す。
 * 更新："http://idenfitier... "は "https://identifier... "に置き換えられました。"http://identifier... "を検索すると、当分の間、"https://idenfitier... "とオートマッチします。

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
* 新機能：マテリアルの詳細を取得するためのapi/Material/v1
* 新規: マテリアルを検索するための api/Material/SearchOpen/preview
* 更新： api/Classification/v3は、RDF-XML、Turtle、Html形式のデータを返すことができるようになりました：

| Accept ヘッダー | 出力フォーマット |
|--|--|
| [デフォルト］ | json |
| application/rdf+xml | RDF XML |
| アプリケーション/エックスタートル | 亀 |
| テキスト/html | html |
| テキスト/タートル | 亀 |

## 2021-11-01
* 新規: api/Domain/v2/Classificationsでドメインの分類リストを取得

## 2021-09-01
* オフィシャル・ファースト・リリース
