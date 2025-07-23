<h2 id="table-of-content">Table of contents</h2>

* [Data model](#data-model)
* [JSON format](#json-format)
* [List of fields](#list-of-fields)
    * [Dictionary](#Dictionary)  
    * [Class](#Class)  
    * [Property](#Property)  
    * [ClassProperty](#ClassProperty)  
    * [ClassRelation](#ClassRelation)  
    * [AllowedValue](#AllowedValue)  
    * [PropertyRelation](#PropertyRelation)  
* [Additional explanations](#additional-explanations)
* [Notifications](#notifications)


<h2 id="data-model">Data model</h2>

The bSDD is a service to facilitate the distribution of data dictionaries (read below about what those are) published by independent organisations. The diagram below shows the simplified data model behind the bSDD:

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_model.png" alt="bSDD entity diagram" style="width: 650px"/>

See our example demonstrating the usage of the above concepts: [bSDD data example](https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png):
<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png" alt="bSDD entity diagram" style="width: 700px"/>

We also have a demonstration dictionary: ["Fruit and vegetables"](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.1).

📢 Read about the 最新 technical updates in the dedicated forum topic: [https://forums.buildingsmart.org/t/bsdd-tech-updates/4889](https://forums.buildingsmart.org/t/bsdd-tech-updates/4889)

<h2 id="json-format">JSON format</h2>

You can deliver data for the buildingSMART Data Dictionary in the JSON file following our standard, which we explain in this document. You can also find the JSON and Excel templates in [/Model/Import Model](https://github.com/buildingSMART/bSDD/tree/master/Model/Import%20Model).

Click on the link to get the list of allowed codes for [countries](https://api.bsdd.buildingsmart.org/api/Country/v1), [languages](https://api.bsdd.buildingsmart.org/api/Language/v1), [units](https://api.bsdd.buildingsmart.org/api/Unit/v1), [reference documents](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1) and [ifc class](https://api.bsdd.buildingsmart.org/api/Dictionary/v2/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3).
参考資料が不足していると思われる場合は、次の方法でお知らせください。[問題掲載](https://github.com/buildingSMART/bSDD/issues)JSONのすべての値は、数値のExampleとAllowedValueフィールドを含め、二重引用符で囲まれた文字列でなければならない。

If you are unfamiliar with JSON, we recommend reading [Introduction to JSON](https://javaee.github.io/tutorial/jsonp001.html). Please note that JSON is a format meant for computer systems to exchange data. If you have your dictionary data in a computer system, then it's best to let the system create the JSON for you.

<h2 id="list-of-fields">List of fields</h2>

NB Default values will only be applied if a field is not specified. If you specify a field value of "null"そのdefault will not be applied. Note that "null" is not allowed for all fields.

<h3 id="Dictionary">Dictionary</h3>

`Data dictionary` - '_a centralized repository of information about data such as meaning, relationships to other data, origin usage and format._' [ISO23386]. '_database that contains metadata_' [ISO12006-3]. Each `Dictionary` (previously `domain`) consists of `Classes` (previously `classifications`) and `Properties`, which could be related to each other or with other `Dictionaries`. Each `Dictionary` object contains general metadata about it, as listed in the table below.

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|------------------|------------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="OrganizationCode">組織コード</span>。 | テキスト | ✅ |  | bSDD に登録したときに受け取った組織のコード。 あなたの組織がまだコードを持っていない場合は、[bSDD User Helpdesk](https://bsi-technicalservices.atlassian.net/servicedesk/customer/portal/3/group/4/create/25) でリクエストしてください。 すべての URI リンクに表示されるため、コードはなるべく短い方がよいでしょう。 許容される文字については、[コードフォーマット](#code-format) のセクションを参照してください。 このコードは数字で始まることはできません。 コード例: "ifc". |
| <span id="DictionaryCode">辞書コード</span>。 | テキスト | ✅ |  | 辞書のコード、できれば短いもの。 例："ifc"。 コードフォーマット](#code-format)の項を参照のこと。 |
| <span id="DictionaryName">辞書名</span>。 | テキスト | ✅\ |  | 辞書が存在する場合、この名前を指定する必要はない。 |
| <span id="DictionaryVersion">辞書バージョン</span>。 | テキスト | ✅ |  | 許容される形式：最大3つのドット区切りの数字、例：1.0.1。 許容される形式："12"、"10.1"、"1.2.3"。 許容されない形式："1.2.3.4"、"ベータ"、"2x3"。 [Semantic Versioning](https://semver.org/)のアプローチに従うことを推奨する。 |
| <span id="LanguageIsoCode">言語アイソコード</span>。 | テキスト | ✅ |  | ISO言語コード：データの言語を表します。 複数の言語でデータを配信したい場合は、言語ごとにJSONファイルを使用してください。 参考リスト[languages](https://api.bsdd.buildingsmart.org/api/Language/v1)を参照してください。 ◆例："de-DE" |
| <span id="LanguageOnly">言語専用</span>。 | ブーリアン | ✅ |  | JSONが言語固有の情報のみを含む場合はtrue、そうでない場合はno。 |
| <span id="UseOwnUri">UseOwnUri</span>。 | ブーリアン | ✅ |  | クラスとプロパティをグローバルに一意に識別するために、独自のURIを使用します。独自のURIを使用しない場合、"https://identifier.buildingsmart.org "で始まるURIがそれぞれの`クラス`と`プロパティ`に割り当てられます。 |
| <span id="DictionaryUri">ディクショナリ</span>。 | テキスト | ✅\ |  | UseOwnUri = trueの場合は必須。すべてのクラスおよびプロパティのURIの最初の部分であるグローバルに一意なURIを指定します。例："urn:mycompany:mydictionary "または "https://mycompany.com/mydictionary" |
| <span id="ライセンス">ライセンス</span | テキスト |  |  | コンテンツのライセンスの識別子。 [Creative Commons](https://creativecommons.org/choose/)または[OSI Approved Licenses](https://opensource.org/licenses/)からライセンスを選択することをお勧めします。該当する場合は、標準化された[SPDX](https://spdx.org/licenses/)識別子を使用して、正規の信頼できる識別を行う必要があります。例えば、"MIT "または "CC-BY-4.0 "です。参考になるリソースは、[ChooseALicense.com](https://choosealicense.com/)です。 |
| <span id="LicenseUrl">ライセンスURL</span>。 | テキスト |  |  | ライセンスページは、指定された「ライセンス」名と一致する必要があります。 |
| <span id="ChangeRequestEmailAddress">ChangeRequestEmailAddress</span>。 | テキスト |  |  | ユーザーからの変更リクエストを受信するための単一のメールアドレス。 メールアドレスを提供することにより、ユーザーからのリクエストを転送し、APIを通じてアドレスを公開することに同意したものとみなされます。 ユーザーは、当社に連絡することにより、情報を撤回する権利を有します。 |
| <span id="ModelVersion">モデルバージョン</span>。 | テキスト |  |  | 入力JSONテンプレートのバージョン番号。 |
| <span id="MoreInfoUrl">MoreInfoUrl</span>。 | テキスト |  |  | 辞書に関する詳細情報を含むウェブページへのURL |
| <span id="QualityAssuranceProcedure">品質保証手続き</span>。 | テキスト |  |  | 例："ETIM international"、"AFNOR NF XP P07-150 (PPBIM)"、"bSI process"、"UN GHS 2015"、"UN CPC 1.1"、"Private"、"Unknown"。 |
| <span id="QualityAssuranceProcedureUrl">品質保証手続きURL</span>。 | テキスト |  |  | 品質保証手順に関する詳細情報を掲載したウェブページへの URL。例："https://www.buildingsmart.org/about/bsi-process" |
| <span id="ReleaseDate">リリース日</span>。 | 日時 |  |  | 日付時刻フォーマット](#datetime-format)を参照。 |
| <span id="Status">ステータス</span>。 | テキスト |  |  | 可能なバージョンステータス: `Preview`, `Active`, `Inactive`. 新しいバージョンをアップロードするときは、常に `Preview` になっている必要があります。その後、[API](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1) または [管理ポータル](https://manage.bsdd.buildingsmart.org/) を介してコンテンツを有効化または無効化できます。 続きを読む: [bSDD コンテンツのライフサイクル](https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/bSDD%20import%20tutorial.md#the-lifecycle-of-the-bsdd-dictionary-version) |
| <span id="クラス">クラス</span | クラス一覧 | ✅ |  | Class`型のオブジェクトのリスト。 Class](#class)の項を参照。 |
| <span id="Properties">プロパティ</span>。 | 物件リスト | ✅ |  | Property`型のオブジェクトのリスト。 Property](#property)の項を参照。 |

\* For delivering data in additional languages, it is sufficient to fill the `Dictionary` type fields, all `Code` fields and the fields marked with `Translatable?` = "Yes" of the other types. Ensure that the `OrganizationCode`, `DictionaryCode` and `DictionaryVersion` are exactly the same and if the data is for adding a language to an existing `Dictionary`, set the field `LanguageOnly` to true.

<h3 id="Class">Class</h3>

`Class` - '_description of a set of objects that share the same characteristics._' [ISO23386]. A `Class` can be any object (examples: "wall", "window") or abstract concept (examples: "time", "room") or process (examples: "installation", "disassembly").


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|---------------------------|--------------------------------|-------------|-----------------|--------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span | テキスト | ✅ |  | 例："abc-00123-01 "または "SpecialWall"。 コード検証が適用される、参照：[コードフォーマット](#code-format)。 接頭辞'Ifc'は、IFC標準のために予約されている。 |
| <span id="Name">名前</span>。 | テキスト | ✅ | ✅ | クラス名、例："IfcCurtainWall" |
| <span id="ClassType">クラスタイプ</span>。 | テキスト | ✅ |  | Class` 型、`Material` 型、`GroupOfProperties` 型、`AlternativeUse` 型のいずれかを指定する必要がある。 クラス型](#class-types) について詳しくはこちらを参照。 指定しない場合、デフォルトで `Class` 型が使用される。 ReferenceDocument` 型、`ComposedProperty` 型、`Dictionary` 型は非推奨となり、アップロード時に使用することはできないが、移行期間中は API の結果に表示されることがある。 |
| <span id="Definition">定義</span>。 | テキスト |  | ✅ | クラス`の定義、意味的な意味を説明する。 ISOに従った必須フィールド。 二重四角括弧リンク](#double-square-bracket-links)をサポートする。 |
| <span id="Description">説明</span>。 | テキスト |  | ✅ | 補足説明のための追加フィールド。 定義_が規格に由来し、さらに説明が必要な場合にのみ使用してください。 |
| <span id="ParentClassCode">親クラスコード</span>。 | テキスト |  |  | 親クラス `Class` への参照。 このフィールドのIDは、配信されたデータの中に存在しなければなりません。 例: "ifc-00123-00" リレーションシップを定義するには](#defining-relations)を参照してください。 |
| <span id="RelatedIfcEntityNamesList">関連Ifcエンティティ名リスト</span>。 | テキスト一覧 |  |  | この `Class` の表現として使用する IFC クラスのコード。 例: ['イフックウォール']. bSDD API [ifc classs](https://api.bsdd.buildingsmart.org/api/Dictionary/v3/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3%2F) を参照。 [リレーションシップの定義方法](#defining-relations) を参照。 |
| <span id="類義語</span></span | テキスト一覧 |  | ✅ | 検索しやすいように、このクラスの代替名称のリスト。 |
| <span id="ActivationDateUtc">アクティベーション日付Utc</span>。 | 日時 |  |  | 日付時刻フォーマット](#datetime-format)を参照。 |
| <span id="ReferenceCode">参照コード</span>。 | テキスト |  |  | 参照コードは辞書固有の用法を持つことができる。 NULLの場合、`Code`の値がフィールドを埋めるために使用される。 参照コードを空にするには、空の文字列""を使用する。 |
| <span id="CountriesOfUse">使用国</span>。 | テキスト一覧 |  |  | この`Class`が使用されている国のISOコードのリスト。 参照リスト[countries](https://api.bsdd.buildingsmart.org//api/Country/v1)を参照してください。 |
| <span id="CountryOfOrigin">原産国</span>。 | テキスト |  |  | この`クラス`の原産国のISO国コード。参照リスト[countries](https://api.bsdd.buildingsmart.org//api/Country/v1)を参照。 |
| <span id="CreatorLanguageIsoCode">クリエイター言語アイソコード</span>。 | テキスト |  |  | 作成者の言語ISOコード。参考リスト[languages](https://api.bsdd.buildingsmart.org/api/Language/v1)を参照。 |
| <span id="DeActivationDateUtc">DeActivationDateUtc</span>。 | 日時 |  |  | 日付時刻フォーマット](#datetime-format)を参照。 |
| <span id="DeprecationExplanation">DeprecationExplanation</span>。 | テキスト |  | ✅ | 非推奨の定義のみを埋める。 |
| <span id="DocumentReference">ドキュメント参照</span>。 | テキスト |  |  | クラス`の完全な、または公式な定義が記載された文書への参照。参照リスト[参照文書](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)を参照。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | ディクショナリ・レベルで `UseOwnUri = true` を指定した場合は、`Class' をグローバルに一意に識別する URI を指定する必要があります。 |
| <span id="ReplacedObjectCodes">ReplacedObjectCodes</span>。 | テキスト一覧 |  |  | このクラスが置き換えるクラス・コードのリスト |
| <span id="ReplacingObjectCodes">ReplacingObjectCodes</span>。 | テキスト一覧 |  |  | このクラスは次のクラスコードに置き換えられる。 |
| <span id="RevisionDateUtc">リビジョンデートUtc</span>。 | 日時 |  |  | 日付時刻フォーマット](#datetime-format)を参照。 |
| <span id="RevisionNumber">リビジョン番号</span>。 | 整数 |  |  |  |
| <span id="Status">ステータス</span>。 | テキスト |  |  | クラス `Class` の状態: `Active` (デフォルト) または `Inactive |
| <span id="SubdivisionsOfUse">細分化された用途</span>。 | テキスト一覧 |  | ✅ | 使用地域のリスト 例："US-MT" |
| <span id="Uid">Uid</span>。 | テキスト |  |  | URIだけでは不十分な場合のための一意な識別（ID）。 |
| <span id="VersionDateUtc">バージョン日付Utc</span>。 | 日時 |  |  | デフォルトでは、インポートされた日付が使われます。 日付時刻フォーマット](#datetime-format)を参照してください。 |
| <span id="VersionNumber">バージョン番号</span>。 | 整数 |  |  |  |
| <span id="VisualRepresentationUri">VisualRepresentationUri</span>。 | テキスト |  | ✅ |  |
| <span id="ClassProperties">クラスプロパティ</span>。 | クラスプロパティ一覧 |  |  | クラスプロパティ](#ClassProperty)の項を参照。 |
| <span id="ClassRelations">クラス関係</span>。 | クラス関係一覧 |  |  | クラスリレーション](#ClassRelation)参照。 |

Note: Since the release of November 2023, Materials are not treated separately anymore. A `Material` is now simply a `Class` of type `Material`.

<h3 id="Property">Property</h3>

`Property` - '_an inherent or acquired feature of an item [`Class`]. Example: Thermal efficiency, heat flow, (...), colour._' [ISO23386].  The assignment of `Properties` to `Classes` is handled through the interim [ClassProperty](#ClassProperty) object. 


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|-------------------------------|--------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span | テキスト | ✅ |  | 辞書内のプロパティの一意な識別。 例："abc-00123-01 "または "SpecialWidth"。 コードバリデーションが適用されます。[コードフォーマット](#code-format)を参照してください。 |
| <span id="Name">名前</span>。 | テキスト | ✅ | ✅ | プロパティの名前 例："IsExternal" |
| <span id="Definition">定義</span>。 | テキスト |  | ✅ | プロパティ`の定義、意味的な意味を説明する。 ISOに従った必須フィールド。 二重四角括弧リンク](#double-square-bracket-links)をサポートする。 |
| <span id="Description">説明</span>。 | テキスト |  | ✅ | 補足説明のための追加フィールド。 定義_が規格に由来し、さらに説明が必要な場合にのみ使用してください。 |
| <span id="DataType">データ型</span>。 | テキスト | ✅ |  | プロパティが表現されるデータ型。 `Boolean`、`Character`、`Integer`、`Real`、`String`、`Time` のいずれかでなければならない。 |
| <span id="単位">単位</span | テキスト一覧 |  |  | 単位は、値を測定できる目盛りを表します（ISO 80000またはISO 4217、またはISO 8601）。 値のリスト。 参照リスト（JSON） [units](https://api.bsdd.buildingsmart.org/api/Unit/v1)を参照してください。 私たちは、[QUDT](http://www.qudt.org/)語彙のサポートに取り組んでいます。 QUDT単位を使用してインポートしたい場合、またはAPI出力にQUDT単位を持たせたい場合は、お知らせください。 |
| <span id="例">例</span>。 | テキスト |  | ✅ | プロパティの例 |
| <span id="ActivationDateUtc">アクティベーション日付Utc</span>。 | 日時 |  |  | 日付時刻フォーマット](#datetime-format)を参照。 |
| <span id="ConnectedPropertyCodes">接続プロパティコード</span>。 | テキスト一覧 |  |  | 他の辞書のプロパティである場合は、コードの代わりに完全なURIを指定することもできます。 アセンブルプロパティ](#assembling-properties)を参照してください。 |
| <span id="CountriesOfUse">使用国</span>。 | テキスト一覧 |  |  | この`プロパティ`が使用されている国のISOコードのリスト。 参照リスト[countries](https://api.bsdd.buildingsmart.org/api/Country/v1)を参照してください。 |
| <span id="CountryOfOrigin">原産国</span>。 | テキスト |  |  | この`プロパティ`の原産国のISO国コード。参照リスト[countries](https://api.bsdd.buildingsmart.org//api/Country/v1)を参照。 |
| <span id="CreatorLanguageIsoCode">クリエイター言語アイソコード</span>。 | テキスト |  |  | 作成者の言語ISOコード。 参照リスト（JSON）[languages](https://api.bsdd.buildingsmart.org/api/Language/v1)を参照。 |
| <span id="DeActivationDateUtc">DeActivationDateUtc</span>。 | 日時 |  |  | 日付時刻フォーマット](#datetime-format)を参照。 |
| <span id="DeprecationExplanation">DeprecationExplanation</span>。 | テキスト |  | ✅ |  |
| <span id="Dimension">ディメンション</span>。 | テキスト |  |  | 物理量の場合、ISO 80000-1 で定義されている [International_System_of_Quantities](https://en.wikipedia.org/wiki/International_System_of_Quantities) に従って次元を指定する。長さ`、質量`、時間`、電流`、熱力学的温度`、物質量`、光度`の順で指定する。 例えば、速度(m/s)は "1 0 -1 0 0 0 0" と表記する。その他の例は [IDS documentation](https://github.com/buildingSMART/IDS/blob/ver/1.0.x/Documentation/UserManual/units.md) を参照。 |
| <span id="DimensionLength">寸法長</span>。 | 整数 |  |  | フィールド `Dimension` を使ってすべてのパーツを指定するか、すべてのパーツを個別に指定する。 |
| <span id="DimensionMass">ディメンションマス</span>。 | 整数 |  |  | Dimension`フィールドを使用してすべてのパーツを指定するか、すべてのパーツを個別に指定する。 |
| <span id="DimensionTime">ディメンションタイム</span>。 | 整数 |  |  | フィールド `Dimension` を使ってすべてのパートを指定するか、すべてのパートを個別に指定する。 |
| <span id="Dimension電流">Dimension電流</span>。 | 整数 |  |  | フィールド `Dimension` を使ってすべてのパートを指定するか、すべてのパートを個別に指定する。 |
| <span id="DimensionThermodynamicTemperature">寸法熱力学温度</span>。 | 整数 |  |  | ThermodynamicTemperatureの次元。フィールド `Dimension` を使ってすべてのパートを指定するか、すべてのパートを個別に指定する。 |
| <span id="DimensionAmountOfSubstance">ディメンション物質量</span>。 | 整数 |  |  | Dimension`フィールドを使用してすべてのパートを指定するか、すべてのパートを個別に指定する。 |
| <span id="DimensionLuminousIntensity">DimensionLuminousIntensity</span>。 | 整数 |  |  | LuminousIntensityの寸法。フィールド `Dimension` を使ってすべての部分を指定するか、すべての部分を個別に指定する。 |
| <span id="DocumentReference">ドキュメント参照</span>。 | テキスト |  |  | プロパティ`の完全な、または公式な定義を持つドキュメントへの参照。参照リスト(JSON) [参照ドキュメント](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)を参照。 |
| <span id="DynamicParameterPropertyCodes">ダイナミックパラメータプロパティコード</span>。 | テキスト一覧 |  |  | 動的プロパティの関数のパラメータであるプロパティのコードのリスト。 プロパティの組み立て](#assembling-properties)を参照してください。 |
| <span id="IsDynamic">イズダイナミック</span>。 | ブーリアン |  |  | デフォルト: `false`. このプロパティが動的プロパティの場合、値はフィールド `DynamicParameterPropertyCodes` で指定されたパラメータに依存します。 プロパティの組み立て](#assembling-properties)を参照してください。 |
| <span id="MaxExclusive">マックスエクスクルーシブ</span>。 | リアル |  |  | 最大許容値、排他的 - 包含値と排他値の両方を記入しないこと |
| <span id="MaxInclusive">マックス・インクルーシブ</span>。 | リアル |  |  | 最大許容値、包含値 - 包含値と排他値の両方を記入しないこと |
| <span id="MinExclusive">MinExclusive</span>。 | リアル |  |  | 最小許容値、排他的 |
| <span id="MinInclusive">ミニインクルーシブ</span>。 | リアル |  |  | 許容最小値（含む |
| <span id="MethodOfMeasurement">測定方法</span>。 | テキスト |  | ✅ | 例："ISO 10077-1に準拠した熱貫流率" |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | 辞書レベルで `UseOwnUri = true` を指定 し た場合には、 Property をグ ロ ーバルに一意に識別す る URI を与え る 必要があ り ます。 |
| <span id="パターン">パターン</span>。 | テキスト |  |  | 許容値を制限するための[XMLスキーマ正規表現](https://www.regular-expressions.info/xml.html) |
| <span id="PhysicalQuantity">物理量</span>。 | テキスト |  | ✅ | プロパティの物理量の名前、例："なし "または "質量" |
| <span id="PropertyValueKind">プロパティ・バリュー・カインド</span>。 | テキスト |  |  | Single` (1つの値。これがデフォルト), `Range` (2つの値), `List` (複数の値), `Complex` (シングル/レンジ/リストのどちらでもない。例えば、IfcActorのようなオブジェクトや、連結されたプロパティの集合体 - [プロパティのアセンブル](#assembling-properties)を参照), `ComplexList` (複合値のリスト). |
| <span id="ReplacedObjectCodes">ReplacedObjectCodes</span>。 | テキスト一覧 |  |  | この `Property` が置き換えるプロパティコードのリスト。 |
| <span id="ReplacingObjectCodes">ReplacingObjectCodes</span>。 | テキスト一覧 |  |  | この `Property` が置き換わるプロパティコードのリスト |
| <span id="RevisionDateUtc">リビジョンデートUtc</span>。 | 日時 |  |  | 日付時刻フォーマット](#datetime-format)を参照。 |
| <span id="RevisionNumber">リビジョン番号</span>。 | 整数 |  |  |  |
| <span id="Status">ステータス</span>。 | テキスト |  |  | プロパティの状態：`Active`（デフォルト）または `Inactive |
| <span id="SubdivisionsOfUse">細分化された用途</span>。 | テキスト一覧 |  | ✅ | 使用地域のリスト 例："US-MT" |
| <span id="TextFormat">テキストフォーマット</span>。 | テキスト |  |  | テキストタイプ（エンコーディング、文字数）のペア エンコーディングは IANA, RFC 2978 の "エンコーディング規格名 "に従って設定される 例："(UTF-8,32)" |
| <span id="Uid">Uid</span>。 | テキスト |  |  | URIだけでは不十分な場合のための一意な識別（ID）。 |
| <span id="VersionDateUtc">バージョン日付Utc</span>。 | 日時 |  |  | デフォルトでは、インポートされた日付が使われます。 日付時刻フォーマット](#datetime-format)を参照してください。 |
| <span id="VersionNumber">バージョン番号</span>。 | 整数 |  |  |  |
| <span id="VisualRepresentationUri">VisualRepresentationUri</span>。 | テキスト |  | ✅ |  |
| <span id="PropertyRelations">プロパティ関係</span>。 | PropertyRelationのリスト |  | ✅ | PropertyRelation](#PropertyRelation) を参照してください。 |
| <span id="AllowedValues">許可された値</span>。 | 許容値のリスト |  | ✅ | プロパティに許可される値のリスト。 注意: boolean型のプロパティには使用しないでください。 AllowedValue](#AllowedValue)のセクションを参照してください。 |

<h3 id="ClassProperty">ClassProperty</h3>

Interim object to assign a `Property` to a `Class` it should describe. Each `Class` can have multiple properties, and each `Property` can be part of many `Classes`, but one `ClassProperty` is always a pair of one `Class` and one `Property`. 

Through `ClassProperty`, one can further specify a 'Property' by defining its unit, property set it should be stored in, and value restrictions when applied to that particular `Class`. For example, a general 'Temperature' can be expressed in Celcius or Fahrenheit and can be any negative or positive value, but when applied to an indoor space, it might be restricted to a range of 5-40 degrees Celcius.   


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|---------------------|----------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span | テキスト |  |  | ClassProperty` の一意な識別コード。 コードバリデーションが適用されます。 コードフォーマット](#code-format) を参照してください。 インポート時に空のままにすると、bSDD はランダムな GUID を生成します。 |
| <span id="PropertyCode">プロパティコード</span>。 | テキスト | ✅\ |  | 同じ `Dictionary` 内にある場合は `Property` への参照。 ⅳ どちらか一方だけが必要で、PropertyCode が使用されている場合は PropertyUri を記入しないでください。 |
| <span id="PropertyUri">プロパティ</span>。 | テキスト | ✅\ |  | PropertyUriが使用されている場合、PropertyCodeは記入しないでください。 |
| <span id="Description">説明</span>。 | テキスト |  | ✅ | クラス固有のプロパティの説明を指定することができます。 省略した場合、プロパティの「一般的な」説明は、該当する場所に表示されます。 |
| <span id="PropertySet">プロパティセット</span>。 | テキスト |  |  | プロパティがIFCデータに配置されるべきセットの名前。 接頭辞'Pset_'は公式IFCのために予約されています。 コードバリデーションが適用されます。詳しくは: [コードフォーマット](#code-format)を参照してください。 詳しくは: [プロパティのアセンブル](#assembling-properties)を参照してください。 |
| <span id="Unit">ユニット</span | テキスト |  |  | 参考文献リスト(json) [単位](https://api.bsdd.buildingsmart.org/api/Unit/v1)を参照。 |
| <span id="PredefinedValue">定義済み値</span>。 | テキスト |  |  | 例："イフックウォール" クラスのプロパティ "IsLoadBearing" の値は "true" になります。 |
| <span id="IsRequired">必須</span>です。 | ブーリアン |  |  | これが `Class` の必須 `Property` であるかどうかを示す。 |
| <span id="IsWritable">書き込み可能</span>。 | ブーリアン |  |  | クラス `` の `プロパティ`` の値を変更できるかどうかを示す。 |
| <span id="MaxExclusive">マックスエクスクルーシブ</span>。 | リアル |  |  | 最大許容値(排他的) `Property`に定義された値を上書きする。 inclusive'と'exclusive'の両方の値を記入してはならない。 |
| <span id="MaxInclusive">マックス・インクルーシブ</span>。 | リアル |  |  | Property`に定義された値よりも優先される。 inclusive'値と'exclusive'値の両方を埋めないでください。 |
| <span id="MinExclusive">MinExclusive</span>。 | リアル |  |  | Property`に定義された値をオーバーライドする。 inclusive'値と'exclusive'値の両方を埋めないでください。 |
| <span id="MinInclusive">ミニインクルーシブ</span>。 | リアル |  |  | Property`に定義された値をオーバーライドする。 inclusive'値と'exclusive'値の両方を記入してはならない。 |
| <span id="パターン">パターン</span>。 | テキスト |  |  | 許 さ れ る 値を制限す る ための [XML Schema 正規表現](https://www.regular-expressions.info/xml.html)。 Property に定義 さ れてい る パ タ ーン を上書き し ます。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | 辞書レベルで `UseOwnUri = true` を指定した場合は、ClassProperty をグローバルに一意に識別する URI を指定する必要があります。 |
| <span id="PropertyType">プロパティタイプ</span>。 | テキスト |  |  | クラス `` の `プロパティ`` の種類: `プロパティ`` (デフォルト) または `依存関係`` (デフォルト) |
| <span id="SortNumber">ソートナンバー</span>。 | 整数 |  |  | この `プロパティ` の `クラス` 内のソート番号。 |
| <span id="Symbol">シンボル</span>。 | テキスト |  |  |  |
| <span id="AllowedValues">許可された値</span>。 | 許容値のリスト |  | ✅ | ClassProperty`に指定できる値のリスト。 Property`に定義されている値を上書きします。 boolean型のプロパティには使用しないでください。 AllowedValue](#AllowedValue)セクションを参照してください。 |
| ~~ExternalPropertyUri~~。 | ~~テキスト |  |  | DEPRECATED - 代わりに `PropertyUri` を使用する。 |

<h3 id="AllowedValue">AllowedValue</h3>

Optional value enumerations that can be listed for `Properties` and `ClassProperties`. For example, a 'Fire Rating' could only have a few allowed values: REI30, REI60, REI90 or REI120.

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="Code">コード</span | テキスト | ✅ |  | Codeは値の一意な識別情報です（最大20文字）。 これは必須で、ほとんどの場合は値と同じです。 値やその説明の翻訳を可能にするために必要です。 Codeのバリデーションが適用されますので、[Code format](#code-format)を参照してください。 |
| <span id="Value">値</span>。 | テキスト | ✅ | ✅ | プロパティが持ち得る値の1つ。例：プロパティが "Color "のような場合、"Green" |
| <span id="Description">説明</span>。 | テキスト |  | ✅ | 値の説明 |
| <span id="Uri">ユリ</span>。 | テキスト |  |  | OwnedUriと重複するため、新モデルバージョンでは非推奨。 |
| <span id="SortNumber">ソートナンバー</span>。 | 整数 |  |  | その値が属する `Property` の値のリストにおけるソート番号。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | 辞書レベルで `UseOwnUri = true` を指定した場合、AllowedValue をグローバルに一意に識別する URI を指定することができる。 |

Note: adding translations of the `AllowedValue` is not supported yet

<h3 id="ClassRelation">ClassRelation</h3>

`Classes` can be linked by relations. There are various types of relations, allowing for the definition of hierarchy, composition, similarity or reference. See section [How to define relations?](#defining-relations)

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelationType">リレーションタイプ</span>。 | テキスト | ✅ |  | HasMaterial`、`HasReference`、`IsEqualTo`、`IsSimilarTo`、`IsParentOf`、`IsChildOf`、`HasPart`、`IsPartOf` のいずれか。 関係の種類](#relation-types) についてもっと読む。 |
| <span id="RelatedClassUri">RelatedClassUri</span>。 | テキスト | ✅ |  | 関連する `Class` の完全な URI。同じ `Dictionary` でも、異なる `Dictionary` でもよい。 例: https://identifier.buildingsmart.org/uri/etim/etim/8.0/class/EC002987 |
| <span id="RelatedClassName">関連クラス名</span>。 | テキスト |  |  |  |
| <span id="Fraction">端数</span>。 | リアル |  |  | HasMaterial`関係にのみ適用される。 オプションで、関係を所有するクラスに適用される総量(例: 体積または重量)の端数を提供する。 クラス/関係タイプごとの端数の合計は1でなければならない。 [IfcMaterialConstituent](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterialConstituent.htm)のFractionに類似している。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | ディクショナリ・レベルで `UseOwnUri = true` を指定した場合は、クラス・リレーションをグローバルに一意に識別する URI を指定する必要があります。 |

<h3 id="PropertyRelation">PropertyRelation</h3>

Analogous to `ClassRelations` but between `Properties`.

| フィールド | データ型 | 必要ですか？ | 翻訳可能か？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelatedPropertyName">関連プロパティ名</span>。 | テキスト |  |  | 関連する `Property` の名前。 |
| <span id="RelatedPropertyUri">RelatedPropertyUri</span>。 | テキスト | ✅ |  | 関連する `Property` の完全な URI。 同じ `Dictionary` または別の `Dictionary` を指定することができる。 |
| <span id="RelationType">リレーションタイプ</span>。 | テキスト | ✅ |  | HasReference`、`IsEqualTo`、`IsSimilarTo`、~~IsParentOf、IsChildOf、HasPart~~のいずれか。 Relation types](#relation-types)についてもっと読む。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | ディクショナリレベルで `UseOwnUri = true` を指定した場合、PropertyRelation をグローバルに一意に識別する URI を与えなければなりません。 |

---

<h2 id="additional-explanations">Additional explanations</h2>

<h3 id="code-format">Code format</h3>

(from April 2024) All codes support diacritics, whitespace, dots, commas, dashes, round brackets (parentheses) underscores and numbers. Not allowed are special characters: ```"#%/\:`{}[]|;<>?~```. Codes are not case-sensitive, and we recommend using small-caps only. 

Some examples of valid codes are: "bs-agri", "apple", "éÄą _- (Д開発,...żź)".

Codes need to be unique within the same data dictionary and are used to generate URIs.

Some codes might be reserved, for example, the IFC standard reserves the codes starting with a prefix 'Ifc' and 'Pset'. 

<h3 id="class-types">Class types</h3>

Each class must have a specific type. Below is the explanation of what each type means, according to ISO 12006-3:
* `Class` - description of a set of objects that share the same characteristics <sup>[ISO12006-3,3.7]</sup>. This is the most common type in bSDD. (Example: wall, space)
* `GroupOfProperties` - collection enabling the properties to be prearranged or organized <sup>[ISO12006-3,3.14]</sup>. For example, 'environmental properties'. See [assembling properties](#assembling-properties).
* `Material` - a physical substance that things can be made from (Example: steel, glass)
* `AlternativeUse` - type to be used if no other type fits the needs.<sup>[ISO12006-3,3.1]</sup>.
   * Be aware that most software implementations disregard this class type, as it is not straightforward to interpret.
* **DEPRECATED** ~~ReferenceDocument - a publication that is consulted to find specific information, particularly in a technical or scientific dictionary. <sup>[ISO12006-3,3.18]</sup>. A reference document can be associated with any data present in a data dictionary.~~
  * In bSDD we have a global list of [reference documents](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1), which includes the most common standards that can be used as reference. This is to avoid having duplicate references with different naming. If you don't find the reference you are looking for, and think it should be added to the list - let us know: [CONTACT FORM](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).
* **DEPRECATED**  ~~ComposedProperty - (...) corresponding to a feature needing multiple properties to be defined. <sup>[ISO12006-3,3.8]</sup>.~~
  * ~~Example: To describe the characteristic "concrete facing quality", it is mandatory to describe 3 properties: concrete planarity, concrete hue, and concrete texture.~~
  * Use `GroupOfProperties` instead.

<h3 id="defining-relations">Defining relations</h3>

`ParentClassCode` - `Class`es within the same dictionary can be organized in a tree-like hierarchy structure. For example: “IfcCurtainWall” is a more
bSDDの用語では、"IfcWall "は、"IfcWall "の特定のクラスである。**親**「このような特殊化関係を定義するには`ParentClassCode`属性を子オブジェクトに与える。

`ClassRelation` and `PropertyRelation`- use those to link your concepts with each other. Relations allow us to define parent-child links also with other dictionaries. Apart from specialization, you can also define other types of relations, such as decomposition (`HasPart` type, see the list of possible types: [Relation types](#relation-types)).

`RelatedIfcEntityNamesList` - IFC is a top-level schema (foundation classes) used for exchanging information between software. Because of that, the bSDD provides a special way to relate your class to IFC. Use `RelatedIfcEntityNamesList` to show which entities from IFC you are referring to or extending. For example, “Signaling LED diode” relates to “IfcLamp” from IFC. `RelatedIfcEntityNamesList` can be used by bSDD-related tools to filter the list of possible classes to a particular IFC category.

<h3 id="relation-types">Relation types</h3>

`Properties` and `Classes` can be related to each other. Each relation must have a specific type to allow software to interpret it. Below is an explanation of what each type means:
* <span id='IsEqualTo'>`IsEqualTo`</span> - if two concepts are unequivocal and have the same name, code, definition and description. Classes also need to share the same class properties. It is quite rare for concepts to be equal. An example of usage is when a concept doesn't have an official translation, but someone defines a new dictionary with that concept in a new language and wants to say it is exactly the same as the original. (We always recommend proposing translations and improvements to the original data dictionaries instead of building duplicate ones). 
* <span id='IsSimilarTo'>`IsSimilarTo`</span> - if two concepts are almost equal but differ by name, code, definition, description or set of class properties. This is a very common relationship type. Used, for example, to say that 'IfcWall' is a similar concept to 'Wall System' from CCI. The downside of such a relation is that it doesn't inform on the level of similarity – is it slightly differing by the wording of the definition, or is the difference huge?
* <span id='HasReference'>`HasReference`</span> - if two concepts relate to each other, but other relation types do not apply. For example, "wall lamp" (or "sconce") is referencing a wall, even though those are different concepts and there is no hierarchy between them.
* **DEPRECATED** ~~IsSynonymOf - if two concepts are unequivocal but have a different name.~~

Only applicable to classes (not properties):
* <span id='IsChildOf'>`IsChildOf`</span> - specialisation relation. The equivalent of the "subtype" relationship <sup>[ISO12006-3, F3.1]</sup>. For example: "Electrical motor" and a "Combustion motor" are children (subtypes) of the generic concept "Motor".
* <span id='IsParentOf'>`IsParentOf`</span> - the opposite relation to `IsChildOf`.
* <span id='HasPart'>`HasPart`</span> - composition relation. For example, an electric motor can be composed of elements such as stators, rotors, etc. <sup>[ISO12006-3, F3.2]</sup>.
* <span id='IsPartOf'>`IsPartOf`</span> - reverse of `HasPart`.
* <span id='HasMaterial'>`HasMaterial`</span> - a class that can be associated with a particular material. For example: "Steel Beam" could be related to the material "Steel".

<h3 id="datetime-format">DateTime format</h3>

The date-time format according to the ISO 8601 series should be used: `YYYY-MM-DDThh:mm:ssTZD`. Import allows both: `2023-05-10`, `2023-05-10T15:10:12Z` and `2023-05-10T15:10:12+02:00`.

<h3 id="property-inheritance">Property inheritance</h3>

* Parent `Class` → child `Class`  
子供`Class`は親からプロパティを継承しない。`Class`子クラスにも親クラスのプロパティを持たせたい場合は、インポートファイルで意図的に指定する必要がある。  
例えば[IfcWall](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall)の親クラスである。[IfcWall標準ケース](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall標準ケース)その一方で[IfcWall](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall)を持つ。[音響評価](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall/prop/Pset_WallCommon/AcousticRating), the [IfcWallStandardCase](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWallStandardCase)それはない。

* `Property` → `ClassProperty`  
`ClassProperty`は一般的な`Property`特定の`Class`プロパティの属性、例えば`AllowedValue`と最小/最大制限は、デフォルトで次のように渡されます。`ClassProperty`の値である。`ClassProperty`原点に影響を与えることなく変更できる`Property`.  
例えば[高さ](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/prop/height)アップル "クラスに適用する場合、その上限は100cmとなる。[アップルハイト](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/class/apple/prop/SizeSet/height)下限は25cm。 

<h3 id="latest-version">Latest version</h3>

In bSDD, all resources get a unique identifier - URI. The URI, among other information, contains codes of the organisation, the dictionary and the version number, for example .../uri/bs-agri/fruitvegs/**1.0.0**/class/fruit
特定のリソースを参照したいが、バージョンがよくわからない場合や、 常に最新のバージョンを参照したい場合には、"latest" 機能を実装しました。 これにより、バージョン番号の代わりに "latest" を使用することが可能になり、 bSDD は、そのリソースを含む最新のアクティブバージョンまたは プレビューバージョンへのリンクを解決します： 
.../uri/bs-agri/fruitvegs/**latest**/クラス/フルーツ。 

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/latest_example.jpg" alt="bSDD latest" style="width: 750px"/>

Try it out:
https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/latest/class/fruit

⚠️ The "latest" points to the most recent resource, meaning that it will change once a new version is present. Use with caution as it is not an immutable URI, and the content can change. For contractual agreements, we suggest using specific version numbers.

<h3 id="assembling-properties">Assembling properties</h3>

**Groups of Properties** (use `Class`.`ClassType`:`GroupOfProperties`) "collection enabling the properties to be prearranged or organized" <sup>[ISO12006-3,3.14]</sup>. In bSDD, implemented as a Type of Class meant to group multiple Properties.

Use Group of Properties to organize properties in a data dictionary.

Example: _'[Global Warming Potential](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/class/GlobalWarmingPotential)' class from '[LCA indicators and modules](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0)' groups four properties: '[...total](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total)', '[...biogenic](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_biogenic)', '[...fossil fuels](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_fossil)' and '[...land use...](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_luluc)'._

**Sets of properties** (use `ClassProperty`.`PropertySet`) - a concept from the IFC standard for grouping properties. In bSDD represented as a text field defined for Class Property, telling in which set this Class Property should appear when serialised to IFC data. 
  * A Property Set, as defined in ISO 16739-1, is a group of properties, but a group of properties is not necessarily a Property Set.
  * A property can be a member of several groups of properties. A class property cannot be a member of several Property Sets.
  * The prefix 'Pset_' is only reserved for the official IFC.

Use Property Set to define where to place a property in an IFC dataset.

Example: _A property 'Concrete Cover' of 'IfcWall' is located in property set: 'Pset_ConcreteElementGeneral'._

**Connected properties** (use `Property`.`ConnectedPropertyCodes`) "List of properties connected to the current property. The connection can be a specialization or a dependency." <sub>[ISO12006-3, 5.3.29]</sub> 

Use Connected Properties if the value of one property depends on the value of another property.

Example: _The property ['Global Warming Potential - total' (GWP)](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total) should be defined for each phase of the life cycle of a product. Defining the property separately for each phase (GWP_A1, GWP_A2, ...) is not desired. Instead, it is connected to another property - '[information module (PHASE)](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/information_module)', taking 18 possible values (A1, A2, C3...). To interpret the meaning of GWP value, one should look at pairs of values: {GWP=1.0, PHASE=A1}, {GWP=15.0, PHASE=A3}, etc. _

⚠️ This feature comes from the ISO standard but is rarely supported by software implementation. The IFC also doesn't support multiple properties with the same name under one property set. Consider avoiding Connected Properties to make the data dictionary more accessible.

**Dynamic properties** (use `Property`.`IsDynamic` and .`DynamicParameterPropertyCodes`) "properties which are parameters of the function for a dynamic property" <sub>[ISO23386, 5.3.29]</sub>. In other words, the value of a dynamic property is dependent on the values of properties specified in `DynamicParameterPropertyCodes`. There is no field in bSDD to define the exact equation of the formula in a machine-interpretable form. 

Use Dynamic Properties to tell which other properties influence the value of the particular property.

Example: _The 'Area' of a wall depends on its 'Height' and 'Length', following the formula: A = H * L._

⚠️ This feature comes from the ISO standard but is rarely supported by software implementation. Consider avoiding Dynamic Properties to make the data dictionary more accessible.

<h3 id="restricting-property-values">Restricting property values</h3>

🚧 TO BE DEVELOPED 🚧
`AllowedValues`...

`Min/MaxInc/Exclusive`...

`Pattern`...

<h3 id="identifying-bsdd-resources">Identifying bSDD resources</h3>

🚧 TO BE DEVELOPED 🚧
`URI`... bSDDまたは外部で生成可能。

`Code`...  See section [Code format](#code-format).

`UID`(GUID)...

<h3 id="specifying-units">Specifying units</h3>

🚧 TO BE DEVELOPED 🚧
`Unit(s)`...

`Dimension`...

`PhysicalQuantity`...

<h3 id="double-square-bracket-links">Double square bracket links</h3>
It is possible to reference other resources from the same dictionary using double square brackets, and the platform will replace the brackets with hyperlinks pointing to that resource. In cases where the same code exists for both class and property, the hyperlink will point to the class. If the code is not found, the square brackets are omitted. The API returns the definition with square brackets. 

<h2 id="notifications">Notifications</h2>

**2023-07 - Important notification:**

> As we're continuously improving bSDD, we've updated all identifiers: the dash between dictionary code and dictionary version has been replaced by a slash, Example:
>  https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs-1.0.0/class/apple は https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/class/apple となります。
> 
> 少なくとも4ヶ月間は、辞書コードとバージョンの間にダッシュを使用したデータの供給と検索をサポートします。 しかし、新しい形式の識別子のみがbSDD APIによって返されることに注意してください。

**2022-08 - 重要なお知らせ**

> bSDDは、"http://identifier.buildingsmart.org "から始まる識別子（別名 "URI"）を、"https://identifier.buildingsmart.org"（"http "から "https"）に移行中である。これは、これらの識別子をハイパーリンクとしても使いやすくするためである。
> 
> 古い "http "識別子を使用するサポートは、まもなく非推奨となる！

📢 最新の技術アップデートについては、専用フォーラムのトピック（https://forums.buildingsmart.org/t/bsdd-tech-updates/4889）をご覧ください。
