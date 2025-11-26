# bSDDとISO規格間の属性のマッピング
**⚠️ このページは進行中であり、参考のために使用しないでください ⚠️**

bSDDは、データ辞書を定義するISO12006-3とISO23386規格に基づいています。openBIMワークフローとの統合を容易にするため、bSDDは、建築環境を記述する相互に関連する用語とプロパティの定義という本質的な側面だけに絞られています。bSDDの制約には、単位リスト、言語リスト、概念間の関係の種類が含まれます（ISOはユーザーに定義の自由を委ねており、ソフトウェアによる解釈を妨げています）。ISO12006-3の継承構造（Root→Object→Concept→Subject/Property）は、bSDDでは1つのレベルに簡略化されている：クラスとプロパティである。 

ISOは、データ辞書の開発にとって重要な、各概念のバージョン管理を個別に許可している。bSDDでは、契約上の合意をサポートするために、各変更は完全な辞書の新しいバージョンとなる。これは、辞書が有効化されていない場合は適用されない。[bSDDにおけるコンテンツ・ライフサイクルの](https://github.com/buildingSMART/bSDD/blob/doc_update/Documentation/bSDD%20import%20tutorial.md)詳細を読む。

bSDD の属性は[bSDD データモデルで](https://github.com/buildingSMART/bSDD/blob/doc_update/Documentation/bSDD%20JSON%20import%20model.md)定義されている。 

| **<nobr>bSDD</nobr>** | **<nobr>ISO23386</nobr>:2020** | **<nobr>ISO12006-3</nobr>:2022** | **<nobr>コメント</nobr>** |
|---|---|---|---|
| プロパティ/クラス：Uid、Uri | Property/GroupOfProperties：グローバル一意識別子 | xtdRoot：ユニークID | _(G)UIDはbSDDではオプション、ISOでは必須。bSDDではUIDの役割はUriに置き換えられ、UIDはそれを必要とするユースケースをサポートするためだけのものである。   Uriは、プロパティのメタデータを見ることを可能にする。_ |
| プロパティ/クラス/辞書ステータス | プロパティステータス | ✖️ | _bSDDとISOには Active と Inactive があり、bSDDには Preview もある。_ |
| (辞書を参照: ReleaseDate) | プロパティ/グループ作成日 | xtdObject：作成日 | _bSDD では、これは最初のバージョンの ReleaseDate の日付である。_ |
| プロパティ/クラスアクティベーション日付 | プロパティ/グループ起動日 | ✖️ | _bSDDでは、ステータスが'Active'に変更された日付である。_ |
| (辞書を参照: ReleaseDate) | プロパティ/グループ最終変更日 | ✖️ | _bSDDでは、変更が発生した最後のバージョンの日付である。_ |
| プロパティ/クラスリビジョン日付 | プロパティ/グループ改定日 | ✖️ |  |
| プロパティ/クラスバージョン日付 | プロパティ/グループバージョン日付 | ✖️ |  |
| プロパティ/クラス   DeActivationDateUtc。 | プロパティ/グループ停止日 | ✖️ | _bSDDでは、ステータスが'Inactive'に変更された日付である。_ |
| プロパティ/クラスバージョン番号 | プロパティ/グループバージョン番号 | xtdObject：メジャーバージョン | _ISO23386におけるバージョン番号は、ISO12006-3におけるメジャーバージョンと同じである(同様に、リビジョン番号はマイナーバージョンである)。bSDD では、属性は ISO23386 のように命名されるが、バージョンはすでに 3 つの番号を含んでいる： 1.2.3 - Major, Minor and Patch (Semantic Versioningの詳細はhttps://semver.org/)。_ |
| プロパティ/クラスリビジョン番号 | プロパティ/グループリビジョン番号 | xtdObject：マイナーバージョン | _上の行を参照のこと。リビジョン番号は bSDD では冗長であるが、あるフィールドが何回リビジョンアップされたかを示すのに使用できる。_ |
| プロパティ/クラス置換オブジェクトコード | Property/GroupOfProperties：置換されたプロパティのリスト | xtdObject：置き換えられたオブジェクト |  |
| プロパティ/クラス   ReplacingObjectCodes | Property/GroupOfProperties：置換プロパティのリスト | ✖️ |  |
| プロパティ/クラス非推奨説明 | Property/GroupOfProperties：廃止の説明 | xtdObject：非推奨の説明 |  |
| プロパティ/クラス   CreatorLanguageIsoCode | プロパティ/グループ作成者の言語 | xtdConcept：作成者の言語 | _ISOではxtdLanguageオブジェクト：bSDD では、bSI 管理リスト：IsoCode, Name (https://api.bsdd.buildingsmart.org/api/Language/v1 ) を持つ bSI 管理リスト。_ |
| プロパティ/クラス名前 | Property/GroupOfProperties：言語名 N | xtdObject：名前 |  |
| プロパティ/クラス定義 | Property/GroupOfProperties：言語Nでの定義 | xtdConcept：定義 |  |
| プロパティ説明 | プロパティ言語Nでの説明 | xtdConcept：説明 |  |
| プロパティ例 | プロパティ言語Nでの例 | xtdConcept：例 |  |
| プロパティ   ConnectedPropertyCodes | プロパティ接続物件 | ✖️ |  |
| (スキーマ/API) | プロパティプロパティのグループ | ✖️ | _bSDD では、クラスプロパティはプロパティグループ（クラス型）の中にあることができます。_ |
| プロパティ/クラス   VisualRepresentationUri | Property/GroupOfProperties：視覚的表現 | xtdConcept：視覚表現 | _ISOではMediaオブジェクトだが、bSDDでは外部の視覚表現へのリンクのみが許される。_ |
| プロパティ/クラス使用国 | プロパティ/グループ使用国 | ✖️ | _bSDDでは、bSIによって管理される定義済みのリスト。_ |
| プロパティ/クラス用途地域 | プロパティ/グループのプロパティ：用途地域 | ✖️ |  |
| プロパティ/クラス原産国 | プロパティ/グループ原産国 | xtdConcept：原産国 | _bSDDでは、bSIによって管理される定義済みのリスト。_ |
| プロパティ物理量 | 特性物理量 | xtdProperty：数量 |  |
| プロパティ寸法 | プロパティ寸法 | xtdProperty：寸法 |  |
| プロパティ測定方法 | 特性測定方法 | ✖️ |  |
| プロパティDataType | プロパティデータ型 | xtdProperty：データ型 | _同じだが、bSDDがない。XTD_RATIONAL 、実装を簡単にするためにXTD_COMPLEX 。_ |
| プロパティIsDynamic | プロパティダイナミック・プロパティ | ✖️ |  |
| プロパティ   DynamicParameterPropertyCodes | プロパティ動的プロパティのパラメータ | ✖️ |  |
| 物件単位 | 物件単位 | xtdProperty：単位 | _ISOでは寸法、記号、係数、スケール、ベース、オフセット bSDD では bS 管理リスト: https://api.bsdd.buildingsmart.org/api/Unit/v1、コードと名前がある。_ |
| ✖️ | プロパティ：定義値の名前 | ✖️ | _ISOで値を定義することは、任意のカスタム属性でリストを拡張することである。bSDDでは、それは相互運用性を制限することになる。_ |
| ✖️ | プロパティ値の定義 | ✖️ | _ISOで値を定義することは、任意のカスタム属性でリストを拡張することである。bSDDでは、それは相互運用性を制限することになる。_ |
| ✖️ | プロパティ公差 | ✖️ | _ISO23386：数値の場合。特定の単位が変動することを許される総量。単位あたりの最大限界値と最小限界値の差。_ |
| ✖️ | プロパティデジタルフォーマット | ✖️ | _ISO23386では、デジタル・テキスト・タイプの精度と単位のペアである。DataFormatパターンと混同しないように。_ |
| プロパティテキストフォーマット | プロパティテキスト形式 | ✖️ |  |
| プロパティ許容値 | プロパティ：言語Nで取り得る値のリスト | xtdProperty：可能な値 | _ISO: 'xtdPropertyの値の説明'。ISOには'NominalValue'があるが、bSDDにはDescription, Value, SortNumber, Uri, Codeがある。_ |
| プロパティ最大排他、最大包含、最小排他、最小包含 | プロパティ境界値 | xtdProperty：境界値 | _ISO xtdInterval オブジェクトに含まれる：Minimum、MinimumIncluded、Maximum、MaximumIncluded。       bSDD では、最小排他(MinExclusive)、最小包含(MinInclusive)、最大排他(MaxExclusive)、最大包含(MaxInclusive)。_ |
| PropertyRelation：（RelationType == IsSynonymOf）。 | ✖️ | xtdConcept：類似 | _IsSynonymOf"型のリレーションで解決されるbSDDでは_ |
| (スキーマ/API) | ✖️ | xtdObject：辞書 | _bSDDでは、プロパティは特定の辞書に配置される。_ |
| プロパティ/クラス   DocumentReference | ✖️ | xtdConcept：参照ドキュメント | _ISO では xtdExternalDocument だが、bSDD では bSI 管理リストの文字列: https://api.bsdd.buildingsmart.org/api/ReferenceDocument/v1_ |
| プロパティ/クラスコード | ✖️ | ✖️ | _コードはUriを生成するために使用され、辞書内での識別に使用できる。_ |
| プロパティDimensionLength | ✖️ | ✖️ |  |
| プロパティDimensionMass | ✖️ | ✖️ |  |
| プロパティDimensionTime | ✖️ | ✖️ |  |
| プロパティ   DimensionElectricCurrent | ✖️ | ✖️ |  |
| プロパティ   DimensionThermodynamicTemperature | ✖️ | ✖️ |  |
| プロパティ物質量 | ✖️ | ✖️ |  |
| プロパティ   DimensionLuminousIntensity | ✖️ | ✖️ |  |
| プロパティ/クラス所有Uri | ✖️ | ✖️ |  |
| プロパティパターン | ✖️ | xtdProperty：データフォーマット | _プロパティ値のパターン。パターンの意味は実装に依存します。_ |
| プロパティPropertyValueKind | ✖️ | ✖️ | _bSDD 内：シングル/レンジ/リスト/コンプレックス/コンプレックスリスト_ |
| プロパティプロパティ関係 | プロパティ：相互接続されたデータ辞書内のプロパティ識別子の関係 | ✖️ |  |
| クラスプロパティ：IsRequired | ✖️ | ✖️ |  |
| クラスプロパティ書き込み可能 | ✖️ | ✖️ |  |
| クラスプロパティ：定義済み値 | ✖️ | ✖️ |  |
| クラスプロパティプロパティコード | ✖️ | ✖️ |  |
| クラスプロパティ：   PropertyUri | ✖️ | ✖️ |  |
| クラスプロパティプロパティセット | ✖️ | ✖️ |  |
| クラスプロパティ：PropertyType | ✖️ | ✖️ | _bSDDでは：プロパティ/依存_ |
| クラスプロパティソート番号 | ✖️ | ✖️ | _ISOにはxtdOrderedValueオブジェクトがあります："定義済みの値のリストにおける順序と値を結びつける"。bSDDのAllowedValuesは、このオプションの順序属性を持っています。_ |
| クラスプロパティシンボル | プロパティ：指定されたプロパティグループ内のプロパティのシンボル | xtdProperty：シンボル | _ISOではシンボル、サブジェクト bSDD では text 属性。_ |
| クラスプロパティ単位 | ✖️ | ✖️ | _ClassPropは単数形、Propertyは複数形。説明は'単位'を参照。_ |
| クラス関係 | GroupOfProperties：相互接続されたデータ辞書のプロパティ識別子のグループの関係。 | ✖️ | _リレーションで解くbSDDでは。_ |
| クラス：ClassificationType | GroupOfProperties：プロパティのグループのカテゴリ | ✖️ | _ISO23386 Category of GroupOfProperties vs bSDD ClassType を参照のこと。_ |
| クラス   ParentClassificationCode | GroupOfProperties：プロパティの親グループ | ✖️ |  |
| クラス   ClassificationProperties | ✖️ | xtdSubject：プロパティ |  |
| クラス分類関係 | ✖️ | xtdSubject：コネクテッド・サブジェクト |  |
| クラスReferenceCode | ✖️ | ✖️ |  |
| クラス関連IfcEntityNamesList | ✖️ | ✖️ | _IFC スキーマをカスタムクラスで拡張するユースケースをサポートする。_ |
| クラス類義語 | ✖️ | ✖️ | _bSDD で同義語を定義するには、その属性で定義する方法と、"IsSynonymOf" 型の関係で定義する方法がある。_ |
| ✖️ | ✖️ | xtd件名フィルター | _bSDDでは、リレーションは同じような役割を果たすが、使いやすさのためにFilterの概念は実装されていない。_ |
| クラス・リレーション関連ClassificationUri | ✖️ | ✖️ |  |
| クラス関連：関連分類名 | ✖️ | ✖️ |  |
| クラス・リレーション：RelationType | ✖️ | ✖️ | _ISO12006-3 の xtdConcept/SimilarTo を参照。_ |
| クラス関係分数 | ✖️ | ✖️ | _オプション関係を所有する分類に適用される、総量（体積または重量など）の端数の提供。分類／関係種別ごとの端数の合計は 1 でなければならない。_ |
| PropertyRelation：関連プロパティ名 | ✖️ | ✖️ |  |
| PropertyRelation：   RelatedPropertyUri | ✖️ | ✖️ |  |
| PropertyRelation：RelationType | ✖️ | ✖️ |  |
| 許容値コード | ✖️ | ✖️ | _コードはUriを生成するために使用され、辞書内での識別に使用できる。_ |
| 許容値説明 | ✖️ | ✖️ |  |
| AllowedValue：Uri。 | ✖️ | ✖️ |  |
| 許容値ソート番号 | ✖️ | ✖️ |  |
| 許容値：値 | ✖️ | ✖️ |  |
| 辞書辞書コード | ✖️ | ✖️ | _コードはUriを生成するために使用され、組織内の識別に使用できる。_ |
| 辞書辞書名 | ✖️ | ✖️ |  |
| 辞書辞書Uri | ✖️ | ✖️ |  |
| 辞書辞書バージョン | ✖️ | ✖️ |  |
| 辞書言語IsoCode | ✖️ | ✖️ |  |
| 辞書ライセンス | ✖️ | ✖️ |  |
| 辞書ライセンス | ✖️ | ✖️ |  |
| 辞書MoreInfoUrl | ✖️ | ✖️ |  |
| 辞書組織コード | ✖️ | ✖️ |  |
| 辞書品質保証手順 | ✖️ | ✖️ |  |
| 辞書品質保証手続きURL | ✖️ | ✖️ |  |
| 辞書リリース日 | ✖️ | ✖️ | _現在のバージョンの日付。_ |

## 単位
未定...

## ISO23386 Category of GroupOfProperties vs bSDD ClassType。
未定...

## 追記
- ISO12006-3によると、すべての名称/定義には英語表記が義務付けられている。
