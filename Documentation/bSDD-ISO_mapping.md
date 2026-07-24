# bSDDとISO規格間の属性対応表
**⚠️ このページは現在作成中のため、参考資料として使用しないでください ⚠️**

bSDDは、データディクショナリを定義するISO 12006-3およびISO 23386規格に基づいています。openBIMワークフローとの統合を容易にするため、bSDDは、建築環境を記述する相互に関連する用語やプロパティの定義という本質的な側面に絞り込まれています。 bSDDの制約には、指定された単位リスト、言語リスト、および概念間の関係の種類が含まれます（ISOは定義の自由度をユーザーに委ねているため、ソフトウェアによる解釈が妨げられています）。 ISO 12006-3の継承構造（ルート→オブジェクト→概念→主語／プロパティ）は、bSDDにおいて「クラス」と「プロパティ」の1レベルに簡略化されています。 

このISO規格では、各概念を個別にバージョン管理することが可能であり、これはデータディクショナリの開発において重要です。bSDDでは、契約上の合意を遵守するため、変更が行われるたびにディクショナリ全体の新しいバージョンが生成されます。ただし、ディクショナリが有効化されていない場合は、この限りではありません。[bSDDにおけるコンテンツのライフサイクル](bSDD%20import%20tutorial.md#the-lifecycle-of-a-dictionary)について、詳細はこちらをご覧ください。

以下は、bSDDとISO規格の属性を対応付けた表です。bSDDの属性は、[bSDDデータモデル](bSDD%20JSON%20import%20model.md)で定義されています。

| **bSDD** | **ISO 23386:2020** | **ISO 12006-3:2022** | **コメント** |
|---|---|---|---|
| プロパティ／クラス：Uid、 Uri | プロパティ／プロパティのグループ：グローバルに一意な識別子 | xtdRoot: UniqueId | _(G)UidはbSDDでは任意ですが、ISOでは必須です。bSDDでは、Uidの役割はURIに置き換えられており、Uidはそれを必要とするユースケースをサポートするためのみに存在します。URIを使用することで、プロパティのメタデータを閲覧することができます。_ |
| プロパティ／クラス／辞書：ステータス | プロパティ／プロパティのグループ：ステータス | ✖️ | _bSDDとISOには「Active」と「Inactive」があります。bSDDにはさらに「Preview」もあるため、ISOの機能を拡張しています。_ |
| （「辞書」の「ReleaseDate」を参照） | プロパティ／プロパティのグループ：作成日 | xtdObject: 作成日 | _bSDDでは、これは最初のバージョンの「ReleaseDate」の日付を指します。_ |
| プロパティ／クラス：   ActivationDateUtc | プロパティ／プロパティのグループ：有効化日 | ✖️ | _bSDDでは、ステータスが'Active'に変更された日付を指します。_ |
| （「辞書」の「ReleaseDate」を参照） | プロパティ／プロパティのグループ：最終変更日 | ✖️ | _bSDDでは、変更が行われたのは直近のバージョンの日付となります。_ |
| プロパティ／クラス：   RevisionDateUtc | プロパティ／プロパティのグループ：改訂日 | ✖️ |  |
| プロパティ／クラス：VersionDateUtc | プロパティ／プロパティのグループ：バージョンの日付 | ✖️ |  |
| プロパティ／クラス：   DeActivationDateUtc | プロパティ／プロパティのグループ：無効化日 | ✖️ | _bSDDでは、ステータスが'非アクティブ'に変更された日付を指します。_ |
| プロパティ／クラス：VersionNumber | プロパティ／プロパティのグループ：バージョン番号 | xtdObject: MajorVersion | _ISO 23386におけるバージョン番号は、ISO 12006-3におけるメジャーバージョンに相当します（同様に、リビジョン番号はマイナーバージョンに相当します）。 bSDDでは、属性の名称はISO 23386と同様ですが、バージョン番号にはすでに3つの数字（1.2.3）が含まれており、それぞれメジャー、マイナー、パッチを表しています（セマンティック・バージョニングの詳細については、https://semver.org/ をご覧ください）。_ |
| プロパティ／クラス：RevisionNumber | プロパティ／プロパティのグループ：リビジョン番号 | xtdObject: マイナーバージョン | _上の行を参照してください。bSDDではリビジョン番号は冗長ですが、特定のフィールドに対して何回リビジョンが行われたかを示すために使用することができます。_ |
| プロパティ／クラス：   ReplacedObjectCodes | プロパティ／プロパティのグループ：置換されたプロパティの一覧 | xtdObject: 置換されたオブジェクト |  |
| プロパティ／クラス：   ReplacingObjectCodes | プロパティ／プロパティのグループ：置換対象のプロパティの一覧 | ✖️ |  |
| プロパティ／クラス：非推奨の理由 | プロパティ／プロパティのグループ：非推奨の理由 | xtdObject: 非推奨の理由 |  |
| プロパティ／クラス：   CreatorLanguageIsoCode | プロパティ／プロパティのグループ：作成者の言語 | xtdConcept: 創造者の言語 | _ISO では、以下のプロパティを持つ xtdLanguage オブジェクト：EnglishName（ISO 639 シリーズに基づく）、NativeName、Comments、Code。bSDD では、以下のプロパティを持つ bSI 管理リスト：IsoCode、Name（https://api.bsdd.buildingsmart.org/api/Language/v1）_ |
| プロパティ／クラス：名前 | プロパティ／プロパティのグループ：言語 N での名称 | xtdObject: 名前 |  |
| プロパティ／クラス：定義 | プロパティ／プロパティのグループ：言語Nにおける定義 | xtdConcept：定義 |  |
| プロパティ：説明 | プロパティ：言語 N による説明 | xtdConcept：説明 |  |
| プロパティ：例 | プロパティ：言語Nにおける例 | xtdConcept：例 |  |
| プロパティ:   ConnectedPropertyCodes | プロパティ：関連するプロパティ | ✖️ |  |
| (スキーマ/API) | プロパティ：プロパティのグループ | ✖️ | _bSDDでは、プロパティはプロパティのグループ（クラスの一種）内に含まれることがあります。_ |
| プロパティ／クラス：   VisualRepresentationUri | プロパティ／プロパティのグループ：視覚的表現 | xtdConcept: 視覚的表現 | _ISOでは「Media」オブジェクトですが、bSDDでは外部の視覚的表現へのリンクのみが許可されています。_ |
| プロパティ／クラス：CountriesOfUse | プロパティ／プロパティのグループ：使用国 | ✖️ | _bSDDでは、bSIによって規定された事前定義済みのリストです。_ |
| プロパティ／クラス：   SubdivisionsOfUse | プロパティ／プロパティのグループ：用途の細分化 | ✖️ |  |
| プロパティ／クラス：原産国 | プロパティ／プロパティのグループ：原産国 | xtdConcept: 原産国 | _bSDDでは、bSIによって規定された事前定義済みのリストです。_ |
| プロパティ：PhysicalQuantity | 属性：物理量 | xtdProperty: QuantityKinds |  |
| プロパティ：ディメンション | プロパティ：ディメンション | xtdProperty: 次元 |  |
| プロパティ：MethodOfMeasurement | 特性：測定方法 | ✖️ |  |
| プロパティ：DataType | プロパティ：データ型 | xtdProperty: データ型 | _上記と同様ですが、bSDDが省略されています。実装を簡略化するため、XTD_RATIONALおよびXTD_COMPLEXを使用しています。_ |
| プロパティ: IsDynamic | プロパティ：動的プロパティ | ✖️ |  |
| プロパティ:   DynamicParameterPropertyCodes | プロパティ：動的プロパティのパラメータ | ✖️ |  |
| プロパティ：ユニット | プロパティ：ユニット | xtdProperty: 単位 | _ISOには、次のような項目があります：Dimension、Symbol、Coefficient、Scale、Base、Offset。bSDDでは、bSが管理するリスト「https://api.bsdd.buildingsmart.org/api/Unit/v1」があり、CodeとNameが含まれています。_ |
| ✖️ | プロパティ：定義値の名前 | ✖️ | _ISOにおける値の定義では、任意のカスタム属性をリストに追加しています。bSDDでは、これにより相互運用性が制限されることになります。_ |
| ✖️ | プロパティ：値の定義 | ✖️ | _ISOにおける値の定義では、任意のカスタム属性をリストに追加しています。bSDDでは、これにより相互運用性が制限されることになります。_ |
| ✖️ | プロパティ：許容誤差 | ✖️ | _ISO 23386：数値について、特定の単位が許容される変動範囲の合計値。これは、単位あたりの上限値と下限値の差である。_ |
| ✖️ | 特徴：デジタル形式 | ✖️ | _ISO 23386 では、これは数値テキスト型における精度と単位の組み合わせを指します。DataFormat パターンと混同しないでください。_ |
| プロパティ：TextFormat | プロパティ：テキスト形式 | ✖️ |  |
| プロパティ：AllowedValues | プロパティ：言語 N における取り得る値の一覧 | xtdProperty: 可能な値 | _ISO：「xtdProperty の値の説明」。ISO には「NominalValue」があるのに対し、bSDD には Description、Value、SortNumber、Uri、Code がある。_ |
| プロパティ：最大排他、最大包含、最小排他、最小包含 | プロパティ：境界値 | xtdProperty: BoundaryValues | _ISOのxtdIntervalオブジェクトには、Minimum、MinimumIncluded、Maximum、MaximumIncludedが含まれています。一方、bSDDでは、これと同じ機能を実現するために、MinExclusive、MinInclusive、最大排他、最大包含という個別の属性が用意されています。_ |
| PropertyRelation:   (RelationType == IsSynonymOf) | ✖️ | xtdConcept: SimilarTo | _IsSynonymOf"型の関係を用いて解決された bSDD において_ |
| (スキーマ/API) | ✖️ | xtdObject: 辞書 | _bSDDでは、プロパティは特定の辞書内に格納されています。_ |
| プロパティ／クラス：   DocumentReference | ✖️ | xtdConcept: 参照文書 | _ISO xtdExternalDocument では、bSDD では bSI の管理リストからの文字列：https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1_ |
| プロパティ／クラス：コード | ✖️ | ✖️ | _コードはURIを生成するために使用され、辞書内での識別にも利用できます。_ |
| プロパティ：DimensionLength | ✖️ | ✖️ |  |
| プロパティ：DimensionMass | ✖️ | ✖️ |  |
| プロパティ：DimensionTime | ✖️ | ✖️ |  |
| プロパティ： DimensionElectricCurrent | ✖️ | ✖️ |  |
| プロパティ:   DimensionThermodynamicTemperature | ✖️ | ✖️ |  |
| プロパティ：物質量 | ✖️ | ✖️ |  |
| プロパティ： DimensionLuminousIntensity | ✖️ | ✖️ |  |
| プロパティ／クラス: 所有Uri | ✖️ | ✖️ |  |
| プロパティ：パターン | ✖️ | xtdProperty: DataFormat | _プロパティ値のパターン。このパターンの意味は、実装に依存する。_ |
| プロパティ：PropertyValueKind | ✖️ | ✖️ | _bSDDでは：単一／範囲／リスト／複合／複合リスト_ |
| プロパティ：PropertyRelations | プロパティ：相互接続されたデータディクショナリにおけるプロパティ識別子の関係 | ✖️ |  |
| ClassProperty: IsRequired | ✖️ | ✖️ |  |
| ClassProperty: IsWritable | ✖️ | ✖️ |  |
| ClassProperty: 事前定義値 | ✖️ | ✖️ |  |
| ClassProperty: PropertyCode | ✖️ | ✖️ |  |
| ClassProperty:   PropertyUri | ✖️ | ✖️ |  |
| ClassProperty: PropertySet | ✖️ | ✖️ |  |
| ClassProperty: PropertyType | ✖️ | ✖️ | _bSDDにおける：プロパティ／依存関係_ |
| クラスプロパティ：SortNumber | ✖️ | ✖️ | _ISOにはxtdOrderedValueオブジェクトがあり、「値を、事前定義された値のリストにおけるその順序と関連付ける」ためのものです。bSDDでは、AllowedValuesにこのオプションのorder属性があります。_ |
| ClassProperty: シンボル | プロパティ：指定されたプロパティグループ内のプロパティのシンボル | xtdProperty: シンボル | _ISOには：記号、主題      bSDDでは：テキスト属性。_ |
| クラスプロパティ：単位 | ✖️ | ✖️ | _ClassProp については単数形、Property については複数形となります。詳細については'単位'の項を参照してください。_ |
| クラス関係 | GroupOfProperties: 相互に連携したデータ辞書内のプロパティ識別子のグループ間の関係 | ✖️ | _bSDDでは、関係を用いて解かれる。_ |
| クラス: ClassificationType | GroupOfProperties: プロパティグループのカテゴリ | ✖️ | _ISO 23386 の「GroupOfProperties」カテゴリと bSDD の「ClassType」の比較_ |
| クラス:   親分類コード | GroupOfProperties: プロパティの親グループ | ✖️ |  |
| クラス:   ClassificationProperties | ✖️ | xtdSubject: プロパティ |  |
| クラス: ClassificationRelations | ✖️ | xtdSubject: 関連する主題 |  |
| クラス: ReferenceCode | ✖️ | ✖️ |  |
| クラス:   RelatedIfcEntityNamesList | ✖️ | ✖️ | _IFCスキーマをカスタムクラスで拡張するというユースケースをサポートするため。_ |
| クラス：同義語 | ✖️ | ✖️ | _bSDD では、同義語を定義する方法が 2 つあります。それは、`that` 属性を使用する方法と、`"IsSynonymOf"` 型の関係を使用する方法です。_ |
| ✖️ | ✖️ | xtd件名：フィルター | _bSDDにおいても、リレーションは同様の役割を果たしますが、使いやすさを考慮して、「フィルター」の概念は実装されていません。_ |
| ClassRelation:   RelatedClassificationUri | ✖️ | ✖️ |  |
| ClassRelation:   関連する分類名 | ✖️ | ✖️ |  |
| ClassRelation: RelationType | ✖️ | ✖️ | _ISO 12006-3 の「xtdConcept/SimilarTo」を参照してください。_ |
| クラス関係：分数 | ✖️ | ✖️ | _ 関係を持つ分類に適用される総量（例：体積または重量）の割合を、任意で指定することができます。分類／関係タイプごとの割合の合計は、必ず1でなければなりません。_ |
| PropertyRelation:   RelatedPropertyName | ✖️ | ✖️ |  |
| PropertyRelation:   RelatedPropertyUri | ✖️ | ✖️ |  |
| PropertyRelation: RelationType | ✖️ | ✖️ |  |
| AllowedValue: コード | ✖️ | ✖️ | _コードはURIを生成するために使用され、辞書内での識別にも利用できます。_ |
| AllowedValue: 説明 | ✖️ | ✖️ |  |
| AllowedValue: Uri | ✖️ | ✖️ |  |
| AllowedValue: SortNumber | ✖️ | ✖️ |  |
| AllowedValue: 値 | ✖️ | ✖️ |  |
| 辞書: DictionaryCode | ✖️ | ✖️ | _コードはURIを生成するために使用され、組織内での識別にも利用できます。_ |
| 辞書: 辞書名 | ✖️ | ✖️ |  |
| 辞書:   DictionaryUri | ✖️ | ✖️ |  |
| 辞書: DictionaryVersion | ✖️ | ✖️ |  |
| 辞書: LanguageIsoCode | ✖️ | ✖️ |  |
| 用語集：ライセンス | ✖️ | ✖️ |  |
| 辞書: LicenseUrl | ✖️ | ✖️ |  |
| 辞書: MoreInfoUrl | ✖️ | ✖️ |  |
| 辞書：OrganizationCode | ✖️ | ✖️ |  |
| 用語集：品質保証手順 | ✖️ | ✖️ |  |
| 辞書:   品質保証手順URL | ✖️ | ✖️ |  |
| 辞書：ReleaseDate | ✖️ | ✖️ | _現在のバージョンの日付。_ |

## 単位
未定…

## ISO 23386 の「GroupOfProperties」カテゴリと bSDD の「ClassType」の比較
未定…

## 補足事項
- ISO 12006-3 によれば、すべての名称および定義について、英語での用語を記載することが義務付けられています。
