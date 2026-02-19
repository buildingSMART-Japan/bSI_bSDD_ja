<h2 id="table-of-content">目次</h2>

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


<h2 id="data-model">データモデル</h2>

bSDDは、独立した組織によって発行されたデータ辞書（データ辞書とは何かについては以下をお読みください）の配布を容易にするためのサービスです。下の図は、bSDD の背後にある単純化されたデータモデルを示しています：

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_model.png" alt="bSDD entity diagram" style="width: 650px"/>

上記のコンセプトの使い方を示した例をご覧ください：[bSDDデータ例](https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png)：<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD_data_example.png" alt="bSDD entity diagram" style="width: 700px"/>


実演辞書もあります：["果物と野菜"](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.1)

📢 最新の技術アップデートについては、専用フォーラムのトピック[https://forums.buildingsmart.org/t/bsdd-tech-updates/4889](https://forums.buildingsmart.org/t/bsdd-tech-updates/4889)をご覧ください。

<h2 id="json-format">JSONフォーマット</h2>

buildingSMARTデータディクショナリのデータは、このドキュメントで説明する標準に従って、JSONファイルで納品することができます。JSONとExcelのテンプレートは、[/Model/Import Modelにも](https://github.com/buildingSMART/bSDD/tree/master/Model/Import%20Model)あります。

リンクをクリックすると、[国](https://api.bsdd.buildingsmart.org/api/Country/v1)、[言語](https://api.bsdd.buildingsmart.org/api/Language/v1)、[単位](https://api.bsdd.buildingsmart.org/api/Unit/v1)、[参照文書](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)、[ifc](https://api.bsdd.buildingsmart.org/api/Dictionary/v2/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3)クラスに使用できるコードの一覧が表示されます。  
参照ドキュメントが不足していると思われる場合は、[issueを投稿して](https://github.com/buildingSMART/bSDD/issues)お知らせください。JSON内の値は、数値の例およびAllowedValueフィールドを含め、すべて二重引用符で囲まれた文字列でなければなりません。

JSONに馴染みのない方は、[JSON入門を](https://javaee.github.io/tutorial/jsonp001.html)お読みになることをお勧めします。JSONは、コンピュータ・システムがデータを交換するためのフォーマットであることに注意してください。辞書データがコンピュータ・システムにある場合、システムにJSONを作成させるのが最善です。

<h2 id="list-of-fields">フィールド一覧</h2>

NB デフォルト値が適用されるのは、フィールドが指定されていない場合のみです。フィールド値に"NULLを"指定した場合、デフォルト値は適用されません。すべてのフィールドで"nullを"指定できるわけではないことに注意してください。

<h3 id="Dictionary">辞書</h3>

`Data dictionary`-*'意味、他のデータとの関係、起源の使用法、形式など、データに関する情報の一元化されたリポジトリ*'。[ISO23386]。*メタデータを含むデータベース*[ISO12006-3]。`Dictionary`(以前は`domain`)は、`Classes`(以前は`classifications`)と`Properties`構成され、これらは互いに関連するか、他の`Dictionaries`関連する可能性がある。`Dictionary`、以下の表に示すように、それに関する一般的なメタデータを含む。

| フィールド | データ型 | 必要ですか？ | 翻訳可能？ | 説明 |
|------------------|------------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="OrganizationCode">組織コード</span> | テキスト | ✅ |  | bSDD への登録時に受け取った組織のコード。あなたの組織がまだコードを持っていない場合は、[bSDD ユーザヘルプデスクで](https://bsi-technicalservices.atlassian.net/servicedesk/customer/portal/3/group/4/create/25)リクエストしてください。コードは、すべての URI リンクに表示されるため、できれば短いものにしてください。許可される文字については、[コード形式の](#code-format)項を参照のこと。このコードは数字で始まることはできない。コード例"ifc. |
| <span id="DictionaryCode">辞書コード</span> | テキスト | ✅ |  | 辞書のコード："ifc".[コード形式](#code-format)参照。 |
| <span id="DictionaryName">辞書名</span> | テキスト | ✅\* |  | 辞書の名前。\*辞書が存在する場合、この名前を指定する必要はない。 |
| <span id="DictionaryVersion">辞書バージョン</span> | テキスト | ✅ |  | 辞書データのバージョン。例：1.0.1。許容値："12" ", 10.1" ", 1.2.3".不可： 1."2.3.4"、"Beta"、"2x3"。私たちは、[セマンティック・バージョニング・アプローチに](https://semver.org/)従うことを推奨します。 |
| <span id="LanguageIsoCode">言語IsoCode</span> | テキスト | ✅ |  | ISO言語コード：データの言語を示す。複数の言語でデータを配信したい場合は、言語ごとにJSONファイルを使用してください。[言語](https://api.bsdd.buildingsmart.org/api/Language/v1)一覧参照。\* 例："de-DE" |
| <span id="LanguageOnly">言語のみ</span> | ブーリアン | ✅ |  | JSONが言語固有の情報のみを含む場合はtrue、そうでない場合はno。 |
| <span id="UseOwnUri">UseOwnUri</span> | ブーリアン | ✅ |  | デフォルト：false。クラスとプロパティをグローバルに一意に識別するために、独自のURIを使用します。独自の URI を使用しない場合、"https://identifier.buildingsmart.org" で始まる URI が各`Class` および`Property` |
| <span id="DictionaryUri">辞書Uri</span> | テキスト | ✅\* |  | UseOwnUri = trueの場合は必須。すべてのクラスおよびプロパティのURIの最初の部分である、グローバルに一意なURIを指定します：urn:mycompany:mydictionary または "https://mycompany.com/mydictionary" |
| <span id="License">ライセンス</span> | テキスト |  |  | コンテンツのライセンスの識別子。[Creative Commons](https://creativecommons.org/choose/)または[OSI Approved Licensesから](https://opensource.org/licenses/)ライセンスを選択することを推奨する。該当する場合、標準化された[SPDX](https://spdx.org/licenses/)識別子を正規の信頼できる識別のために使用する必要があります："MIT"または"CC-BY-4.0"。役に立つリソースは[ChooseALicense.com](https://choosealicense.com/)です。 |
| <span id="LicenseUrl">ライセンス</span> | テキスト |  |  | ライセンスの全文を掲載したウェブサイトへのリンク。ライセンスページは、提供された"ライセンス"名と一致する必要があります。 |
| <span id="ChangeRequestEmailAddress">ChangeRequestEmailAddress</span> | テキスト |  |  | ユーザーからの変更リクエストを受け取るための単一のメールアドレス。メールアドレスを提供することで、ユーザーからのリクエストを転送し、APIを通じてアドレスを公開することに同意するものとします。お客様は、当社に連絡することにより、情報を撤回する権利を有します。 |
| <span id="ModelVersion">モデルバージョン</span> | テキスト |  |  | 入力JSONテンプレートのバージョン番号。 |
| <span id="MoreInfoUrl">MoreInfoUrl</span> | テキスト |  |  | 辞書に関する詳細情報を含むウェブページへのURL |
| <span id="QualityAssuranceProcedure">品質保証手順</span> | テキスト |  |  | 辞書に使用される品質保証手順の名称または簡単な説明："ETIM international"、"AFNOR NF XP P07-150 (PPBIM)"、"bSI プロセス"、"UN GHS 2015"、"UN CPC 1.1"、"非公開"、"不明"。 |
| <span id="QualityAssuranceProcedureUrl">品質保証手続きURL</span> | テキスト |  |  | 品質保証手順に関する詳細情報を掲載したウェブページへの URL："https://www.buildingsmart.org/about/bsi-process" |
| <span id="ReleaseDate">リリース日</span> | 日時 |  |  | バージョンのリリース日。「[Date Time format](#datetime-format)」を参照。 |
| <span id="Status">ステータス</span> | テキスト |  |  | 可能なバージョンステータス：`Preview`、`Active` `Inactive` 。新しいバージョンをアップロードするときは、常に`Preview` である必要があります。その後、[API](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1)または[管理ポータルを介して](https://manage.bsdd.buildingsmart.org/)コンテンツをアクティブ化または非アクティブ化できます。続きを読む:[bSDDコンテンツのライフサイクル](https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/bSDD%20import%20tutorial.md#the-lifecycle-of-the-bsdd-dictionary-version) |
| <span id="Classes">クラス</span> | クラス一覧 | ✅ |  | `Class` 型のオブジェクトのリスト。[クラス](#class) |
| <span id="Properties">プロパティ</span> | 物件リスト | ✅ |  | `Property` 型のオブジェクトのリスト。[プロパティ](#property) |


\* 追加言語でデータを配信するためには、`Dictionary`タイプフィールド、すべての`Code`フィールド、および他のタイプの`Translatable?`=Yesと"マークされたフィールドを埋めるだけで十分である。`OrganizationCode`、`DictionaryCode`、`DictionaryVersion`まったく同じであることを確認し、データが既存の`Dictionary`言語を追加するためのものである場合は、`LanguageOnly`フィールドをtrueに設定する。

<h3 id="Class">クラス</h3>

`Class`-*"同じ特徴を共有するオブジェクトの集合の記述*"。[ISO23386]。`Class`、オブジェクト（例："壁"、"窓"）、抽象概念（例："時間"、"部屋"）、プロセス（例："設置"、"分解"）を指定できます。


| フィールド | データ型 | 必要ですか？ | 翻訳可能？ | 説明 |
|---------------------------|--------------------------------|-------------|-----------------|--------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト | ✅ |  | 辞書内のクラスの一意な識別。これは、IFCモデルで識別子として使用される情報です。例："abc-00123-01"または"SpecialWall"。コード・バリデーションが適用されます：[コード形式を](#code-format)参照してください。接頭辞"Ifc"は、IFC標準のために予約されています。 |
| <span id="Name">名称</span> | テキスト | ✅ | ✅ | `Class,` 例"IfcCurtainWall |
| <span id="ClassType">クラスタイプ</span> | テキスト | ✅* |  | 次のいずれかでなければならない：`Class`、`Material`、`GroupOfProperties`、`AlternativeUse`.[クラス・タイプの](#class-types)詳細はこちら。指定しない場合、デフォルトで`Class` タイプが使用されます。`ReferenceDocument` 、`ComposedProperty` 、`Dictionary` のタイプは非推奨となり、アップロード時に使用することはできませんが、移行期間中はAPI結果に表示されることがあります。 |
| <span id="Definition">定義</span> | テキスト |  | ✅ | `Class` の定義。意味的な意味を説明する。ISO に従った必須フィールド。[二重角括弧リンクを](#double-square-bracket-links)サポート。 |
| <span id="Description">説明</span> | テキスト |  | ✅ | 補足説明のための追加フィールド。*定義(Definition)*が規格に由来し、さらに説明が必要な場合にのみ使用してください。 |
| <span id="ParentClassCode">親クラスコード</span> | テキスト |  |  | 親への参照`Class` 。このフィールドのIDは、配信されたデータに存在しなければならない（MUST）。例"ifc-00123-00.[リレーションシップを定義するには？](#defining-relations) |
| <span id="RelatedIfcEntityNamesList">関連Ifcエンティティ名リスト</span> | テキスト一覧 |  |  | この`Class` の表現として使用するIFCクラスのコード。例えば['IfcWall'].bSDD API[ifcクラスを](https://api.bsdd.buildingsmart.org/api/Dictionary/v3/Classes?uri=https%3A%2F%2Fidentifier.buildingsmart.org%2Furi%2Fbuildingsmart%2Fifc%2F4.3%2F)参照してください。[リレーションシップを定義するには？](#defining-relations) |
| <span id="Synonyms">同義語</span> | テキスト一覧 |  | ✅ | 検索しやすいように、このクラスの代替名称のリスト。 |
| <span id="ActivationDateUtc">アクティベーション日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="ReferenceCode">参照コード</span> | テキスト |  |  | 参照コードは、辞書固有の用法を持つことができる。NULLの場合、`Code` の値がフィールドを埋めるために使用される。`ReferenceCode` を空にするには、空の文字列 を使用する。 |
| <span id="CountriesOfUse">使用国</span> | テキスト一覧 |  |  | この`Class` が使用されている国 ISO コードのリスト。参照リスト[国を](https://api.bsdd.buildingsmart.org//api/Country/v1)参照してください。 |
| <span id="CountryOfOrigin">原産国</span> | テキスト |  |  | この`Class` の原産国の ISO 国コード。参照リストの[国を](https://api.bsdd.buildingsmart.org//api/Country/v1)参照してください。 |
| <span id="CreatorLanguageIsoCode">CreatorLanguageIsoCode</span> | テキスト |  |  | 作成者の言語ISOコード。参照リストの[言語を](https://api.bsdd.buildingsmart.org/api/Language/v1)参照。 |
| <span id="DeActivationDateUtc">解除日Utc</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="DeprecationExplanation">非推奨説明</span> | テキスト |  | ✅ | 非推奨の定義のみを埋める。 |
| <span id="DocumentReference">ドキュメント参照</span> | テキスト |  |  | `Class` の完全な定義または正式な定義が記載された文書への言及。参考文献リストの[参考文献を](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)参照のこと。 |
| <span id="OwnedUri">所有Uri</span> | テキスト |  |  | ディクショナリ・レベルで`UseOwnUri = true` を指定した場合、グローバルに一意に識別するURIを指定する必要があります。`Class` |
| <span id="ReplacedObjectCodes">置換オブジェクトコード</span> | テキスト一覧 |  |  | このクラスが置き換えるクラス・コードのリスト |
| <span id="ReplacingObjectCodes">オブジェクトコードの置き換え</span> | テキスト一覧 |  |  | このクラスは以下のクラスコードで置き換えられる。 |
| <span id="RevisionDateUtc">リビジョン日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="RevisionNumber">リビジョン番号</span> | 整数 |  |  |  |
| <span id="Status">ステータス</span> | テキスト |  |  | `Class` のステータス：`Active` （デフォルト）または`Inactive` |
| <span id="SubdivisionsOfUse">用途地域</span> | テキスト一覧 |  | ✅ | 使用地域のリスト例"US-MT |
| <span id="Uid">Uid</span> | テキスト |  |  | URIだけでは不十分な場合のための一意な識別（ID）。 |
| <span id="VersionDateUtc">バージョン日付</span> | 日時 |  |  | デフォルトでは、インポートされた日付が使用されます。[Date Time formatを](#datetime-format)参照。 |
| <span id="VersionNumber">バージョン番号</span> | 整数 |  |  |  |
| <span id="VisualRepresentationUri">VisualRepresentationUri</span> | テキスト |  | ✅ |  |
| <span id="ClassProperties">クラスプロパティ</span> | クラスプロパティ一覧 |  |  | [ClassProperty](#ClassProperty)の項を参照。 |
| <span id="ClassRelations">クラス関係</span> | クラス関係一覧 |  |  | [クラス関係](#ClassRelation)参照 |

注：2023 年 11 月のリリース以降、マテリアルは個別に扱われなくなりました。`Material`、`Material`、`Class`なりました。

<h3 id="Property">プロパティ</h3>

`Property`- '*ある品物が本来持っている、あるいは後天的に獲得した特徴 [`Class`]'。例：熱効率、ヒートフロー、（...）、色*。[ISO23386]。  `Classes`、`Properties`割り当ては、中間の[ClassProperty](#ClassProperty)オブジェクトを通じて処理されます。 


| フィールド | データ型 | 必要ですか？ | 翻訳可能？ | 説明 |
|-------------------------------|--------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト | ✅ |  | 辞書内のプロパティの一意な識別。これは、IFCモデルで識別子として使用される情報です。例："abc-00123-01"または"ExternalArea"。コード・バリデーションが適用されます：[コード・](#code-format)フォーマットを参照してください。 |
| <span id="Name">名称</span> | テキスト | ✅ | ✅ | 物件名例"外部エリア |
| <span id="Definition">定義</span> | テキスト |  | ✅ | `Property` の定義。意味的な意味を説明する。ISO に従った必須フィールド。[二重角括弧リンクを](#double-square-bracket-links)サポート。 |
| <span id="Description">説明</span> | テキスト |  | ✅ | 補足説明のための追加フィールド。*定義(Definition)*が規格に由来し、さらに説明が必要な場合にのみ使用してください。 |
| <span id="DataType">データ型</span> | テキスト | ✅ |  | プロパティが表現されるデータ型。次のいずれかでなければならない： `Boolean`、`Character`、`Integer`、`Real`、`String` 、 `Time` |
| <span id="Units">単位</span> | テキスト一覧 |  |  | 単位コードのリスト。単位は、値を測定するための目盛りを表す (ISO 80000 または ISO 4217、あるいは ISO 8601)。bSDD[単位の](https://api.bsdd.buildingsmart.org/api/Unit/v1)参照リスト[(JSON)](https://api.bsdd.buildingsmart.org/api/Unit/v1)、または[単位の CSV テーブル](../DataFiles/units.csv)形式を参照。私たちは[QUDT](http://www.qudt.org/)単位の多くをサポートしていますが、もし足りない単位があれば、[issueとして単位のリクエストを投稿して](https://github.com/buildingSMART/bSDD/issues)ください。 |
| <span id="Example">例</span> | テキスト |  | ✅ | `Property`の例示値 |
| <span id="ActivationDateUtc">アクティベーション日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="ConnectedPropertyCodes">接続プロパティコード</span> | テキスト一覧 |  |  | 1つ以上の接続プロパティのコードのリスト。別の辞書のプロパティである場合は、コードの代わりに完全なURIを指定することもできる。[アセンブルプロパティを](#assembling-properties)参照。 |
| <span id="CountriesOfUse">使用国</span> | テキスト一覧 |  |  | この`Property` が使用されている国のISOコードのリスト。参照リスト[国を](https://api.bsdd.buildingsmart.org/api/Country/v1)参照してください。 |
| <span id="CountryOfOrigin">原産国</span> | テキスト |  |  | この`Property` の原産国の ISO 国コード。参照リストの[国を](https://api.bsdd.buildingsmart.org//api/Country/v1)参照してください。 |
| <span id="CreatorLanguageIsoCode">CreatorLanguageIsoCode</span> | テキスト |  |  | 作成者の言語ISOコード。参照リスト(JSON[)言語](https://api.bsdd.buildingsmart.org/api/Language/v1) |
| <span id="DeActivationDateUtc">解除日Utc</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="DeprecationExplanation">非推奨説明</span> | テキスト |  | ✅ |  |
| <span id="Dimension">寸法</span> | テキスト |  |  | 物理量の場合，ISO 80000-1 で定義されているように，[International_System_of_Quantities](https://en.wikipedia.org/wiki/International_System_of_Quantities) に従って寸法を指定する。その順序は，`length` ，`mass` ，`time` ，`electric current` ，`thermodynamic temperature` ，`amount of substance` ，`luminous intensity` である。例えば、速度（m/s）は"1 0 -1 0 0 0 0 と表記される。[IDSドキュメントの](https://github.com/buildingSMART/IDS/blob/ver/1.0.x/Documentation/UserManual/units.md)他の例 |
| <span id="DimensionLength">寸法長さ</span> | 整数 |  |  | 長さ寸法。`Dimension` フィールドを使用してすべての部品を指定するか、すべての部品を個別に指定する。 |
| <span id="DimensionMass">寸法質量</span> | 整数 |  |  | 質量寸法。`Dimension` フィールドを使用してすべての部品を指定するか、すべての部品を個別に指定する。 |
| <span id="DimensionTime">ディメンションタイム</span> | 整数 |  |  | Time ディメンジョン。フィールド`Dimension` を使用してすべての部分を指定するか、すべての部分を個別に指定する。 |
| <span id="DimensionElectricCurrent">寸法電流</span> | 整数 |  |  | ElectricCurrent（電流）ディメンジョン。`Dimension` フィールドを使用してすべての部分を指定するか、すべての部分を個別に指定する。 |
| <span id="DimensionThermodynamicTemperature">寸法熱力学温度</span> | 整数 |  |  | ThermodynamicTemperature（熱力学的温度）ディメンジョン。`Dimension` フィールドを使用して一部のディメンジョンを指定するか、すべてのディメンジョンを個別に指定する。 |
| <span id="DimensionAmountOfSubstance">物質量</span> | 整数 |  |  | AmountOfSubstance ディメンジョン。`Dimension` フィールドを使用してすべての部位を指定するか、すべての部位を個別に指定する。 |
| <span id="DimensionLuminousIntensity">寸法光度</span> | 整数 |  |  | LuminousIntensity ディメンジョン。`Dimension` フィールドを使用してすべての部分を指定するか、すべての部分を個別に指定する。 |
| <span id="DocumentReference">ドキュメント参照</span> | テキスト |  |  | `Property` の完全な、または公式な定義が記載された文書への参照。参照リスト (JSON)[参照文書を](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)参照のこと。 |
| <span id="DynamicParameterPropertyCodes">DynamicParameterPropertyCodes</span> | テキスト一覧 |  |  | 動的プロパティの関数のパラメータであるプロパティのコードのリスト。[プロパティの組み立てを](#assembling-properties)参照。 |
| <span id="IsDynamic">IsDynamic</span> | ブーリアン |  |  | デフォルト：`false` 。これが動的プロパティの場合、値はフィールド`DynamicParameterPropertyCodes` で与えられたパラメタに依存します。[プロパティの組み立てを](#assembling-properties)参照してください。 |
| <span id="MaxExclusive">最大排他</span> | リアル |  |  | 最大許容値、排他的 - 包含値と排他値の両方を記入しないこと |
| <span id="MaxInclusive">最大包含</span> | リアル |  |  | 最大許容値、包含値 - 包含値と排他値の両方を記入しないこと |
| <span id="MinExclusive">最小排他</span> | リアル |  |  | 最小許容値、排他的 |
| <span id="MinInclusive">最小包含</span> | リアル |  |  | 許容最小値（含む） |
| <span id="MethodOfMeasurement">測定方法</span> | テキスト |  | ✅ | 例"ISO 10077-1に準拠した熱貫流率 |
| <span id="OwnedUri">所有Uri</span> | テキスト |  |  | ディクショナリレベルで`UseOwnUri = true` を指定した場合には、 Property をグローバルに一意に識別する Uri を与える必要があります。 |
| <span id="Pattern">パターン</span> | テキスト |  |  | 許容値を制限するための[XMLスキーマ正規表現](https://www.regular-expressions.info/xml.html) |
| <span id="PhysicalQuantity">物理量</span> | テキスト |  | ✅ | 特性の物理量の名称、例："質量" "なし"または"質量" |
| <span id="PropertyValueKind">プロパティ値</span> | テキスト |  |  | `Single` （1つの値。これがデフォルト）、`Range` （2つの値）、`List` （複数の値）、`Complex` （単一/範囲/リストのいずれでもない。例えば、IfcActorのようなオブジェクトや、接続されたプロパティの集合体 -[プロパティの組み立てを](#assembling-properties)参照）、`ComplexList` （複合値のリスト）のいずれかでなければなりません。 |
| <span id="ReplacedObjectCodes">置換オブジェクトコード</span> | テキスト一覧 |  |  | この`Property` が置き換えるプロパティコードのリスト |
| <span id="ReplacingObjectCodes">オブジェクトコードの置き換え</span> | テキスト一覧 |  |  | このプロパティコードのリスト`Property` は次のように置き換えられる。 |
| <span id="RevisionDateUtc">リビジョン日付</span> | 日時 |  |  | [日付時刻のフォーマットを](#datetime-format)参照。 |
| <span id="RevisionNumber">リビジョン番号</span> | 整数 |  |  |  |
| <span id="Status">ステータス</span> | テキスト |  |  | プロパティの状態：`Active` （デフォルト）または`Inactive` |
| <span id="SubdivisionsOfUse">用途地域</span> | テキスト一覧 |  | ✅ | 使用地域のリスト例"US-MT |
| <span id="TextFormat">テキストフォーマット</span> | テキスト |  |  | テキスト種別（エンコーディング、キャラクタ数）のペアエンコーディングは IANA の"エンコーディング規格名（RFC " 2978）"に従って設定されます。 |
| <span id="Uid">Uid</span> | テキスト |  |  | URIだけでは不十分な場合のための一意な識別（ID）。 |
| <span id="VersionDateUtc">バージョン日付</span> | 日時 |  |  | デフォルトでは、インポートされた日付が使用されます。[Date Time formatを](#datetime-format)参照。 |
| <span id="VersionNumber">バージョン番号</span> | 整数 |  |  |  |
| <span id="VisualRepresentationUri">VisualRepresentationUri</span> | テキスト |  | ✅ |  |
| <span id="PropertyRelations">プロパティ関連</span> | PropertyRelationのリスト |  | ✅ | 関連するプロパティのリスト。[PropertyRelation](#PropertyRelation)参照。 |
| <span id="AllowedValues">許容値</span> | 許容値のリスト |  | ✅ | プロパティに許容される値のリスト。注意: boolean型のプロパティには使用しないでください。[AllowedValue](#AllowedValue) セクションを参照してください。 |


<h3 id="ClassProperty">クラスプロパティ</h3>

`Property`を、それが記述すべき`Class`に割り当てるための中間オブジェクト。各`Class`複数のプロパティを持つことができ、各`Property`多くの`Classes`一部になることができますが、1 つの`ClassProperty`は常に、1 つの`Class`1 つの`Property`ペアです。 

`ClassProperty`、単位、格納されるプロパティセット、および特定の`Class`適用される場合の値の制限を定義することによって、プロパティ'をさらに指定することができます。例えば、一般的な'温度'は摂氏または華氏で表すことができ、負の値でも正の値でもかまいませんが、室内空間に適用する場合は摂氏5度から40度の範囲に制限されるかもしれません。   


| フィールド | データ型 | 必要ですか？ | 翻訳可能？ | 説明 |
|---------------------|----------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト |  |  | `ClassProperty` の固有識別コード。コード・バリデーションが適用される：[コード形式](#code-format)。インポート時に空のままだと、bSDDはランダムなGUIDを生成する。 |
| <span id="PropertyCode">プロパティコード</span> | テキスト | ✅\* |  | 同じ`Dictionary` 内にある場合は`Property` への参照。\* PropertyCodeが使用されている場合は、PropertyUriを記入しないでください。 |
| <span id="PropertyUri">PropertyUri</span> | テキスト | ✅\* |  | `Property` が別の`Dictionary` にある場合の参照、例[：https://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3/prop/ClearWidth](https://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3/prop/ClearWidth) \* どちらか一方のみが必要であり、PropertyUri が使用中の場合は PropertyCode を記入しない。 |
| <span id="Description">説明</span> | テキスト |  | ✅ | クラス固有のプロパティの説明を指定することができます。省略された場合、該当するプロパティの'一般的な'説明が表示されます。 |
| <span id="PropertySet">プロパティセット</span> | テキスト |  |  | IFCデータで、プロパティを配置するセットの名前。接頭辞 'Pset_' は、公式のIFC のために予約されています。コード・バリデーションが適用されます：[コードフォーマット](#code-format)。続きを読む:[プロパティを組み立てる](#assembling-properties)。 |
| <span id="Unit">単位</span> | テキスト |  |  | ユニットのコード。Property 'Units'(リスト)とは異なり、この属性は単一の値を取る。[ユニットの](https://api.bsdd.buildingsmart.org/api/Unit/v1)参考リスト[（JSON）](https://api.bsdd.buildingsmart.org/api/Unit/v1)または[ユニットのCSVテーブルの](../DataFiles/units.csv)形式を参照してください。私たちは[QUDT](http://www.qudt.org/)ユニットの多くをサポートしていますが、もしユニットが見つからない場合は、[ユニットリクエストをissueとして投稿して](https://github.com/buildingSMART/bSDD/issues)ください。 |
| <span id="PredefinedValue">定義済み値</span> | テキスト |  |  | この`Property` の事前定義値。例:"IfcWall"クラスの場合、"IsLoadBearing"プロパティの値は"true"になります。 |
| <span id="IsRequired">必須</span> | ブーリアン |  |  | これが`Class`の必須`Property`であるかどうかを示す。 |
| <span id="IsWritable">書き込み可能</span> | ブーリアン |  |  | `Class` のこの`Property` の値を変更できるかどうかを示す。 |
| <span id="MaxExclusive">最大排他</span> | リアル |  |  | 最大許容値、排他的。`Property` に定義された値を上書きする。 'inclusive' および 'exclusive' 値の両方を記入してはならない。 |
| <span id="MaxInclusive">最大包含</span> | リアル |  |  | 最大許容値。`Property` に定義された値を上書きする。 'inclusive' と 'exclusive' の両方の値を記入してはならない。 |
| <span id="MinExclusive">最小排他</span> | リアル |  |  | 最小許容値、排他的。`Property` に定義された値を上書きする。 'inclusive' および 'exclusive' 値の両方を記入してはならない。 |
| <span id="MinInclusive">最小包含</span> | リアル |  |  | 最小許容値。`Property` に定義された値を上書きする。 'inclusive' および 'exclusive' 値の両方を記入してはならない。 |
| <span id="Pattern">パターン</span> | テキスト |  |  | 許容値を制限するための[XML Schema 正規表現](https://www.regular-expressions.info/xml.html)。Property に対して定義されたパターンを上書きします。 |
| <span id="OwnedUri">所有Uri</span> | テキスト |  |  | ディクショナリ・レベルで`UseOwnUri = true` を指定した場合は、ClassProperty をグローバルに一意に識別する URI を指定する必要があります。 |
| <span id="PropertyType">プロパティタイプ</span> | テキスト |  |  | `Class` の`Property` のタイプ：`Property` （デフォルト）または`Dependency` |
| <span id="SortNumber">ソート番号</span> | 整数 |  |  | この`Property` のソート番号。`Class` |
| <span id="Symbol">シンボル</span> | テキスト |  |  |  |
| <span id="AllowedValues">許容値</span> | 許容値のリスト |  | ✅ | `ClassProperty` の許容値のリスト。`Property` のために定義された値をオーバーライドします。 boolean タイプのプロパティには、この値を使用しないでください。[AllowedValue](#AllowedValue)参照。 |
| ~~外部プロパティUri~~ | ~~テキスト~~ |  |  | 廃止 - 代わりに`PropertyUri` を使用してください。 |


<h3 id="AllowedValue">許容値</h3>

`Properties`および`ClassProperties`列挙できるオプション値の列挙。例えば、Fire Rating'にはいくつかの値しか許されません：REI30、REI60、REI90、またはREI120です。

| フィールド | データ型 | 必要ですか？ | 翻訳可能？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="Code">コード</span> | テキスト | ✅ |  | コードは、値の一意な識別情報です。IFCモデルで識別子として使用される情報です。これは必須であり、ほとんどの場合、値と同じです。値やその説明の翻訳を可能にするために必要です。コードのバリデーションが適用されます：[コード・フォーマット](#code-format)。 |
| <span id="Value">価値</span> | テキスト | ✅ | ✅ | 値の名前：値の名前。これは主に翻訳用で、IFCモデルでは使用しません。 |
| <span id="Description">説明</span> | テキスト |  | ✅ | 値の説明 |
| <span id="Uri">Uri*。</span> | テキスト |  |  | * 所有Uriと重複するため、新モデルバージョンでは非推奨。 |
| <span id="SortNumber">ソート番号</span> | 整数 |  |  | その値が属する`Property` の値リストにおける値のソート番号。 |
| <span id="OwnedUri">所有Uri</span> | テキスト |  |  | 辞書レベルで`UseOwnUri = true` を指定した場合、AllowedValueをグローバルに一意に識別するURIを指定できます。 |

注:`AllowedValue`翻訳の追加はまだサポートされていません。

<h3 id="ClassRelation">クラス関係</h3>

`Classes`関係によってリンクすることができます。リレーションにはさまざまなタイプがあり、階層、合成、類似、参照の定義が可能です。[リレーションを定義するには?](#defining-relations)

| フィールド | データ型 | 必要ですか？ | 翻訳可能？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelationType">関係タイプ</span> | テキスト | ✅ |  | 次のいずれか： `HasMaterial`、`HasReference`、`IsEqualTo`、`IsSimilarTo`、`IsParentOf`、`IsChildOf`、`HasPart`、`IsPartOf`.[関係タイプについて](#relation-types)もっと読む。 |
| <span id="RelatedClassUri">関連クラスUri</span> | テキスト | ✅ |  | 関連する`Class` の完全 URI。`Dictionary` と同じでも異なっていてもかまいません。例： https://identifier.buildingsmart.org/uri/etim/etim/8.0/class/EC002987 |
| <span id="RelatedClassName">関連クラス名</span> | テキスト |  |  |  |
| <span id="Fraction">分数</span> | リアル |  |  | `HasMaterial` 関係にのみ適用される。オプションで、関係を所有するクラスに適用される総量（例：体積または重量）の端数を指定します。クラス/リレーションタイプごとの分数の合計は 1 でなければなりません。[IfcMaterialConstituent](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterialConstituent.htm)の Fraction に類似。 |
| <span id="OwnedUri">所有Uri</span> | テキスト |  |  | ディクショナリ・レベルで`UseOwnUri = true` を指定した場合は、ClassRelation をグローバルに一意に識別する URI を指定する必要があります。 |


<h3 id="PropertyRelation">プロパティ関係</h3>

`ClassRelations`に似ていますが、`Properties`間にあります。

| フィールド | データ型 | 必要ですか？ | 翻訳可能か？ | 説明 |
|--------------------------|----------|-----------|---------------|-----------------------------------------------------------------------------|
| <span id="RelatedPropertyName">関連プロパティ名</span> | テキスト |  |  | 関連サイト名`Property`. |
| <span id="RelatedPropertyUri">関連プロパティUri</span> | テキスト | ✅ |  | 関連する`Property` の完全 URI。それは同じでも異なっていてもよい`Dictionary` 。 |
| <span id="RelationType">関係タイプ</span> | テキスト | ✅ |  | 次のいずれか： `HasReference`、`IsEqualTo`、`IsSimilarTo`、~~IsParentOf, IsChildOf, HasPart~~.[関係タイプについて](#relation-types)もっと読む。 |
| <span id="OwnedUri">所有Uri</span> | テキスト |  |  | ディクショナリレベルで`UseOwnUri = true` を指定した場合、 PropertyRelation をグローバルに一意に識別する Uri を与えなければならない。 |

---

<h2 id="additional-explanations">補足説明</h2>

<h3 id="code-format">コード形式</h3>

(2024年4月以降) すべてのコードで、発音区分、空白、ドット、コンマ、ダッシュ、丸括弧、アンダースコア、数字が使用可能。特殊文字は使用できません： ```"#%/\:`{}[]|;<>?~```コードは大文字と小文字を区別しません。 

有効なコードの例としては、"bs-agri", "apple","éÄą _- (Д開発,...żź)"などがある。

コードは同じデータ辞書内で一意である必要があり、URIを生成するために使用される。

コードの長さは100文字まで。

例えば、IFC規格では、接頭辞'Ifc'と'Pset'で始まるコードが予約されている。 

<h3 id="class-types">クラスの種類</h3>

各クラスには特定のタイプが必要です。以下は、ISO 12006-3に従った、各タイプの意味の説明です：
* `Class` - 同じ特徴を共有するオブジェクトの集合の記述<sup>[ISO12006-3,3.7]</sup>。bSDD では最も一般的なタイプである。(例：壁、空間）
* `GroupOfProperties` - プロパティ・コレクションは、プロパティをあらかじめ整理または整頓できるようにするものである<sup>[ISO12006-3,3.14]</sup>。例えば、'environmental properties'など。[プロパティの組み立て](#assembling-properties)'を参照。
* `Material` - 物を作ることができる物理的な物質（例：鋼鉄、ガラス）
* `AlternativeUse` - を使用する[<sup>ISO12006-3,3.1]</sup>。
   * ほとんどのソフトウェア実装は、このクラス型を無視する。
* **DEPRECATED** ~~参照文書（ReferenceDocument） - 特定の情報を見つけるために参照される出版物。<sup>[iso12006-3,3.18]</sup>。参照文書は、データ辞書に存在するあらゆるデータと関連付けることができる。~~
  * bSDDでは、[参照として](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)使用できる最も一般的な規格を含む[参照](https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1)文書のグローバルリストを用意している。これは、異なるネーミングの参考文献が重複しないようにするためです。もしお探しの参考文献が見つからず、リストに加えるべきだとお考えでしたら、ぜひお知らせください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).
* **DEPRECATED** ~~ComposedProperty - (...) 複数のプロパティを定義する必要があるフィーチャーに対応する。<sup>[iso12006-3,3.8]</sup>。~~
  * ~~例"コンクリートの"特徴的な"表面品質を"表現するためには、コンクリートの平面性、コンクリートの色相、コンクリートの質感という3つの特性を表現することが必須である。~~
  * 代わりに`GroupOfProperties` 。

<h3 id="defining-relations">関係の定義</h3>

`ParentClassCode`-`Class` 同じ辞書内の、ツリーのような階層構造で編成できます。例えば「IfcPile」は、「IfcDeepFoundation」のより具体的なクラスです。bSDDの用語では、IfcDeepFoundation"は "IfcPile"**の親**であると言います。このような特殊化関係を定義するには、子オブジェクトの`ParentClassCode`属性を使用します。


`ClassRelation`と`PropertyRelation` これらを使って、概念同士をリンクします。関係によって、他の辞書との親子リンクを定義することもできます。特殊化とは別に、分解 (`HasPart`タイプ、可能なタイプのリスト:[リレーション・タイプを](#relation-types)参照) のような他のタイプのリレーションを定義することもできます。

`RelatedIfcEntityNamesList`-IFCは、ソフトウェア間の情報交換に使用されるトップレベルのスキーマ (基礎クラス) です。そのため、bSDD は、あなたのクラスをIFC_PH_1804D42C に関連付けるための特別な方法を提供しています。`RelatedIfcEntityNamesList`使用して、IFCのどのエンティティを参照または拡張しているかを示します。たとえば、「信号LEDダイオード」は、IFCの「IfcLamp」に関連しています。 `RelatedIfcEntityNamesList`、bSDD 関連ツールで使用することができ、特定のIFCカテゴリにクラスのリストを絞り込むことができます。

<h3 id="relation-types">関係タイプ</h3>

`Properties`、`Classes`互いに関連付けることができます。各関係は、ソフトウェアが解釈できるように、特定の型を持たなければなりません。以下は、それぞれの型が意味することの説明です：
* <span id='IsEqualTo'>`IsEqualTo`</span> - 2つの概念が明確で、同じ名前、コード、定義、説明を持っている場合。クラスもまた、同じクラス・プロパティを共有する必要がある。概念が同じであることは非常にまれです。使い方の例としては、ある概念に公式な翻訳がないにもかかわらず、誰かがその概念を新しい言語で新しい辞書を定義し、元の概念とまったく同じであると言いたい場合です。(私たちは常に、重複する辞書を作成する代わりに、元のデータ辞書に翻訳や改良を提案することを推奨します）。
* <span id='IsSimilarTo'>`IsSimilarTo`</span> - 2つの概念がほぼ等しいが、名前、コード、定義、説明、またはクラス・プロパティのセットによって異なる場合。これは非常に一般的な関係タイプです。例えば、IfcWall'は、CCIの'ウォール・システム'と類似した概念であると言う場合に使用されます。このようなリレーションシップの欠点は、類似性のレベルがわからないことです。
* <span id='HasReference'>`HasReference`</span> - 2つの概念が互いに関連しているが、他の関係タイプが適用されない場合。例えば、"壁掛けランプ"（または"燭台）は壁を参照している。たとえ、それらは異なる概念であり、それらの間に階層がなくても。
* **DEPRECATED** ~~IsSynonymOf - 二つの概念が同一であるが、名前が異なる場合。~~

クラスにのみ適用される（プロパティには適用されない）：
* <span id='IsChildOf'>`IsChildOf`</span> - 特殊化関係。"サブタイプ"関係<sup>[ISO12006-3, F3.1]</sup> に相当する。例えば"電気モーターと" "燃焼モーターは"、総称概念"Motor の子（サブタイプ）である。
* <span id='IsParentOf'>`IsParentOf`</span> - `IsChildOf` とは逆の関係である。
* <span id='HasPart'>`HasPart`</span> - 構成関係。例えば、電動機はステータ、ロータなどの要素で構成される。[<sup>ISO12006-3, f3.2]</sup>。
* <span id='IsPartOf'>`IsPartOf`</span> - `HasPart` の逆。
* <span id='HasMaterial'>`HasMaterial`</span> - 特定の素材に関連付けられるクラス。例えば"Steel Beamは"材料"Steelに"関連する。

<h3 id="datetime-format">日付形式</h3>

ISO 8601シリーズに従った日付時刻形式を使用すること： `YYYY-MM-DDThh:mm:ssTZD`。インポートでは、`2023-05-10`、`2023-05-10T15:10:12Z`、`2023-05-10T15:10:12+02:00` の両方を使用できます。

<h3 id="property-inheritance">財産相続</h3>

* 親`Class`→ 子`Class`子`Class`、親`Class`プロパティを継承しません。子クラスにも親クラスのプロパティを持たせたい場合は、インポート・ファイルで意図的に指定する必要があります。例えば、[IfcWall](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall)は[IfcWallStandardCase](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWallStandardCase) の親クラスです。[IfcWallには](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall) [AcousticRatingという](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall/prop/Pset_WallCommon/AcousticRating)プロパティがありますが、[IfcWallStandardCaseには](https://search.bsdd.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWallStandardCase)ありません。



* `Property`→`ClassProperty`、`ClassProperty`は、特定の`Class` に対する一般的な`Property`のインスタンス化です。`AllowedValue`最小/最大制限などのプロパティの属性は、デフォルトで`ClassProperty`渡されます。`ClassProperty`値は、オリジン`Property`影響を与えることなく変更することができます。例えば、[Height](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/prop/height)の上限は 100 cm です。Apple"クラスに適用すると、[Apple-Heightの](https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/class/apple/prop/SizeSet/height)下限は25cmになります。



<h3 id="latest-version">最新バージョン</h3>

bSDDでは、すべてのリソースはURIという一意の識別子を持ちます。URIは、他の情報の中で、組織のコード、辞書とバージョン番号を含んでいます。例えば、.../uri/bs-agri/fruitvegs/1.**0.0/class/fruit** 特定のリソースを参照したいが、バージョンがわからない、あるいは、常に最新のバージョンを参照したい場合、私たちは"最新の"機能を実装しました。今、バージョン番号の代わりに"latest"を使うことが可能で、 bSDD はそのリソースを含む最新のアクティブバージョンまたはプレビューバージョンへのリンクを解決します: ...**/uri/bs-agri/fruitvegs/latest/class/fruit**.



<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/latest_example.jpg" alt="bSDD latest" style="width: 750px"/>

https://search.bsdd.buildingsmart.org/uri/bs-agri/fruitvegs/latest/class/fruit。


⚠️ latestは"最新のリソースを指し、新しいバージョンが存在すると変更されることを意味する。これは不変のUriではなく、内容が変わる可能性があるため、注意して使用してください。契約上の合意には、特定のバージョン番号を使うことをお勧めします。

<h3 id="assembling-properties">組み立て特性</h3>

`Class`使用。`ClassType`:`GroupOfProperties`"プロパティをあらかじめ並べたり、整理したりすることを可能にするコレクション" <sup>[ISO12006-3,3.14]</sup>。bSDD では、複数の Properties をグループ化するための Type of Class として実装されている。

データ辞書内のプロパティを整理するには、プロパティのグループを使用します。

例：*'[LCA指標とモジュール](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0)'の'[地球温暖化係数](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/class/GlobalWarmingPotential)'クラスは、4つのプロパティをグループ化している：[合計](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total)'、'[生物起源](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_biogenic)'、'[化石燃料](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_fossil)'、'[土地利用](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_luluc)*。

**プロパティを** `ClassProperty``PropertySet`- グループ化するためのIFC標準の概念です。bSDD では、Class Property のために定義されたテキスト・フィールドとして表され、IFCデータにシリアル化されたときに、このクラス・プロパティがどのセットに表示されるべきかを示します。 
  * ISO 16739-1で定義されるプロパティセットはプロパティのグループであるが、プロパティのグループは必ずしもプロパティセットではない。
  * プロパティは、複数のプロパティ・グループのメンバになることができます。クラス・プロパティは、複数のプロパティ・セットのメンバになることはできません。
  * 接頭辞'Pset_'は、公式のIFCにのみ予約されています。

IFCデータセットのどこにプロパティを配置するかを定義するには、Property Set を使用します。

例*例：'IfcWall'のプロパティ'Concrete Cover'はプロパティセットにあります：Pset_ConcreteElementGeneral' にあります*。

`Property``ConnectedPropertyCodes` "カレントプロパティに連結されているプロパティのリスト。接続は、特殊化または依存であることができます。" <sub>[iso12006-3、5.3.29]</sub>。

あるプロパティの値が他のプロパティの値に依存する場合は、Connected Propertiesを使用します。

例*例：['地球温暖化係数-合計'（GWP）](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/GWP_total)プロパティは、製品のライフサイクルの各フェーズに対して定義されるべきである。各フェーズ（GWP_A1, GWP_A2、...）に個別にプロパティを定義することは望ましくない。その代わりに、GWP_A1, GWP_A2, ...は、別のプロパティである'[情報モジュール（PHASE）](https://search.bsdd.buildingsmart.org/uri/LCA/LCA/3.0/prop/information_module)'に接続され、18の可能な値（A1, A2, C3...）をとる。GWP値の意味を解釈するには、値のペアを見る必要がある：{GWP=1.0、PHASE=A1}、{GWP=15.0、PHASE=A3}などである*。 

⚠️ この機能は ISO 標準に由来しますが、ソフトウェア実装でサポートされることはほとんどありません。また、IFCは、 1 つのプロパティセットの下で同名の複数のプロパティに対応していません。データ辞書をより利用しやすくするために、接続プロパティを避けることを検討してください。

**動的プロパティ** `Property` を使用。`IsDynamic`および .`DynamicParameterPropertyCodes`"動的プロパティの関数のパラメータであるプロパティ" <sub>[ISO23386, 5.3.29]</sub>。言い換えれば、動的プロパティの値は、`DynamicParameterPropertyCodes`指定されたプロパティの値に依存する。bSDDには、機械的に解釈可能な形で式の正確な式を定義するフィールドはありません。 

ダイナミック・プロパティを使用すると、他のどのプロパティが特定のプロパティの値に影響を与えるかを知ることができます。

例*壁の'面積'は、その'高さ'と'長さ'によって決まる：A = H * L*。

⚠️ この機能はISO標準に由来するが、ソフトウェア実装でサポートされることはほとんどない。データ辞書をより利用しやすくするために、ダイナミック・プロパティを避けることを検討する。

<h3 id="double-square-bracket-links">ダブルスクエアブラケットリンク</h3>
同じ辞書から他のリソースを参照するには、二重の角括弧を使用します。クラスとプロパティの両方に同じコードが存在する場合、ハイパーリンクはクラスを指します。コードが見つからない場合、角括弧は省略されます。API は、定義を角括弧付きで返します。 

<h2 id="notifications">お知らせ</h2>

**2023-07 - 重要なお知らせ**

> 辞書コードと辞書バージョンの間のダッシュはスラッシュに置き換えられました：辞書コードと辞書バージョンの間のダッシュは、スラッシュに置き換えられました。 &gt; 例: &gt; https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs-1.0.0/class/apple は、現在 https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.0.0/class/apple &gt; &gt; 私たちは、(少なくとも)4ヶ月間、辞書コードとバージョンの間のダッシュを使用したデータの供給と検索をサポートします。しかし、新しい形式の識別子だけがbSDD APIによって返されることに注意してください。




**2022-08 - 重要なお知らせ**

> bSDD は、"http://identifier.buildingsmart.org" "で始まる識別子 (別名"Uri")"から https://identifier.buildingsmart.org" (http から https) に移行する過程にある。これは、これらの識別子をハイパーリンクとしても使いやすくするためである。&gt; 古い"http"識別子を使用するサポートはまもなく廃止される予定です！



📢 最新の技術アップデートについては、専用フォーラムのトピック（https://forums.buildingsmart.org/t/bsdd-tech-updates/4889）をご覧ください。
