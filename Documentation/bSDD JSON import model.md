<h2 id="table-of-content">Table of contents</h2>

* [データモデル](#data-model)
* [JSONフォーマット](#json-format)
* [フィールド一覧](#list-of-fields)
    * [辞書](#Dictionary)  
    * [クラス](#Class)  
    * [プロパティ](#Property)  
    * [クラスプロパティ](#ClassProperty)  
    * [クラス関係](#ClassRelation)  
    * [許容値](#AllowedValue)  
    * [プロパティ関係](#PropertyRelation)  
* [補足説明](#additional-explanations)
* [お知らせ](#notifications)


<h2 id="data-model">Data model</h2>

bSDDは、独立した組織によって発行されたデータ辞書（データ辞書とは何かについては以下をお読みください）の配布を容易にするためのサービスです。 下の図は、bSDDの背後にある簡略化されたデータモデルを示しています：

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_model.png" alt="bSDD entity diagram" style="width: 650px"/>

上記のコンセプトの使用例をご覧ください：[bSDDデータ例](https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png):
<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png" alt="bSDD entity diagram" style="width: 700px"/>

デモンストレーション用の辞書もあります：[「果物と野菜](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.1).

📢 最新の技術的なアップデートについては、専用のフォーラムトピックでお読みください：[https://forums.buildingsmart.org/t/bsdd-tech-updates/4889](https://forums.buildingsmart.org/t/bsdd-tech-updates/4889)

<h2 id="json-format">JSON format</h2>

buildingSMARTデータディクショナリのデータは、JSONファイルで納品することができます。 JSONとExcelのテンプレートは、以下のリンクからダウンロードできます。[/モデル/インポートモデル](https://github.com/buildingSMART/bSDD/tree/master/Model/Import%20Model).

リンクをクリックすると、以下のコードのリストが表示されます。[国々](https://api.bsdd.buildingsmart.org/api/Country/v1),[言語](https://api.bsdd.buildingsmart.org/api/Language/v1),[単位](https://api.bsdd.buildingsmart.org/api/Unit/v1),[参考文献](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)そして[ifcクラス](https://api.bsdd.buildingsmart.org/api/Dictionary/v2/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3).
If you think there are reference documents missing, please let us know by [posting an issue](https://github.com/buildingSMART/bSDD/issues). All values in JSON must be strings captured in double quotes, including for numeric Example and AllowedValue fields.

JSONに馴染みのない方は、以下を読むことをお勧めします。[JSON入門](https://javaee.github.io/tutorial/jsonp001.html)JSONは、コンピュータ・システムがデータを交換するためのフォーマットであることに注意してください。 辞書データがコンピュータ・システムにある場合は、システムにJSONを作成させるのが最善です。

<h2 id="list-of-fields">List of fields</h2>

NBデフォルト値は、フィールドが指定されていない場合にのみ適用される。 フィールド値に "null "を指定した場合、デフォルト値は適用されない。 すべてのフィールドに "null "を指定できるわけではないことに注意。

<h3 id="Dictionary">Dictionary</h3>

`Data dictionary` - '_データの意味、他のデータとの関係、出所、使用方法、形式など、データに関する情報を一元的に保管する場所。_iso23386]。_メタデータ・データベース_ISO12006-3]。`Dictionary`(以前は`domain`で構成されている。`Classes`(以前は`classifications`そして`Properties`それは互いに関連し合っているか、あるいは他のものと関連している可能性がある。`Dictionaries`それぞれ`Dictionary`オブジェクトには、そのオブジェクトに関する一般的なメタデータが含まれている。

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|------------------|------------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="OrganizationCode">組織コード</span>。 | テキスト | ✅ |  | bSDD に登録したときに受け取った組織のコード。 あなたの組織がまだコードを持っていない場合は、[bSDD User Helpdesk](https://bsi-technicalservices.atlassian.net/servicedesk/customer/portal/3/group/4/create/25) でリクエストしてください。 すべての URI リンクに表示されるため、コードはなるべく短い方がよいでしょう。 許容される文字については、[コードフォーマット](#code-format) のセクションを参照してください。 このコードは数字で始まることはできません。 コード例: "ifc". |
| <span id="DictionaryCode">辞書コード</span>。 | テキスト | ✅ |  | 辞書のコード、できれば短く。 例："ifc"。 コードフォーマット](#code-format)の項を参照のこと。 |
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

`Class` - '_同じ特徴を共有するオブジェクトの集合の記述。_iso23386]。`Class`は、物体（例：「壁」、「窓」）、抽象概念（例：「時間」、「部屋」）、またはプロセス（例：「設置」、「分解」）である。


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|---------------------------|--------------------------------|-------------|-----------------|--------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span | テキスト | ✅ |  | 例："abc-00123-01 "または "SpecialWall"。 コード検証が適用される、参照：[コードフォーマット](#code-format)。 接頭辞'Ifc'は、IFC標準のために予約されている。 |
| <span id="Name">名前</span>。 | テキスト | ✅ | ✅ | クラス名、例："IfcCurtainWall" |
| <span id="ClassType">クラスタイプ</span>。 | テキスト | ✅ |  | Class` 型、`Material` 型、`GroupOfProperties` 型、`AlternativeUse` 型のいずれかを指定する必要がある。 クラス型](#class-types) について詳しくはこちらを参照。 指定しない場合、デフォルトで `Class` 型が使用される。 ReferenceDocument` 型、`ComposedProperty` 型、`Dictionary` 型は非推奨となり、アップロード時に使用することはできないが、移行期間中は API の結果に表示されることがある。 |
| <span id="Definition">定義</span>。 | テキスト |  | ✅ | クラス`の定義、意味的な意味を説明する。 ISOに従った必須フィールド。 二重四角括弧リンク](#double-square-bracket-links)をサポートする。 |
| <span id="Description">説明</span>。 | テキスト |  | ✅ | 補足説明のための追加フィールド。 定義_が規格に由来し、さらに説明が必要な場合にのみ使用してください。 |
| <span id="ParentClassCode">親クラスコード</span>。 | テキスト |  |  | 親クラス `Class` への参照。 このフィールドのIDは、配信されたデータの中に存在しなければなりません。 例: "ifc-00123-00" リレーションシップを定義するには](#defining-relations)を参照してください。 |
| <span id="RelatedIfcEntityNamesList">関連Ifcエンティティ名リスト</span>。 | テキスト一覧 |  |  | この `Class` の表現として使用する IFC クラスのコード。 例: ['IfcWall']. bSDD API [ifc classs](https://api.bsdd.buildingsmart.org/api/Dictionary/v3/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3%2F) を参照。 [リレーションシップの定義方法](#defining-relations) を参照。 |
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

`Property` - '_アイテムに固有の、あるいは後天的な特徴`Class`例：熱効率、ヒートフロー、色。_の代入が必要である[ISO23386]。`Properties`への`Classes`は中間[クラスプロパティ](#ClassProperty)オブジェクトがある。 


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
| <span id="ReplacingObjectCodes">ReplacingObjectCodes</span>。 | テキスト一覧 |  |  | この `Property` は次のように置き換えられる。 |
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

を割り当てる中間オブジェクト。`Property`への`Class`それぞれ`Class`は複数のプロパティを持つことができ`Property`多くの`Classes`しかし、1つだけ`ClassProperty`は常に`Class`そして`Property`. 

を通して`ClassProperty`を定義することによって、さらに「Property」を指定することができます。`Class`例えば、一般的な「温度」は摂氏または華氏で表すことができ、負の値でも正の値でも構わないが、室内空間に適用する場合、摂氏5～40度の範囲に制限されることがある。   


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|---------------------|----------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span | テキスト |  |  | ClassProperty` の一意な識別コード。 コードバリデーションが適用されます。 コードフォーマット](#code-format) を参照してください。 インポート時に空のままにすると、bSDD はランダムな GUID を生成します。 |
| <span id="PropertyCode">プロパティコード</span>。 | テキスト | ✅\ |  | 同じ `Dictionary` 内にある場合は `Property` への参照。 ⅳ どちらか一方だけが必要で、PropertyCode が使用されている場合は PropertyUri を記入しないでください。 |
| <span id="PropertyUri">プロパティ</span>。 | テキスト | ✅\ |  | PropertyUriが使用されている場合、PropertyCodeは記入しないでください。 |
| <span id="Description">説明</span>。 | テキスト |  | ✅ | クラス固有のプロパティの説明を指定することができます。 省略した場合、プロパティの「一般的な」説明は、該当する場所に表示されます。 |
| <span id="PropertySet">プロパティセット</span>。 | テキスト |  |  | プロパティがIFCデータに配置されるべきセットの名前。 接頭辞'Pset_'は公式IFCのために予約されています。 コードバリデーションが適用されます。詳しくは: [コードフォーマット](#code-format)を参照してください。 詳しくは: [プロパティのアセンブル](#assembling-properties)を参照してください。 |
| <span id="Unit">ユニット</span | テキスト |  |  | 参考文献リスト(json) [単位](https://api.bsdd.buildingsmart.org/api/Unit/v1)を参照。 |
| <span id="PredefinedValue">定義済み値</span>。 | テキスト |  |  | 例："IfcWall" クラスのプロパティ "IsLoadBearing" の値は "true" になります。 |
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

オプションの列挙値。`Properties`そして`ClassProperties`例えば、「耐火等級」の許容値は、REI30、REI60、REI90、REI120のいずれかである。

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="Code">コード</span | テキスト | ✅ |  | Codeは値の一意な識別情報です（最大20文字）。 これは必須で、ほとんどの場合は値と同じです。 値やその説明の翻訳を可能にするために必要です。 Codeのバリデーションが適用されますので、[Code format](#code-format)を参照してください。 |
| <span id="Value">バリュー</span>。 | テキスト | ✅ | ✅ | プロパティが持ち得る値の1つ。例：プロパティが "Color "のような場合、"Green" |
| <span id="Description">説明</span>。 | テキスト |  | ✅ | 値の説明 |
| <span id="Uri">ユリ</span>。 | テキスト |  |  | OwnedUriと重複するため、新モデルバージョンでは非推奨。 |
| <span id="SortNumber">ソートナンバー</span>。 | 整数 |  |  | その値が属する `Property` の値のリストにおけるソート番号。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | 辞書レベルで `UseOwnUri = true` を指定した場合、AllowedValue をグローバルに一意に識別する URI を指定することができる。 |

Note: adding translations of the `AllowedValue` is not supported yet

<h3 id="ClassRelation">ClassRelation</h3>

`Classes`リレーションには様々な種類があり、階層、合成、類似、参照の定義が可能である。 を参照のこと。[関係をどう定義するか？](#defining-relations)

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelationType">リレーションタイプ</span>。 | テキスト | ✅ |  | HasMaterial`、`HasReference`、`IsEqualTo`、`IsSimilarTo`、`IsParentOf`、`IsChildOf`、`HasPart`、`IsPartOf` のいずれか。 関係の種類](#relation-types) についてもっと読む。 |
| <span id="RelatedClassUri">RelatedClassUri</span>。 | テキスト | ✅ |  | 関連する `Class` の完全な URI。同じ `Dictionary` でも、異なる `Dictionary` でもよい。 例: https://identifier.buildingsmart.org/uri/etim/etim/8.0/class/EC002987 |
| <span id="RelatedClassName">関連クラス名</span>。 | テキスト |  |  |  |
| <span id="Fraction">端数</span>。 | リアル |  |  | HasMaterial`関係にのみ適用される。 オプションで、関係を所有するクラスに適用される総量(例: 体積または重量)の端数を提供する。 クラス/関係タイプごとの端数の合計は1でなければならない。 [IfcMaterialConstituent](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterialConstituent.htm)のFractionに類似している。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | ディクショナリ・レベルで `UseOwnUri = true` を指定した場合は、クラス・リレーションをグローバルに一意に識別する URI を指定する必要があります。 |

<h3 id="PropertyRelation">PropertyRelation</h3>

に似ている。`ClassRelations`しかし`Properties`.

| フィールド | データ型 | 必要ですか？ | 翻訳可能か？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelatedPropertyName">関連プロパティ名</span>。 | テキスト |  |  | 関連する `Property` の名前。 |
| <span id="RelatedPropertyUri">RelatedPropertyUri</span>。 | テキスト | ✅ |  | 関連する `Property` の完全な URI。 同じ `Dictionary` または別の `Dictionary` を指定することができる。 |
| <span id="RelationType">リレーションタイプ</span>。 | テキスト | ✅ |  | HasReference`、`IsEqualTo`、`IsSimilarTo`、~~IsParentOf、IsChildOf、HasPart~~のいずれか。 Relation types](#relation-types)についてもっと読む。 |
| <span id="OwnedUri">OwnedUri</span>。 | テキスト |  |  | ディクショナリレベルで `UseOwnUri = true` を指定した場合、PropertyRelation をグローバルに一意に識別する URI を与えなければなりません。 |

---

<h2 id="additional-explanations">Additional explanations</h2>

<h3 id="code-format">Code format</h3>

(2024年4月以降) すべてのコードで、発音区別符号、空白、ドット、コンマ、ダッシュ、丸括弧、アンダースコア、数字をサポートしています。 特殊文字は使用できません：```"#%/\:`{}[]|;<>?~```コードは大文字と小文字を区別しません。 

有効なコードの例としては、"bs-agri"、"apple"、"éÄą _- (Д開発,...żź) "などがある。

コードは同じデータ辞書内で一意である必要があり、URIを生成するために使用される。

例えば、IFC規格では、接頭辞'Ifc'と'Pset'で始まるコードを予約している。 

<h3 id="class-types">Class types</h3>

以下は、ISO 12006-3に従った、各タイプの意味の説明である：
* `Class` - 同じ特徴を共有するオブジェクトの集合の記述<sup>[ISO12006-3,3.7] 。</sup>bSDDで最も一般的なタイプです。 例：壁、スペース
* `GroupOfProperties` - コレクションを使用すると、プロパティを事前に配置または整理することができます。<sup>[ISO12006-3,3.14] 。</sup>例えば、「環境特性」。[組み立て特性](#assembling-properties).
* `Material` - 物を作ることができる物理的な物質（例：鋼鉄、ガラス）
* `AlternativeUse` - 他の型がニーズに合わない場合に使用される。<sup>[iso12006-3,3.1]。</sup>.
   * ほとんどのソフトウェア実装では、このクラス型を無視する。
* **廃止**~~参考文献 - 特定の情報を見つけるために参照される出版物で、特に技術的または科学的な辞書。<sup>[ISO12006-3,3.18] 。</sup>参照文書は、データ辞書に存在するあらゆるデータと関連付けることができる。
  * bSDDでは、グローバルなリストとして[参考文献](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)もしお探しの規格が見つからず、リストに加えるべきだとお考えでしたら、ぜひお知らせください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).
* **廃止**~~ComposedProperty - (...) 複数のプロパティを定義する必要があるフィーチャーに対応します。<sup>[ISO12006-3,3.8]。</sup>.~~
  * ~~例："コンクリートの面構え "という特徴を表現するためには、コンクリートの平面性、コンクリートの色相、コンクリートの質感という3つの特性を表現する必要がある。
  * 用途`GroupOfProperties`その代わりだ。

<h3 id="defining-relations">Defining relations</h3>

`ParentClassCode` - `Class`例えば、"IfcCurtainWall "は、"IfcCurtainWall "よりもさらに階層的な構造である。
specific class of “IfcWall”. In bSDD terminology, we say that “IfcWall” is a **parent of** “IfcCurtainWall”. To define such specialization relation, use the `ParentClassCode` attribute on the child object.

`ClassRelation`そして`PropertyRelation`- 関係によって、他の辞書との親子関係も定義できます。 特殊化とは別に、分解 (`HasPart`タイプについては、可能なタイプのリストを参照のこと：[関係タイプ](#relation-types)).

`RelatedIfcEntityNamesList` - IFCは、ソフトウェア間で情報を交換するために使用されるトップレベルのスキーマ（基礎クラス）です。 そのため、bSDDはクラスをIFCに関連付ける特別な方法を提供します。`RelatedIfcEntityNamesList`例えば、"Signaling LED diode "は、IFCの "IfcLamp "に関連しています。`RelatedIfcEntityNamesList`は、bSDD 関連のツールで、可能なクラスのリストを特定の IFC カテゴリにフィルタリングするために使用できます。

<h3 id="relation-types">Relation types</h3>

`Properties`そして`Classes`各関係は、ソフトウェアがそれを解釈できるように、特定の型を持たなければならない。 以下に、各型の意味を説明する：
* <span id='IsEqualTo'>`IsEqualTo`</span> - 2つの概念が明確で、同じ名前、コード、定義、説明を持っている場合。 クラスはまた、同じクラスプロパティを共有する必要があります。 概念が等しいことは非常にまれです。 使用例としては、ある概念が公式な翻訳を持っていないにもかかわらず、誰かが新しい言語でその概念を持つ新しい辞書を定義し、それがオリジナルとまったく同じであると言いたい場合です（私たちは常に、重複する辞書を構築する代わりに、オリジナルのデータ辞書に翻訳や改良を提案することを推奨しています）。 
* <span id='IsSimilarTo'>`IsSimilarTo`</span> - 2つの概念がほぼ等しいが、名前、コード、定義、説明、またはクラスプロパティのセットによって異なる場合。 これは非常に一般的な関係タイプです。 例えば、「IfcWall」がCCIの「Wall System」と類似した概念であることを言うために使用されます。 このような関係の欠点は、類似性のレベルが通知されないことです - それは定義の文言によってわずかに異なっているか、または大きな違いですか？
* <span id='HasReference'>`HasReference`</span> - 例えば、"wall lamp"（または "sconce"）は、異なる概念であり、それらの間に階層がないにもかかわらず、壁を参照している。
* **廃止**~~IsSynonymOf（同義語） - 2つの概念が明白であるが、名前が異なる場合。

クラスにのみ適用される（プロパティには適用されない）：
* <span id='IsChildOf'>`IsChildOf`</span> - subtype "関係に相当する。<sup>[ISO12006-3, F3.1]。</sup>例えば、「電気モーター」と「燃焼モーター」は、一般概念「モーター」の子（サブタイプ）である。
* <span id='IsParentOf'>`IsParentOf`</span> - とは逆の関係にある。`IsChildOf`.
* <span id='HasPart'>`HasPart`</span> - 例えば、電気モーターはステーター、ローターなどの要素で構成される。<sup>[ISO12006-3, F3.2]。</sup>.
* <span id='IsPartOf'>`IsPartOf`</span> - 逆`HasPart`.
* <span id='HasMaterial'>`HasMaterial`</span> - 特定の材料に関連付けられるクラス。 例えば、"Steel Beam "は材料 "Steel "に関連付けられる。

<h3 id="datetime-format">DateTime format</h3>

ISO 8601シリーズに準拠した日付時刻形式を使用すること：`YYYY-MM-DDThh:mm:ssTZD`インポートはその両方を可能にする：`2023-05-10`,`2023-05-10T15:10:12Z`そして`2023-05-10T15:10:12+02:00`.

<h3 id="property-inheritance">Property inheritance</h3>

* 親`Class`→ 子供`Class`  
The child `Class` does not inherit properties from the parent `Class`. If authors want child classes to also have properties of parent classes, they should specify them intentionally in import files.  
For example, the [IfcWall](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall) is a parent class of [IfcWallStandardCase](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWallStandardCase). While [IfcWall](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall) has the property [AcousticRating](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall/prop/Pset_WallCommon/AcousticRating), the [IfcWallStandardCase](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWallStandardCase) doesn't.

* `Property`→`ClassProperty`  
`ClassProperty` is an instantiation of general `Property` for a particular `Class`. The attributes of a property, such as `AllowedValue` and min/max restrictions,  are by default passed to `ClassProperty`. The values of the `ClassProperty` can be modified without influencing the origin `Property`.  
For example, the [Height](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/prop/height) has an upper limit of 100 cm. When applied to the "Apple" class, the [Apple-Height](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/class/apple/prop/SizeSet/height) has a lower limit - 25cm. 

<h3 id="latest-version">Latest version</h3>

bSDDでは、すべてのリソースは一意な識別子であるURIを持つ。 URIは、他の情報の中で、組織のコード、辞書、およびバージョン番号を含み、例えば.../uri/bs-agri/fruitvegs/フルーツヴェッグスのようになる。**1.0.0**/クラス/フルーツ
If you want to reference specific resources but are not sure of the version or want to always point to the most recent version, we implemented the "latest" feature. Now, it is possible to use "latest" instead of a version number, and bSDD will resolve the link to the latest active or preview version containing that resource: 
.../uri/bs-agri/fruitvegs/**latest**/class/fruit. 

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/latest_example.jpg" alt="bSDD latest" style="width: 750px"/>

お試しあれ：
https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/latest/class/fruit

⚠️ "latest "は最新のリソースを指し、新しいバージョンが存在すると変更されることを意味する。不変のURIではなく、内容が変更される可能性があるため、注意して使用すること。 契約上の合意については、特定のバージョン番号を使用することを推奨する。

<h3 id="assembling-properties">Assembling properties</h3>

**物件グループ**使用`Class`.`ClassType`:`GroupOfProperties`) "プロパティを事前に配置または整理することを可能にするコレクション"<sup>[ISO12006-3,3.14] 。</sup>bSDD では、複数のプロパティをグループ化するための クラスの一種として実装されている。

データ辞書内のプロパティを整理するには、プロパティのグループを使用します。

例_'[地球温暖化の可能性](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/class/GlobalWarmingPotential)クラス[LCA指標とモジュール](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0)'は4つのプロパティをグループ化している。[...合計](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total)', '[...バイオジェニック](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_biogenic)', '[...化石燃料](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_fossil)'と'[...土地利用...](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_luluc)'._

**プロパティのセット**使用`ClassProperty`.`PropertySet`bSDD では、クラス・プロパティに定義されたテキスト・フィールドとして表現され、IFC データにシリアル化されたときに、このクラス・プロパティがどのセットで表示されるかを示します。 
  * ISO 16739-1で定義されるプロパティセットはプロパティのグループであるが、プロパティのグループは必ずしもプロパティセットではない。
  * プロパティは、複数のプロパティ・グループのメンバになることができます。 クラス・プロパティは、複数のプロパティ・セットのメンバになることはできません。
  * 接頭辞'Pset_'は公式IFCにのみ予約されている。

プロパティセットを使用して、IFC データセットのどこにプロパティを配置するかを定義します。

例_IfcWall」のプロパティ「Concrete Cover」は、プロパティセット「Pset_ConcreteElementGeneral」にあります。_

**接続物件**使用`Property`.`ConnectedPropertyCodes`) "現在のプロパティに接続されているプロパティのリスト。 接続は、特殊化または依存関係であることができます。"<sub>[ISO12006-3, 5.3.29]。</sub> 

あるプロパティの値が他のプロパティの値に依存する場合は、Connected Propertiesを使用します。

例[地球温暖化係数-合計」（GWP）](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total)各フェーズ（GWP_A1、GWP_A2、...）ごとに個別に定義することは望まれない。 その代わりに、このプロパティは、別のプロパティ（'[情報モジュール（PHASE）](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/information_module)GWP値の意味を解釈するには、{GWP=1.0, PHASE=A1}、{GWP=15.0, PHASE=A3}などの値のペアを見る必要がある。

⚠️ この機能はISO標準に由来していますが、ソフトウェア実装でサポートされていることはほとんどありません。 また、IFCは1つのプロパティセットで同じ名前の複数のプロパティをサポートしていません。 データ辞書をより利用しやすくするために、接続プロパティを避けることを検討してください。

**ダイナミック・プロパティ**使用`Property`.`IsDynamic`と。`DynamicParameterPropertyCodes`) "動的プロパティの関数のパラメータであるプロパティ"<sub>[iso23386、5.3.29]。</sub>言い換えれば、ダイナミック・プロパティの値は、次のように指定されたプロパティの値に依存する。`DynamicParameterPropertyCodes`bSDDには、公式の正確な方程式を機械的に解釈可能な形で定義するフィールドはない。 

ダイナミック・プロパティを使用して、他のどのプロパティが特定のプロパティの値に影響を与えるかを示します。

例_壁の「面積」は、「高さ」と「長さ」によって決まる。_

⚠️ この機能はISO標準に由来するが、ソフトウェア実装でサポートされることはほとんどない。 データ辞書をより利用しやすくするために、ダイナミック・プロパティを避けることを検討すること。

<h3 id="restricting-property-values">Restricting property values</h3>

開発する🚧。
`AllowedValues`...

`Min/MaxInc/Exclusive`...

`Pattern`...

<h3 id="identifying-bsdd-resources">Identifying bSDD resources</h3>

開発する🚧。
`URI`... Can be generated by bSDD or external.

`Code`... セクションを参照[フォーマットコード](#code-format).

`UID`(GUID)...

<h3 id="specifying-units">Specifying units</h3>

開発する🚧。
`Unit(s)`...

`Dimension`...

`PhysicalQuantity`...

<h3 id="double-square-bracket-links">Double square bracket links</h3>
It is possible to reference other resources from the same dictionary using double square brackets, and the platform will replace the brackets with hyperlinks pointing to that resource. In cases where the same code exists for both class and property, the hyperlink will point to the class. If the code is not found, the square brackets are omitted. The API returns the definition with square brackets. 

<h2 id="notifications">Notifications</h2>

**2023-07 - 重要なお知らせ**

> 辞書コードと辞書バージョンの間のダッシュは、スラッシュに置き換えられました：
>  https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs-1.0.0/class/apple will now be https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/class/apple
> 
> 少なくとも4ヶ月間は、辞書コードとバージョンの間にダッシュを使用したデータの供給と検索をサポートします。 しかし、新しい形式の識別子のみがbSDD APIによって返されることに注意してください。

**2022-08 - 重要なお知らせ**

> bSDDは、"http://identifier.buildingsmart.org "から始まる識別子（別名 "URI"）を、"https://identifier.buildingsmart.org"（"http "から "https"）に移行中である。これは、これらの識別子をハイパーリンクとしても使いやすくするためである。
> 
> 古い "http "識別子を使用するサポートは、まもなく非推奨となる！

📢 最新の技術アップデートについては、専用フォーラムのトピック（https://forums.buildingsmart.org/t/bsdd-tech-updates/4889）をご覧ください。
