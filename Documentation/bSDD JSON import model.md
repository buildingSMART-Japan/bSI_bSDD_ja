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

bSDDは、独立した組織によって発行されたデータ辞書（データ辞書とは何かについては以下をお読みください）の配布を容易にするためのサービスです。下の図は、bSDD の背後にある単純化されたデータモデルを示しています：

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_model.png" alt="bSDD entity diagram" style="width: 650px"/>

上記のコンセプトの使い方を示した例をご覧ください：[bSDDデータ例](https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png)：  
<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png" alt="bSDD entity diagram" style="width: 700px"/>

デモンストレーション用の辞書もあります：[「果物と野菜](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.1)

📢 最新の技術アップデートについては、専用フォーラムトピックでお読みください：[https://forums.buildingsmart.org/t/bsdd-tech-updates/4889](https://forums.buildingsmart.org/t/bsdd-tech-updates/4889)

<h2 id="json-format">JSON format</h2>

buildingSMARTデータディクショナリのデータは、このドキュメントで説明する標準に従って、JSONファイルで納品することができます。JSONとExcelのテンプレートは、[/Model/Import Modelにも](https://github.com/buildingSMART/bSDD/tree/master/Model/Import%20Model)あります。

リンクをクリックすると、[国](https://api.bsdd.buildingsmart.org/api/Country/v1)、[言語](https://api.bsdd.buildingsmart.org/api/Language/v1)、[単位](https://api.bsdd.buildingsmart.org/api/Unit/v1)、[参考文書](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)、[ifc](https://api.bsdd.buildingsmart.org/api/Dictionary/v2/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3)クラスに使用できるコードの一覧が表示されます。  
参照ドキュメントが不足していると思われる場合は、[issueを投稿して](https://github.com/buildingSMART/bSDD/issues)お知らせください。JSON内の値は、数値の例およびAllowedValueフィールドを含め、すべて二重引用符で囲まれた文字列でなければなりません。

JSONに馴染みのない方は、[JSON入門を](https://javaee.github.io/tutorial/jsonp001.html)お読みになることをお勧めします。JSONは、コンピュータ・システムがデータを交換するためのフォーマットであることに注意してください。辞書データがコンピュータ・システムにある場合、システムにJSONを作成させるのが最善です。

<h2 id="list-of-fields">List of fields</h2>

NBデフォルト値は、フィールドが指定されていない場合にのみ適用されます。フィールド値に "null "を指定した場合、デフォルト値は適用されない。すべてのフィールドで "null "を指定できるわけではないことに注意。

<h3 id="Dictionary">Dictionary</h3>

`Data dictionary` -*データの意味、他のデータとの関係、出所、使用法、形式など、データに関する情報の一元化されたリポジトリ*」。[ISO23386]。*メタデータを含むデータベース*」[ISO12006-3]。各`Dictionary` (以前は`domain`)は、`Classes` (以前は`classifications`)と`Properties` から構成される。 は、互いに関連することも、他の`Dictionaries` と関連することもある。各`Dictionary` オブジェクトは、以下の表に示すように、それに関する一般的なメタデータを含む。

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|------------------|------------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="OrganizationCode">組織コード</span> | テキスト | ✅ |  | bSDD への登録時に受け取った組織のコード。あなたの組織がまだコードを持っていない場合は、[bSDD ユーザヘルプデスクで](https://bsi-technicalservices.atlassian.net/servicedesk/customer/portal/3/group/4/create/25)リクエストしてください。コードは、すべての URI リンクに表示されるため、短いものが望ましい。許可される文字については、[コード形式の](#code-format)項を参照のこと。このコードは数字で始まることはできない。コードの例「ifc". |
| <span id="DictionaryCode">辞書コード</span> | テキスト | ✅ |  | 辞書のコード：「ifc"。[コード形式](#code-format)参照。 |
| <span id="DictionaryName">辞書名</span> | テキスト | ✅\ |  | 辞書の名前。\*辞書が存在する場合、この名前を指定する必要はない。 |
| <span id="DictionaryVersion">辞書バージョン</span> | テキスト | ✅ |  | 辞書データのバージョン。例：1.0.1。例：1.0.1："12", "10.1", "1.2.3".不可：「1.2.3.4"、"ベータ"、"2x3"。私たちは、[セマンティック・バージョニング・アプローチに](https://semver.org/)従うことを推奨します。 |
| <span id="LanguageIsoCode">言語IsoCode</span> | テキスト | ✅ |  | ISO言語コード：データの言語を示す。複数の言語でデータを配信したい場合は、言語ごとにJSONファイルを使用してください。[言語](https://api.bsdd.buildingsmart.org/api/Language/v1)一覧参照。\* 例"de-DE" |
| <span id="LanguageOnly">言語のみ</span> | ブーリアン | ✅ |  | JSONが言語固有の情報のみを含む場合はtrue、そうでない場合はno。 |
| <span id="UseOwnUri">UseOwnUri</span> | ブーリアン | ✅ |  | デフォルト：false。クラスとプロパティをグローバルに一意に識別するために、独自のURIを使用します。独自のURIを使用しない場合、"https://identifier.buildingsmart.org" で始まるURIが各`Class` と `Property' に割り当てられます。 |
| <span id="DictionaryUri">辞書Uri</span> | テキスト | ✅\ |  | UseOwnUri = trueの場合は必須。すべてのクラスおよびプロパティのURIの最初の部分である、グローバルに一意なURIを指定します："urn:mycompany:mydictionary "または "https://mycompany.com/mydictionary" |
| <span id="License">ライセンス</span> | テキスト |  |  | コンテンツのライセンスの識別子。[Creative Commons](https://creativecommons.org/choose/)または[OSI Approved Licensesから](https://opensource.org/licenses/)ライセンスを選択することを推奨する。該当する場合、標準化された[SPDX](https://spdx.org/licenses/)識別子を正規の信頼できる識別のために使用する必要があります（例："MIT "または "CC-BY-4.0"）：例えば、"MIT "や "CC-BY-4.0 "などです。役に立つリソースは、[ChooseALicense.com](https://choosealicense.com/)です。 |
| <span id="LicenseUrl">ライセンス</span> | テキスト |  |  | ライセンスの全文を掲載したウェブサイトへのリンク。ライセンスページは、提供された「ライセンス」名と一致する必要があります。 |
| <span id="ChangeRequestEmailAddress">ChangeRequestEmailAddress</span> | テキスト |  |  | ユーザーからの変更リクエストを受け取るための単一のメールアドレス。メールアドレスを提供することで、ユーザーからのリクエストを転送し、APIを通じてアドレスを公開することに同意するものとします。お客様は、当社に連絡することにより、情報を撤回する権利を有します。 |
| <span id="ModelVersion">モデルバージョン</span> | テキスト |  |  | 入力JSONテンプレートのバージョン番号。 |
| <span id="MoreInfoUrl">MoreInfoUrl</span> | テキスト |  |  | 辞書に関する詳細情報を含むウェブページへのURL |
| <span id="QualityAssuranceProcedure">品質保証手順</span> | テキスト |  |  | 辞書に使用される品質保証手順の名称または簡単な説明：例："ETIM international"、"AFNOR NF XP P07-150 (PPBIM)"、"bSI プロセス"、"UN GHS 2015"、"UN CPC 1.1"、"非公開"、"不明" |
| <span id="QualityAssuranceProcedureUrl">品質保証手続きURL</span> | テキスト |  |  | 品質保証手順に関する詳細情報を掲載したウェブページへの URL："https://www.buildingsmart.org/about/bsi-process" |
| <span id="ReleaseDate">リリース日</span> | 日時 |  |  | バージョンのリリース日。「[Date Time format](#datetime-format)」を参照。 |
| <span id="Status">ステータス</span> | テキスト |  |  | 可能なバージョンステータス：`Preview` `Active` `Inactive` 。新しいバージョンをアップロードするときは、常に`Preview` である必要があります。その後、[API](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1)または[管理ポータルを介して](https://manage.bsdd.buildingsmart.org/)コンテンツをアクティブ化または非アクティブ化できます。続きを読む:[bSDDコンテンツのライフサイクル](https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/bSDD%20import%20tutorial.md#the-lifecycle-of-the-bsdd-dictionary-version) |
| <span id="Classes">クラス</span> | クラス一覧 | ✅ |  | `Class` 型のオブジェクトのリスト。[クラス](#class) |
| <span id="Properties">プロパティ</span> | 物件リスト | ✅ |  | `Property` 型のオブジェクトのリスト。[プロパティ](#property) |


\* 追加言語でデータを配信する場合は、`Dictionary` タイプフィールド、すべての`Code` フィールド、および他のタイプの`Translatable?` = "Yes "とマークされたフィールドを埋めるだけで十分です。`OrganizationCode` 、`DictionaryCode` 、`DictionaryVersion` がまったく同じであることを確認し、データが既存の`Dictionary` に言語を追加するためのものである場合は、フィールド`LanguageOnly` を true に設定する。

<h3 id="Class">Class</h3>

`Class` -*同じ特徴を共有するオブジェクトの集合の記述*」。[ISO23386]。`Class` は、任意のオブジェクト（例：「壁」、「窓」）、抽象概念（例：「時間」、「部屋」）、またはプロセス（例：「設置」、「分解」）である。


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|---------------------------|--------------------------------|-------------|-----------------|--------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト | ✅ |  | 辞書内のクラスの一意の識別。例："abc-00123-01 "または "SpecialWall"。コード・バリデーションが適用されます：[コード形式](#code-format)。接頭辞「Ifc」は、IFC 標準のために予約されている。 |
| <span id="Name">名称</span> | テキスト | ✅ | ✅ | `Class,` ："イフカーテンウォール" |
| <span id="ClassType">クラスタイプ</span> | テキスト | ✅ |  | のいずれかでなければならない：`Class` `Material`,`GroupOfProperties`,`AlternativeUse`.[クラス・タイプの](#class-types)詳細はこちら。指定しない場合、デフォルトで`Class` タイプが使用されます。`ReferenceDocument` 、`ComposedProperty` 、`Dictionary` のタイプは非推奨となり、アップロード時に使用することはできませんが、移行期間中はAPI結果に表示されることがあります。 |
| <span id="Definition">定義</span> | テキスト |  | ✅ | `Class` の定義。意味的な意味を説明する。ISO に従った必須フィールド。[二重角括弧リンクを](#double-square-bracket-links)サポート。 |
| <span id="Description">説明</span> | テキスト |  | ✅ | 補足説明のための追加フィールド。*定義(Definition)*が規格に由来し、さらに説明が必要な場合にのみ使用してください。 |
| <span id="ParentClassCode">親クラスコード</span> | テキスト |  |  | 親への参照`Class` 。このフィールドのIDは、配信されたデータに存在しなければならない（MUST）。例"ifc-00123-00"。[リレーションシップを定義するには？](#defining-relations) |
| <span id="RelatedIfcEntityNamesList">関連Ifcエンティティ名リスト</span> | テキスト一覧 |  |  | この`Class` の表現として使用する IFC クラスのコード。例えば[IfcWall']。bSDD API[ifc classs を](https://api.bsdd.buildingsmart.org/api/Dictionary/v3/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3%2F)参照。[関係を定義するには？](#defining-relations) |
| <span id="Synonyms">同義語</span> | テキスト一覧 |  | ✅ | 検索しやすいように、このクラスの代替名称のリスト。 |
| <span id="ActivationDateUtc">アクティベーション日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="ReferenceCode">参照コード</span> | テキスト |  |  | 参照コードは、辞書固有の用法を持つことができる。NULLの場合、`Code` の値がフィールドを埋めるために使用される。`ReferenceCode` を空にするには、空の文字列""を使用する。 |
| <span id="CountriesOfUse">使用国</span> | テキスト一覧 |  |  | この`Class` が使用されている国 ISO コードのリスト。参照リスト[国を](https://api.bsdd.buildingsmart.org//api/Country/v1)参照してください。 |
| <span id="CountryOfOrigin">原産国</span> | テキスト |  |  | この`Class` の原産国の ISO 国コード。参照リストの[国を](https://api.bsdd.buildingsmart.org//api/Country/v1)参照してください。 |
| <span id="CreatorLanguageIsoCode">CreatorLanguageIsoCode</span> | テキスト |  |  | 作成者の言語ISOコード。参照リストの[言語を](https://api.bsdd.buildingsmart.org/api/Language/v1)参照。 |
| <span id="DeActivationDateUtc">解除日Utc</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="DeprecationExplanation">非推奨説明</span> | テキスト |  | ✅ | 非推奨の定義のみを埋める。 |
| <span id="DocumentReference">ドキュメント参照</span> | テキスト |  |  | `Class` の完全な定義または正式な定義が記載された文書への言及。 参考文献リストの[参考文献を](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)参照のこと。 |
| <span id="OwnedUri">所有ウリ</span> | テキスト |  |  | ディクショナリ・レベルで`UseOwnUri = true` を指定した場合は、`Class' をグローバルに一意に識別する URI を指定する必要があります。 |
| <span id="ReplacedObjectCodes">置換オブジェクトコード</span> | テキスト一覧 |  |  | このクラスが置き換えるクラス・コードのリスト |
| <span id="ReplacingObjectCodes">オブジェクトコードの置き換え</span> | テキスト一覧 |  |  | このクラスは次のクラスコードに置き換えられる。 |
| <span id="RevisionDateUtc">リビジョン日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="RevisionNumber">リビジョン番号</span> | 整数 |  |  |  |
| <span id="Status">ステータス</span> | テキスト |  |  | `Class` のステータス :`Active` (デフォルト) または `Inactive |
| <span id="SubdivisionsOfUse">用途地域</span> | テキスト一覧 |  | ✅ | 使用地域のリスト 例"US-MT" |
| <span id="Uid">ウイド</span> | テキスト |  |  | URIだけでは不十分な場合のための一意な識別（ID）。 |
| <span id="VersionDateUtc">バージョン日付</span> | 日時 |  |  | デフォルトでは、インポートされた日付が使用されます。[Date Time formatを](#datetime-format)参照。 |
| <span id="VersionNumber">バージョン番号</span> | 整数 |  |  |  |
| <span id="VisualRepresentationUri">VisualRepresentationUri</span> | テキスト |  | ✅ |  |
| <span id="ClassProperties">クラスプロパティ</span> | クラスプロパティ一覧 |  |  | [ClassProperty](#ClassProperty)の項を参照。 |
| <span id="ClassRelations">クラス関係</span> | クラス関係一覧 |  |  | [クラス関係](#ClassRelation)参照 |

注：2023年11月のリリース以降、マテリアルは個別に扱われなくなった。`Material` は単に`Material` タイプの`Class` である。

<h3 id="Property">Property</h3>

`Property` -*アイテムに固有の、または後天的な特徴 [`Class`].例：熱効率、ヒートフロー、（...）、色。*[ISO23386]。  `Properties` から`Classes` への代入は、中間の[ClassProperty](#ClassProperty)オブジェクトを通して処理されます。 


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|-------------------------------|--------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト | ✅ |  | 辞書内のプロパティの一意な識別。例："abc-00123-01 "または "SpecialWidth"。コード・バリデーションが適用されます：[コード形式](#code-format)。 |
| <span id="Name">名称</span> | テキスト | ✅ | ✅ | プロパティの名前 例"IsExternal" |
| <span id="Definition">定義</span> | テキスト |  | ✅ | `Property` の定義。意味的な意味を説明する。ISO に従った必須フィールド。[二重角括弧リンクを](#double-square-bracket-links)サポート。 |
| <span id="Description">説明</span> | テキスト |  | ✅ | 補足説明のための追加フィールド。*定義(Definition)*が規格に由来し、さらに説明が必要な場合にのみ使用してください。 |
| <span id="DataType">データ型</span> | テキスト | ✅ |  | プロパティが表現されるデータ型。のいずれかでなければならない：  `Boolean` `Character` ,`Integer`,`Real`,`String`, `Time |
| <span id="Units">単位</span> | テキスト一覧 |  |  | 単位は、値を測定できる目盛りを表す（ISO 80000またはISO 4217、またはISO 8601）。値のリスト。[単位の](https://api.bsdd.buildingsmart.org/api/Unit/v1)参照リスト[（JSON）](https://api.bsdd.buildingsmart.org/api/Unit/v1)または[単位のCSVテーブルの](../DataFiles/units.csv)形式を参照してください。私たちは[QUDTの](http://www.qudt.org/)多くの単位をサポートしていますが、もし足りない単位があれば、[issueとして単位のリクエストを投稿して](https://github.com/buildingSMART/bSDD/issues)ください。 |
| <span id="Example">例</span> | テキスト |  | ✅ | プロパティの例 |
| <span id="ActivationDateUtc">アクティベーション日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="ConnectedPropertyCodes">接続プロパティコード</span> | テキスト一覧 |  |  | 1つ以上の接続プロパティのコードのリスト。他の辞書のプロパティである場合は、コードの代わりに完全なURIを指定することもできる。[アセンブルプロパティを](#assembling-properties)参照。 |
| <span id="CountriesOfUse">使用国</span> | テキスト一覧 |  |  | この`Property` が使用されている国 ISO コードのリスト。参照リスト[国を](https://api.bsdd.buildingsmart.org/api/Country/v1)参照してください。 |
| <span id="CountryOfOrigin">原産国</span> | テキスト |  |  | この`Property` の原産国の ISO 国コード。参照リストの[国を](https://api.bsdd.buildingsmart.org//api/Country/v1)参照してください。 |
| <span id="CreatorLanguageIsoCode">CreatorLanguageIsoCode</span> | テキスト |  |  | 作成者の言語ISOコード。参照リスト(JSON[)言語](https://api.bsdd.buildingsmart.org/api/Language/v1) |
| <span id="DeActivationDateUtc">解除日Utc</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="DeprecationExplanation">非推奨説明</span> | テキスト |  | ✅ |  |
| <span id="Dimension">寸法</span> | テキスト |  |  | 物理量の場合，ISO 80000-1 で定義されているように，[*InternationalSystemof*_Quantities](https://en.wikipedia.org/wiki/International_System_of_Quantities) に従って寸法を指定する。その順序は，`length` ，`mass` ，`time` ，`electric current` ，`thermodynamic temperature` ，`amount of substance` ，`luminous intensity` である。例えば、速度（m/s）は "1 0 -1 0 0 0 0 "と表記される。[IDSのドキュメントに](https://github.com/buildingSMART/IDS/blob/ver/1.0.x/Documentation/UserManual/units.md)あるその他の例 |
| <span id="DimensionLength">寸法長さ</span> | 整数 |  |  | 長さ寸法。フィールド`Dimension` を使用してすべての部品を指定するか、すべての部品を個別に指定する。 |
| <span id="DimensionMass">寸法質量</span> | 整数 |  |  | 質量寸法。`Dimension` フィールドを使用してすべての部品を指定するか、すべての部品を個別に指定する。 |
| <span id="DimensionTime">ディメンションタイム</span> | 整数 |  |  | フィールド`Dimension` を使用してすべてのパートを指定するか、すべてのパートを個別に指定する。 |
| <span id="DimensionElectricCurrent">寸法電流</span> | 整数 |  |  | フィールド`Dimension` を使用してすべての部 品を指定するか、すべての部品を 個別に指定する。 |
| <span id="DimensionThermodynamicTemperature">寸法熱力学温度</span> | 整数 |  |  | ThermodynamicTemperature（熱力学的温度）ディメンジョン。`Dimension` フィールドを使用してすべての部分を指定するか、すべての部分を個別に指定する。 |
| <span id="DimensionAmountOfSubstance">DimensionAmountOfSubstance（ディメンション物質量</span> | 整数 |  |  | AmountOfSubstance ディメンジョン。`Dimension` フィールドを使用してすべての部位を指定するか、すべての部位を個別に指定します。 |
| <span id="DimensionLuminousIntensity">寸法光度</span> | 整数 |  |  | LuminousIntensity ディメンジョン。フィールド`Dimension` を使ってすべての部分を指定するか、すべての部分を個別に指定する。 |
| <span id="DocumentReference">ドキュメント参照</span> | テキスト |  |  | `Property` の完全な、または公式な定義が記載された文書への参照。 参照リスト (JSON)[参照文書を](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)参照のこと。 |
| <span id="DynamicParameterPropertyCodes">DynamicParameterPropertyCodes</span> | テキスト一覧 |  |  | 動的プロパティの関数のパラメータであるプロパティのコードのリスト。[プロパティの組み立てを](#assembling-properties)参照。 |
| <span id="IsDynamic">IsDynamic</span> | ブーリアン |  |  | デフォルト：`false` 。こ れが動的プ ロパテ ィ の場合、 値はフ ィ ール ド`DynamicParameterPropertyCodes` で与え ら れたパ ラ メ タ に依存 し ます。[プロパティの組み立てを](#assembling-properties)参照してください。 |
| <span id="MaxExclusive">マックスエクスクルーシブ</span> | リアル |  |  | 最大許容値、排他的 - 包含値と排他値の両方を記入しないこと |
| <span id="MaxInclusive">マックスインクルーシブ</span> | リアル |  |  | 最大許容値、包含値 - 包含値と排他値の両方を記入しないこと |
| <span id="MinExclusive">Minエクスクルーシブ</span> | リアル |  |  | 最小許容値、排他的 |
| <span id="MinInclusive">ミニインクルーシブ</span> | リアル |  |  | 許容最小値（含む |
| <span id="MethodOfMeasurement">測定方法</span> | テキスト |  | ✅ | 例「ISO 10077-1による熱貫流率 |
| <span id="OwnedUri">所有ウリ</span> | テキスト |  |  | ディクショナリ レベルで`UseOwnUri = true` を指定 し てい る 場合は、 Property をグ ロ ーバルに一意に識別す る URI を与え る 必要があ り ます |
| <span id="Pattern">パターン</span> | テキスト |  |  | 許容値を制限するための[XMLスキーマ正規表現](https://www.regular-expressions.info/xml.html) |
| <span id="PhysicalQuantity">物理量</span> | テキスト |  | ✅ | プロパティの物理量の名前："なし "または "質量" |
| <span id="PropertyValueKind">プロパティ値</span> | テキスト |  |  | `Single` (1つの値。これがデフォルト),`Range` (2つの値),`List` (複数の値),`Complex` (単一/範囲/リストのどちらでもない。例えば、IfcActorのようなオブジェクトや、接続されたプロパティの集合体 -[プロパティの集合体を](#assembling-properties)参照),`ComplexList` (複合値のリスト) のいずれかでなければならない。 |
| <span id="ReplacedObjectCodes">置換オブジェクトコード</span> | テキスト一覧 |  |  | この`Property` が置き換えるプロパティコードのリスト |
| <span id="ReplacingObjectCodes">オブジェクトコードの置き換え</span> | テキスト一覧 |  |  | このプロパティコードのリスト`Property` は次のように置き換えられる。 |
| <span id="RevisionDateUtc">リビジョン日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="RevisionNumber">リビジョン番号</span> | 整数 |  |  |  |
| <span id="Status">ステータス</span> | テキスト |  |  | プロパティのステータス：`Active` （デフォルト）または `Inactive |
| <span id="SubdivisionsOfUse">用途地域</span> | テキスト一覧 |  | ✅ | 使用地域のリスト 例"US-MT" |
| <span id="TextFormat">テキストフォーマット</span> | テキスト |  |  | テキス ト 種別 （エン コ ーデ ィ ン グ、 キ ャ ラ ク タ 数） のペア エン コ ーデ ィ ン グは、 IANA の RFC 2978 の 「エン コ ーデ ィ ン グ規格名」 に従っ て設定 さ れます："(UTF-8,32)" |
| <span id="Uid">ウイド</span> | テキスト |  |  | URIだけでは不十分な場合のための一意な識別（ID）。 |
| <span id="VersionDateUtc">バージョン日付</span> | 日時 |  |  | デフォルトでは、インポートされた日付が使用されます。[Date Time formatを](#datetime-format)参照。 |
| <span id="VersionNumber">バージョン番号</span> | 整数 |  |  |  |
| <span id="VisualRepresentationUri">VisualRepresentationUri</span> | テキスト |  | ✅ |  |
| <span id="PropertyRelations">プロパティ関連</span> | PropertyRelationのリスト |  | ✅ | 関連するプロパティのリスト。[PropertyRelation](#PropertyRelation)参照。 |
| <span id="AllowedValues">許容値</span> | 許容値のリスト |  | ✅ | プロパティに許容される値のリスト。注意: boolean型のプロパティには使用しないでください。[AllowedValue](#AllowedValue) セクションを参照してください。 |


<h3 id="ClassProperty">ClassProperty</h3>

`Property` を、それが記述すべき`Class` に割り当てるための中間オブジェクト。各`Class` は複数のプロパティを持つことができ、各`Property` は多くの`Classes` の一部になることができますが、1つの`ClassProperty` は常に1つの`Class` と1つの`Property` のペアです。 

`ClassProperty` を通して、単位、格納されるべきプロパティセット、および特定の`Class` に適用される場合の値の制限を定義することにより、「プロパティ」をさらに指定することができる。例えば、一般的な「温度」は、摂氏または華氏で表すことができ、負の値でも正の値でもよ いが、室内空間に適用する場合は、摂氏5～40度の範囲に制限されるかもしれない。   


| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|---------------------|----------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト |  |  | `ClassProperty` の固有識別コード。 コード・バリデーションが適用される：[コード形式](#code-format)。インポート時に空のままだと、bSDDはランダムなGUIDを生成する。 |
| <span id="PropertyCode">プロパティコード</span> | テキスト | ✅\ |  | 同じ`Dictionary` 内にある場合は`Property` への参照。\* PropertyCodeが使用されている場合は、PropertyUriを記入しないでください。 |
| <span id="PropertyUri">PropertyUri</span> | テキスト | ✅\ |  | `Property` が別の`Dictionary` にある場合の参照：[PropertyUriが使用されている場合、PropertyCodeは記入しない。 |
| <span id="Description">説明</span> | テキスト |  | ✅ | クラス固有のプロパティの説明を指定することができます。省略された場合、該当するプロパティの「一般的な」説明が表示されます。 |
| <span id="PropertySet">プロパティセット</span> | テキスト |  |  | プロパティが IFC データに配置されるべきセットの名前。接頭辞 'Pset_' は公式 IFC 用に予約されています。コードバリデーションが適用されます：[コード形式を](#code-format)参照してください。詳細：[プロパティのアセンブル](#assembling-properties)。 |
| <span id="Unit">単位</span> | テキスト |  |  | Property 'Units'(リスト)とは異なり、この属性は単一の値を取る。[ユニットの](https://api.bsdd.buildingsmart.org/api/Unit/v1)参考リスト[（JSON）](https://api.bsdd.buildingsmart.org/api/Unit/v1)または[ユニットのCSVテーブルの](../DataFiles/units.csv)形式を参照してください。私たちは[QUDTの](http://www.qudt.org/)多くのユニットをサポートしていますが、もし見逃しているユニットがあれば、[ユニットリクエストをissueとして投稿して](https://github.com/buildingSMART/bSDD/issues)ください。 |
| <span id="PredefinedValue">定義済み値</span> | テキスト |  |  | この`Property` に対する定義済みの値。例: "IfcWall "クラスのプロパティ "IsLoadBearing "の値は "true "です。 |
| <span id="IsRequired">必須</span> | ブーリアン |  |  | このクラスが`Property` で必須かどうかを示す。 |
| <span id="IsWritable">書き込み可能</span> | ブーリアン |  |  | `Class` のこの`Property` の値を変更できるかどうかを示す。 |
| <span id="MaxExclusive">マックスエクスクルーシブ</span> | リアル |  |  | 最大許容値、排他的。`Property` に定義された値を上書きする。 'inclusive' および 'exclusive' 値の両方を記入してはならない。 |
| <span id="MaxInclusive">マックスインクルーシブ</span> | リアル |  |  | 最大許容値。`Property` に定義された値を上書きする。 'inclusive' と 'exclusive' の両方の値を記入してはならない。 |
| <span id="MinExclusive">Minエクスクルーシブ</span> | リアル |  |  | 最小許容値、排他的。`Property` に定義された値を上書きする。 'inclusive' および 'exclusive' 値の両方を記入してはならない。 |
| <span id="MinInclusive">ミニインクルーシブ</span> | リアル |  |  | 最小許容値。`Property` に定義された値を上書きする。 'inclusive' および 'exclusive' 値の両方を記入してはならない。 |
| <span id="Pattern">パターン</span> | テキスト |  |  | 許容値を制限するための[XML Schema 正規表現](https://www.regular-expressions.info/xml.html)。Property に対して定義されたパターンを上書きします。 |
| <span id="OwnedUri">所有ウリ</span> | テキスト |  |  | ディクショナリ・レベルで`UseOwnUri = true` を指定した場合は、ClassProperty をグローバルに一意に識別する URI を指定する必要があります。 |
| <span id="PropertyType">プロパティタイプ</span> | テキスト |  |  | `Class` に対する`Property` のタイプ :`Property` (デフォルト) または `Dependency |
| <span id="SortNumber">ソート番号</span> | 整数 |  |  | この`Property` の `Class` 内のソート番号。 |
| <span id="Symbol">シンボル</span> | テキスト |  |  |  |
| <span id="AllowedValues">許容値</span> | 許容値のリスト |  | ✅ | `ClassProperty` の許容値のリスト。`Property` のために定義された値をオーバーライドします。 boolean タイプのプロパティには、この値を使用しないでください。[AllowedValue](#AllowedValue)参照。 |
| ~~外部プロパティUri~~ | ~~テキスト~~ |  |  | 廃止 - 代わりに`PropertyUri` を使用してください。 |


<h3 id="AllowedValue">AllowedValue</h3>

`Properties` 、`ClassProperties` 。例えば、'Fire Rating'にはいくつかの値しか許されない：REI30、REI60、REI90、REI120。

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト | ✅ |  | Codeは、値を一意に識別するためのものである（最大20文字）。これは必須であり、ほとんどの場合、値と同じです。値やその説明の翻訳を可能にするために必要です。コードのバリデーションが適用されます：[コードフォーマット](#code-format) |
| <span id="Value">価値</span> | テキスト | ✅ | ✅ | プロパティが持ちうる値の1つ：例：プロパティが "Color "の場合、"Green" |
| <span id="Description">説明</span> | テキスト |  | ✅ | 値の説明 |
| <span id="Uri">ウリ</span> | テキスト |  |  | OwnedUriと重複するため、新モデルバージョンでは非推奨。 |
| <span id="SortNumber">ソート番号</span> | 整数 |  |  | その値が属する`Property` の値リストにおける値のソート番号。 |
| <span id="OwnedUri">所有ウリ</span> | テキスト |  |  | ディクショナリ・レベルで`UseOwnUri = true` を指定した場合、AllowedValue をグローバルに一意に識別する URI を指定できます。 |

注：`AllowedValue` の翻訳追加はまだサポートされていません。

<h3 id="ClassRelation">ClassRelation</h3>

`Classes` は関係によってリンクすることができる。リレーションには様々な種類があり、階層、合成、類似性、参照などを定義することができる。[リレーションを定義するには？](#defining-relations)

| フィールド | データ型 | 必要か？ | トランス・ラタブル？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelationType">関係タイプ</span> | テキスト | ✅ |  | のいずれか：  `HasMaterial` `HasReference` ,`IsEqualTo`,`IsSimilarTo`,`IsParentOf`,`IsChildOf`,`HasPart`,`IsPartOf`.[関係タイプについて](#relation-types)もっと読む。 |
| <span id="RelatedClassUri">関連クラスUri</span> | テキスト | ✅ |  | 関連する`Class` の完全な URI。`Dictionary` と同じでも異なっていてもかまいません。例：https://identifier.buildingsmart.org/uri/etim/etim/8.0/class/EC002987 |
| <span id="RelatedClassName">関連クラス名</span> | テキスト |  |  |  |
| <span id="Fraction">分数</span> | リアル |  |  | `HasMaterial` 関係にのみ適用される。オプションで、関係を所有するクラスに適用される総量（例：体積または重量）の端数を指定します。クラス/関係タイプごとの分数の合計は 1 でなければならない。[IfcMaterialConstituent](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterialConstituent.htm)の Fraction に類似。 |
| <span id="OwnedUri">所有ウリ</span> | テキスト |  |  | ディクショナリ・レベルで`UseOwnUri = true` を指定した場合は、クラス・リレーションをグローバルに一意に識別する URI を指定する必要があります。 |


<h3 id="PropertyRelation">PropertyRelation</h3>

`ClassRelations` と似ているが、`Properties` の間である。

| フィールド | データ型 | 必要ですか？ | 翻訳可能か？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelatedPropertyName">関連プロパティ名</span> | テキスト |  |  | 関連サイト名`Property`. |
| <span id="RelatedPropertyUri">関連プロパティUri</span> | テキスト | ✅ |  | 関連する`Property` の完全な URI。それは同じでも異なっていてもよい`Dictionary` 。 |
| <span id="RelationType">関係タイプ</span> | テキスト | ✅ |  | のいずれか：  `HasReference` `IsEqualTo` ,`IsSimilarTo`,~~IsParentOf, IsChildOf, HasPart~~.[関係タイプについて](#relation-types)もっと読む。 |
| <span id="OwnedUri">所有ウリ</span> | テキスト |  |  | ディクショナリレベルで`UseOwnUri = true` を指定した場合には、 PropertyRelation をグローバルに一意に識別する URI を与えなければなりません。 |

---

<h2 id="additional-explanations">Additional explanations</h2>

<h3 id="code-format">Code format</h3>

(2024年4月以降) すべてのコードで、発音区分、空白、ドット、コンマ、ダッシュ、丸括弧、アンダースコア、数字が使用可能。特殊文字は使用できません：`"#%/\:`{}[]|;&lt;&gt;?~```.コードは大文字と小文字を区別しません。 

有効なコードの例をいくつか挙げる："bs-agri"、"apple"、"éÄą _- (Д開発,...ź)"。

コードは同じデータ辞書内で一意である必要があり、URIを生成するために使用される。

例えば、IFC規格では、接頭辞'Ifc'と'Pset'で始まるコードが予約されている。 

<h3 id="class-types">Class types</h3>

各クラスには特定のタイプが必要です。以下は、ISO 12006-3に従った、各タイプの意味の説明です：
* `Class` - 同じ特徴を共有するオブジェクトの集合の記述<sup>[ISO12006-3,3.7]</sup>。bSDD では最も一般的なタイプである。(例：壁、空間）
* `GroupOfProperties` - プロパティ・コレクションは、プロパティをあらかじめ整理または整頓できるようにするものである<sup>[ISO12006-3,3.14]</sup>。例えば、'environmental properties'など。[プロパティの組み立て](#assembling-properties)」を参照。
* `Material` - 物を作ることができる物理的な物質（例：鋼鉄、ガラス）
* `AlternativeUse` - を使用する[<sup>ISO12006-3,3.1]</sup>。
   * ほとんどのソフトウェア実装は、このクラス型を無視する。
* **DEPRECATED** ~~参照文書（ReferenceDocument） - 特定の情報を見つけるために参照される出版物。<sup>[iso12006-3,3.18]</sup>。参照文書は、データ辞書に存在するあらゆるデータと関連付けることができる。~~
  * bSDDでは、[参照として](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)使用できる最も一般的な規格を含む[参照](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)文書のグローバルリストを用意している。これは、異なるネーミングの参考文献が重複しないようにするためです。もしお探しの参考文献が見つからず、リストに加えるべきだとお考えでしたら、ぜひお知らせください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).
* **DEPRECATED** ~~ComposedProperty - (...) 複数のプロパティを定義する必要があるフィーチャーに対応する。<sup>[iso12006-3,3.8]</sup>。~~
  * ~~例コンクリート面品質」という特性を記述するためには、コンクリートの平面性、コンクリートの色相、コンクリートの質感という3つの特性を記述することが必須である。~~
  * 代わりに`GroupOfProperties` 。

<h3 id="defining-relations">Defining relations</h3>

`ParentClassCode` -`Class`同じ辞書内の要素は、ツリーのような階層構造で整理することができる。たとえば例えば、"IfcCurtainWall" は、より階層的な構造である。  
の特定のクラスである。bSDDの用語では、"IfcWall "は "IfcCurtainWall "**の親**であると言う。このような特殊化関係を定義するには、子オブジェクトの`ParentClassCode` 。

`ClassRelation` そして`PropertyRelation` 、これらを使って概念同士をリンクします。関係によって、他の辞書との親子リンクも定義できます。特殊化とは別に、分解のような他のタイプの関係も定義することができます (`HasPart` タイプ、可能なタイプのリストを参照:[関係タイプ](#relation-types))。

`RelatedIfcEntityNamesList` - IFC は、ソフトウェア間の情報交換に使用されるトップレベルのスキーマ（基礎クラス）です。そのため、bSDD はあなたのクラスを IFC に関連付けるための特別な方法を提供します。`RelatedIfcEntityNamesList` を使用して、IFC のどのエンティティを参照または拡張しているかを示します。例えば、"Signaling LED diode" は、IFC の "IfcLamp" に関連しています。`RelatedIfcEntityNamesList` は、bSDD 関連のツールで、可能なクラスのリストを特定の IFC カテゴリにフィルタリングするために使用できます。

<h3 id="relation-types">Relation types</h3>

`Properties` と`Classes` は互いに関連づけることができる。各関係は、ソフトウェアがそれを解釈できるように、特定の型を持たなければならない。以下に、それぞれの型が意味することを説明する：
* <span id='IsEqualTo'>`IsEqualTo`</span> - 2つの概念が明確で、同じ名前、コード、定義、説明を持っている場合。クラスもまた、同じクラス・プロパティを共有する必要がある。概念が同じであることは非常にまれです。使い方の例としては、ある概念に公式な翻訳がないにもかかわらず、誰かがその概念を新しい言語で新しい辞書を定義し、元の概念とまったく同じであると言いたい場合です。(私たちは常に、重複する辞書を作成する代わりに、元のデータ辞書に翻訳や改良を提案することを推奨します）。
* <span id='IsSimilarTo'>`IsSimilarTo`</span> - 2つの概念がほぼ等しいが、名前、コード、定義、説明、またはクラス・プロパティのセットによって異なる場合。これは非常に一般的な関係タイプである。例えば、'IfcWall' が CCI の 'Wall System' と類似の概念であることを示すために使用されます。このようなリレーションシップの欠点は、類似性のレベルがわからないことです。
* <span id='HasReference'>`HasReference`</span> - 2つの概念が互いに関連しているが、他の関係タイプが適用されない場合。たとえば、"壁掛けランプ"（または "燭台"）は、異なる概念であり、それらの間に階層がないにもかかわらず、壁を参照しています。
* **DEPRECATED** ~~IsSynonymOf - 二つの概念が同一であるが、名前が異なる場合。~~

クラスにのみ適用される（プロパティには適用されない）：
* <span id='IsChildOf'>`IsChildOf`</span> - specialisation 関係。"subtype "関係<sup>[ISO12006-3, F3.1]</sup>に相当する。例えば「電気モーター "と "燃焼モーター "は、総称概念 "モーター "の子（サブタイプ）である。
* <span id='IsParentOf'>`IsParentOf`</span> - `IsChildOf` とは逆の関係である。
* <span id='HasPart'>`HasPart`</span> - 構成関係。例えば、電動機はステータ、ロータなどの要素で構成される。[<sup>ISO12006-3, f3.2]</sup>。
* <span id='IsPartOf'>`IsPartOf`</span> - `HasPart` の逆。
* <span id='HasMaterial'>`HasMaterial`</span> - 特定の素材に関連付けられるクラス。例えば例えば、"Steel Beam "は "Steel "という材料に関連付けられる。

<h3 id="datetime-format">DateTime format</h3>

ISO 8601 シリーズに従った日付時刻形式を使用する必要があります:`YYYY-MM-DDThh:mm:ssTZD`.インポートでは両方が使用できます：`2023-05-10` `2023-05-10T15:10:12Z` および`2023-05-10T15:10:12+02:00` 。

<h3 id="property-inheritance">Property inheritance</h3>

* 親`Class` → 子`Class`
The child `Class` does not inherit properties from the parent `Class`. If authors want child classes to also have properties of parent classes, they should specify them intentionally in import files.  
For example, the [IfcWall](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall) is a parent class of [IfcWallStandardCase](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWallStandardCase). While [IfcWall](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall) has the property [AcousticRating](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall/prop/Pset_WallCommon/AcousticRating), the [IfcWallStandardCase](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWallStandardCase) doesn't.

* `Property` →`ClassProperty`
`ClassProperty` is an instantiation of general `Property` for a particular `Class`. The attributes of a property, such as `AllowedValue` and min/max restrictions,  are by default passed to `ClassProperty`. The values of the `ClassProperty` can be modified without influencing the origin `Property`.  
For example, the [Height](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/prop/height) has an upper limit of 100 cm. When applied to the "Apple" class, the [Apple-Height](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/class/apple/prop/SizeSet/height) has a lower limit - 25cm. 

<h3 id="latest-version">Latest version</h3>

bSDDでは、すべてのリソースはURIという一意の識別子を持つ。URIは、他の情報の中で、組織、辞書、およびバージョン番号のコードを含んでいる。例えば、.../uri/bs-agri/fruitvegs/1**.0.0/class/fruitの**ように。  
特定のリソースを参照したいが、そのバージョンがよくわからない、 あるいは、常に最新のバージョンを参照したい場合、私たちは "latest" 機能を実装しました。今、バージョン番号の代わりに "latest" を使用することが可能であり、 bSDD は、そのリソースを含む最新のアクティブバージョンまたは プレビューバージョンへのリンクを解決します：   
...**/uri/bs-agri/fruitvegs/latest/class/fruit**. 

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/latest_example.jpg" alt="bSDD latest" style="width: 750px"/>

お試しあれ：  
https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/latest/class/fruit

⚠️ "latest "は最新のリソースを指し、新しいバージョンが存在すると変更されることを意味する。これは不変のURIではなく、内容が変わる可能性があるため、注意して使用してください。契約上の合意には、特定のバージョン番号を使うことをお勧めします。

<h3 id="assembling-properties">Assembling properties</h3>

**プロパティのグループ**(use`Class`.`ClassType`:`GroupOfProperties`) "プロパティをあらかじめ並べたり、整理したりすることを可能にするコレクション"<sup>[ISO12006-3,3.14]</sup> 。bSDD では、複数の Properties をグループ化するための Type of Class として実装されている。

データ辞書内のプロパティを整理するには、プロパティのグループを使用します。

例：*「[LCA指標とモジュール](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0)」の「[地球温暖化係数](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/class/GlobalWarmingPotential)」クラスは、4つのプロパティをグループ化している：[合計](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total)」、「[生物起源](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_biogenic)」、「[化石燃料](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_fossil)」、「[土地利用](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_luluc)」。*

**プロパティのセット**（`ClassProperty`.`PropertySet` を使用） - プロパティをグループ化するための IFC 標準の概念。bSDD では、クラス・プロパティに定義されたテキスト・フィールドとして表され、このクラス・プロパティが IFC データにシリアライズされたときに、どのセットに表示されるかを示します。 
  * ISO 16739-1で定義されるプロパティセットはプロパティのグループであるが、プロパティのグループは必ずしもプロパティセットではない。
  * プロパティは、複数のプロパティ・グループのメンバになることができます。クラス・プロパティは、複数のプロパティ・セットのメンバになることはできません。
  * 接頭辞'Pset_'は公式IFCにのみ予約されている。

プロパティセットを使用して、IFC データセットのどこにプロパティを配置するかを定義します。

例*例: 'IfcWall' のプロパティ 'Concrete Cover' はプロパティセットにあります：'PsetConcreteElementGeneral*'._ にあります。

**接続プロパティ**(use`Property`.`ConnectedPropertyCodes`) "現在のプロパティに接続されているプロパティのリスト。接続は特殊化または依存関係である。"<sub>[iso12006-3、5.3.29]</sub>。

あるプロパティの値が他のプロパティの値に依存する場合は、Connected Propertiesを使用します。

例*例：[「地球温暖化係数-合計」（GWP](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total)）は、製品のライフサイクルの各段階について定義される べきである。各フェーズ（GWPA1*、GWPA2*、...）について * *個別にプロパティを定義する**ことは望ましくない。その代わりに、このプロパティは、別のプロパティである「[情報モジュール（PHASE）](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/information_module)」に接続され、18の可能な値（A1、A2、C3...）をとる。GWP値の意味を解釈するには、値のペアを見る必要がある：{GWP=1.0、PHASE=A1}、{GWP=15.0、PHASE=A3}などである。 *

⚠️ この機能はISO標準に由来するが、ソフトウェア実装でサポートされることはほとんどない。また、IFCは、1つのプロパティセットの下で同じ名前を持つ複数のプロパティに対応していません。データ辞書をより利用しやすくするために、接続プロパティを避けることを検討してください。

**動的プ ロ パテ ィ**（`Property` と`IsDynamic` と`DynamicParameterPropertyCodes` を使用） 「動的プ ロ パテ ィ に対す る 関数のパ ラ メ タ であ る プ ロ パテ ィ 」<sub>[ISO23386, 5.3.29]</sub>。言い換えれば、動的プロパティの値は、`DynamicParameterPropertyCodes` で指定されたプロパティの値に依存します。bSDD には、式の正確な式を機械的に解釈可能な形で定義するフィールドはない。 

ダイナミック・プロパティを使用すると、他のどのプロパティが特定のプロパティの値に影響を与えるかを知ることができます。

例*壁の「面積」は、その「高さ」と「長さ」によって決まる：A = H * L。*

⚠️ この機能はISO標準に由来するが、ソフトウェア実装でサポートされることはほとんどない。データ辞書をより利用しやすくするために、ダイナミック・プロパティを避けることを検討する。

<h3 id="restricting-property-values">Restricting property values</h3>

開発する🚧。  
`AllowedValues`...

`Min/MaxInc/Exclusive`...

`Pattern`...

<h3 id="identifying-bsdd-resources">Identifying bSDD resources</h3>

開発する🚧。  
`URI`...bSDDまたは外部で生成可能。

`Code`... [コードフォーマット](#code-format)参照。

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

&gt; 辞書コードと辞書バージョンの間のダッシュはスラッシュに置き換えられました：  
&gt; "URL0*"は "URL1*"になる  
&gt;   
&gt; 少なくとも）4ヶ月間は、辞書コードとバージョンの間のダッシュを使用したデータの供給と検索をサポートします。しかし、bSDD API が返すのは新しい形式の識別子だけであることに注意してください。

**2022-08 - 重要なお知らせ**

&gt; bSDD は、""URL0*"" から*始まる識別子（別名 "URI"）を "*"URL1*"" （"http" から "https"）に移行しているところである。これは、これらの識別子をハイパーリンクとしても使いやすくするためである。  
&gt;   
&gt; 古い "http "識別子を使用するサポートは、まもなく廃止されます！

📢 最新の技術アップデートについては、専用フォーラムのトピック（https://forums.buildingsmart.org/t/bsdd-tech-updates/4889）をご覧ください。
