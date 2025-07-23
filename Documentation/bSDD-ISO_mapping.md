# bSDDとISO規格間の属性のマッピング

**⚠️ このページは進行中であり、参考のために使用しないでください ⚠️**

bSDDは、データ辞書を定義するISO12006-3規格とISO23386規格に基づいています。 openBIMワークフローとの統合を容易にするため、bSDDは、建築環境を記述する相互に関連する用語とプロパティの定義という本質的な側面に絞られています。 bSDDの制約には、課される単位リスト、言語リスト、および概念間の関係のタイプが含まれます（ISOはユーザーに定義の自由を委ねており、ソフトウェアによる解釈を妨げています）。 ISO12006-3の継承構造（ルート→オブジェクト→概念→サブジェクト/プロパティ）は、bSDDではクラスとプロパティという1つのレベルに簡素化されています。 

bSDDでは、契約上の合意をサポートするために、各変更は完全な辞書の新しいバージョンになります。 辞書がアクティブ化されていない場合は、この限りではありません。 詳細を読む[bSDDにおけるコンテンツライフサイクル](https://github.com/buildingSMART/bSDD/blob/doc_update/Documentation/bSDD%20import%20tutorial.md).

以下は、bSDD と ISO 規格の属性をマッピングした表である。[bSDDデータモデル](https://github.com/buildingSMART/bSDD/blob/doc_update/Documentation/bSDD%20JSON%20import%20model.md). 

| **bSDD** | **ISO23386:2020** | **ISO12006-3:2022** | **どのように** |
|---|---|---|---|
| プロパティ/クラス: Uid, Uri | Property/GroupOfProperties: 世界的に一意な識別子 | xtdRoot: UniqueId | _(G)UIDは、bSDDではオプション、ISOでは必須である。 bSDDでは、UIDの役割はURIに置き換えられ、UIDはそれを必要とするユースケースをサポートするためだけのものである。 URIは、プロパティのメタデータを閲覧することを可能にする。_ |
| プロパティ/クラス/辞書: ステータス | プロパティ/プロパティグループ: Status | ✖️ | _bSDDとISOには "Active "と "Inactive "があり、bSDDには "Preview "もある。_ |
| (辞書を参照: ReleaseDate） | プロパティ/グループ・オブ・プロパティ：作成日 | xtdObject: 作成日 | _bSDD では、これは最初のバージョンの ReleaseDate の日付である。_ |
| プロパティ/クラス: ActivationDateUtc | Property/GroupOfProperties：起動日 | ✖️ | _bSDDでは、ステータスが'Active'に変更された日付である。_ |
| (辞書を参照: ReleaseDate） | プロパティ/グループ・オブ・プロパティ：最終変更日 | ✖️ | _bSDDでは、変更が発生した最後のバージョンの日付である。_ |
| プロパティ/クラス: RevisionDateUtc | Property/GroupOfProperties：改訂日 | ✖️ |  |
| プロパティ/クラス: VersionDateUtc | Property/GroupOfProperties：バージョン日付 | ✖️ |  |
| プロパティ/クラス: DeActivationDateUtc | Property/GroupOfProperties：無効化された日付 | ✖️ | _bSDDでは、ステータスが「Inactive」に変更された日付である。_ |
| プロパティ/クラス: VersionNumber | Property/GroupOfProperties：バージョン番号 | xtdObject: メジャーバージョン | _ISO23386におけるバージョン番号は、ISO12006-3におけるメジャーバージョンと同じです(同様に、リビジョン番号はマイナーバージョンです)。 bSDDでは、属性はISO23386のように命名されますが、バージョンにはすでに3つの番号が含まれています: 1.2.3 - メジャー、マイナー、パッチです(セマンティックバージョニングの詳細については、https://semver.org/ をお読みください)。_ |
| プロパティ/クラス: RevisionNumber | Property/GroupOfProperties: リビジョン番号 | xtdObject: マイナーバージョン | _リビジョン番号は bSDD では冗長だが、あるフィールドのリビジョンが何回行われたかを示すのに使われる。_ |
| プロパティ/クラス: ReplacedObjectCodes | Property/GroupOfProperties: 置換されたプロパティのリスト | xtdObject: 置換オブジェクト |  |
| プロパティ/クラス: ReplacingObjectCodes | Property/GroupOfProperties: 置換プロパティのリスト | ✖️ |  |
| プロパティ/クラス: DeprecationExplanation | Property/GroupOfProperties: 非推奨の説明 | xtdObject: 非推奨の説明 |  |
| プロパティ/クラス: CreatorLanguageIsoCode | Property/GroupOfProperties：クリエイターの言語 | xtdConcept: 作成者の言語 | _ISO では、xtdLanguage オブジェクトで、EnglishName （ISO 639 シリーズ準拠）、NativeName、Comments、Code を持つ。 bSDD では、bSI 管理リストで、IsoCode、Name （https://api.bsdd.buildingsmart.org/api/Language/v1 ）を持つ。_ |
| プロパティ/クラス: 名前 | Property/GroupOfProperties: N言語の名前 | xtdObject: 名前 |  |
| プロパティ/クラス: 定義 | Property/GroupOfProperties：言語Nでの定義 | xtdConcept: 定義 |  |
| 物件: 説明 | プロパティ：言語Nでの説明 | xtdConcept: 記述 |  |
| プロパティ: 例 | 特性：言語Nでの例 | xtdConcept: 例 |  |
| プロパティ: ConnectedPropertyCodes | プロパティ： 接続プロパティ | ✖️ |  |
| (スキーマ/API) | 物件：物件グループ | ✖️ | _bSDD では、クラスプロパティはプロパティグループ（クラス型）の中にあることができます。_ |
| プロパティ/クラス: VisualRepresentationUri | Property/GroupOfProperties：ビジュアル表現 | xtdConcept: ビジュアル表現 | _ISOではMediaオブジェクトだが、bSDDでは外部視覚表現へのリンクのみが許される。_ |
| プロパティ/クラス: CountriesOfUse | プロパティ/グループ・オブ・プロパティ：使用国 | ✖️ | _bSDDでは、bSIによって管理される定義済みのリスト。_ |
| プロパティ/クラス: SubdivisionsOfUse | 物件／物件グループ：用途の細分化 | ✖️ |  |
| プロパティ/クラス: CountryOfOrigin | Property/GroupOfProperties：原産国 | xtdConcept: 原産国 | _bSDDでは、bSIによって管理される定義済みのリスト。_ |
| プロパティ：PhysicalQuantity | 特性：物理量 | xtdプロパティ: QuantityKinds |  |
| プロパティ：寸法 | プロパティ：寸法 | xtdProperty: ディメンション |  |
| プロパティ: MethodOfMeasurement | 特性：測定方法 | ✖️ |  |
| プロパティ: DataType | プロパティ：データ型 | xtdProperty: データ型 | _同じだが、bSDDがない：実装を簡単にするためにXTD_RATIONALとXTD_COMPLEX。_ |
| プロパティ: IsDynamic | プロパティ: ダイナミック・プロパティ | ✖️ |  |
| プロパティ: DynamicParameterPropertyCodes | Property: 動的プロパティのパラメータ | ✖️ |  |
| 物件: ユニット | 物件: ユニット | xtdProperty: 単位 | _ISOでは、Dimension, Symbol, Coefficient, Scale, Base, Offsetがある。 bSDDでは、bSが管理するリスト： https://api.bsdd.buildingsmart.org/api/Unit/v1, CodeとNameがある。_ |
| ✖️ | プロパティ：定義値の名前 | ✖️ | _ISOで値を定義することは、カスタム属性でリストを拡張することになる。 bSDDでは、それは相互運用性を制限することになる。_ |
| ✖️ | プロパティ：値の定義 | ✖️ | _ISOで値を定義することは、カスタム属性でリストを拡張することになる。 bSDDでは、それは相互運用性を制限することになる。_ |
| ✖️ | 物件: 寛容 | ✖️ | _ISO23386: 数値の場合; 特定の単位が変動することを許容される総量。_ |
| ✖️ | プロパティ: デジタルフォーマット | ✖️ | _ISO23386では、デジタルテキスト型の精度と単位のペア。 DataFormatパターンと混同しないように。_ |
| プロパティ: TextFormat | プロパティ: テキスト形式 | ✖️ |  |
| プロパティ: AllowedValues | プロパティ：言語Nで取り得る値のリスト | xtdProperty: 可能な値 | _ISO: 'xtdPropertyの値の説明' ISOには'NominalValue'があるが、bSDDにはDescription, Value, SortNumber, Uri, Codeがある。_ |
| プロパティ：MaxExclusive、MaxInclusive、MinExclusive、MinInclusive | プロパティ：境界値 | xtdProperty: 境界値 | _ISOのxtdIntervalオブジェクトには、Minimum、MinimumIncluded、Maximum、MaximumIncludedが含まれる。 bSDDでは、MinExclusive、MinInclusive、MaxExclusive、MaxInclusiveが含まれる。_ |
| PropertyRelation： （RelationType == IsSynonymOf）。 | ✖️ | xtdConcept: SimilarTo | _IsSynonymOf "型の関係で解決されたbSDDにおいて_ |
| (スキーマ/API) | ✖️ | xtdObject: 辞書 | _bSDDでは、プロパティは特定の辞書に配置される。_ |
| プロパティ/クラス: DocumentReference | ✖️ | xtdConcept: 参照ドキュメント | _ISO では xtdExternalDocument だが、bSDD では bSI 管理リストの文字列: https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1_ |
| プロパティ/クラス: コード | ✖️ | ✖️ | _コードはURIを生成するために使用され、辞書内での識別に使用できる。_ |
| プロパティ: DimensionLength | ✖️ | ✖️ |  |
| プロパティ：DimensionMass | ✖️ | ✖️ |  |
| プロパティ: DimensionTime | ✖️ | ✖️ |  |
| プロパティ: DimensionElectricCurrent | ✖️ | ✖️ |  |
| プロパティ：DimensionThermodynamicTemperature | ✖️ | ✖️ |  |
| プロパティ：DimensionAmountOfSubstance | ✖️ | ✖️ |  |
| プロパティ: DimensionLuminousIntensity | ✖️ | ✖️ |  |
| プロパティ/クラス: OwnedUri | ✖️ | ✖️ |  |
| プロパティ: パターン | ✖️ | xtdProperty: データ形式 | _プロパティ値のパターン。パターンの意味は実装に依存します。_ |
| プロパティ: PropertyValueKind | ✖️ | ✖️ | _bSDD 内：シングル/レンジ/リスト/コンプレックス/コンプレックスリスト_ |
| プロパティ: プロパティ関係 | Property：相互接続されたデータ辞書内のプロパティ識別子の関係 | ✖️ |  |
| クラスプロパティ：IsRequired | ✖️ | ✖️ |  |
| クラスプロパティ：IsWritable | ✖️ | ✖️ |  |
| クラスプロパティ：定義済み値 | ✖️ | ✖️ |  |
| クラスプロパティ：プロパティコード | ✖️ | ✖️ |  |
| ClassProperty: PropertyUri | ✖️ | ✖️ |  |
| クラスプロパティ：プロパティセット | ✖️ | ✖️ |  |
| ClassProperty: PropertyType | ✖️ | ✖️ | _bSDDでは：プロパティ/依存_ |
| クラスプロパティ：ソート番号 | ✖️ | ✖️ | _ISOにはxtdOrderedValueオブジェクトがある："あらかじめ定義された値のリストの中で、値とその順序を結びつける"。 bSDDのAllowedValuesには、このオプションの順序属性がある。_ |
| クラスプロパティ：シンボル | Property：指定されたプロパティグループ内のプロパティのシンボル | xtdProperty: シンボル | _ISO は: シンボル、サブジェクト bSDD では: テキスト属性。_ |
| クラスプロパティ：単位 | ✖️ | ✖️ | _ClassPropは単数形、Propertyは複数形。 説明は「単位」を参照。_ |
| クラス関係 | GroupOfProperties: 相互接続されたデータ辞書のプロパティ識別子のグループの関係。 | ✖️ | _リレーションで解くbSDDでは。_ |
| クラス: ClassificationType | GroupOfProperties: プロパティ・グループのカテゴリー | ✖️ | _ISO23386 Category of GroupOfProperties vs bSDD ClassType を参照のこと。_ |
| クラス：ParentClassificationCode | GroupOfProperties: プロパティの親グループ | ✖️ |  |
| クラス: ClassificationProperties | ✖️ | xtdSubject: プロパティ |  |
| クラス: ClassificationRelations | ✖️ | xtdSubject: 接続されたサブジェクト |  |
| クラス: ReferenceCode | ✖️ | ✖️ |  |
| クラス: RelatedIfcEntityNamesList | ✖️ | ✖️ | _カスタムクラスでIFCスキーマを拡張するユースケースをサポートする。_ |
| クラス: 類義語 | ✖️ | ✖️ | _bSDD で同義語を定義するには、その属性で定義する方法と、"IsSynonymOf" タイプのリレーションで定義する方法がある。_ |
| ✖️ | ✖️ | xtd件名: フィルター | _bSDDでは、リレーションは同じような役割を果たすが、使いやすさのためにFilterの概念は実装されていない。_ |
| ClassRelation: RelatedClassificationUri | ✖️ | ✖️ |  |
| ClassRelation：関連分類名 | ✖️ | ✖️ |  |
| ClassRelation: RelationType | ✖️ | ✖️ | _ISO12006-3 の xtdConcept/SimilarTo を参照。_ |
| クラス関係：分数 | ✖️ | ✖️ | _関係を所有する「分類」に適用される、総量（体積や重量など）の端数をオプションで指定する。 分類／関係タイプごとの端数の合計は、1でなければならない。_ |
| PropertyRelation：関連プロパティ名 | ✖️ | ✖️ |  |
| PropertyRelation: RelatedPropertyUri | ✖️ | ✖️ |  |
| PropertyRelation: RelationType | ✖️ | ✖️ |  |
| 許容値： コード | ✖️ | ✖️ | _コードはURIを生成するために使用され、辞書内での識別に使用できる。_ |
| 許可される値: 説明 | ✖️ | ✖️ |  |
| 許容値: Uri | ✖️ | ✖️ |  |
| 許容値：ソート番号 | ✖️ | ✖️ |  |
| 許容値： 値 | ✖️ | ✖️ |  |
| 辞書: 辞書コード | ✖️ | ✖️ | _コードはURIの生成に使用され、組織内の識別に使用できる。_ |
| 辞書: 辞書名 | ✖️ | ✖️ |  |
| 辞書: DictionaryUri | ✖️ | ✖️ |  |
| 辞書: 辞書バージョン | ✖️ | ✖️ |  |
| 辞書: LanguageIsoCode | ✖️ | ✖️ |  |
| 辞書: ライセンス | ✖️ | ✖️ |  |
| 辞書: LicenseUrl | ✖️ | ✖️ |  |
| 辞書: MoreInfoUrl | ✖️ | ✖️ |  |
| 辞書：OrganizationCode | ✖️ | ✖️ |  |
| 辞書: 品質保証手順 | ✖️ | ✖️ |  |
| 辞書: QualityAssuranceProcedureUrl | ✖️ | ✖️ |  |
| 辞書: リリース日 | ✖️ | ✖️ | _現在のバージョンの日付。_ |

## Units
未定...

## ISO23386 Category of GroupOfProperties vs bSDD ClassType。
未定...

## 追記
- ISO12006-3によると、すべての名称/定義には英語表記が義務付けられている。
