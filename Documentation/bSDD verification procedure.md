# The bSDD Verification Procedures

While the bSDD service is governed by buildingSMART International, the content of the bSDD is governed by independent organisations -- data dictionary owners. To ensure quality, the bSDD content undergoes the following verification procedures: 

| **タイプ** | **いつ** | **誰が** | **コスト** | **何** |
|---------------------------|------------------|-----------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **組織の見直し** | 登録時 | bSIチーム | 無料 | それぞれの新しい組織は、その目的がbSDDの使命に合っているかどうかを確認するために審査される。 |
| **インポート検証** | アップロード | 自動化 | 無料 | bSDDアップロード毎に自動ステップを起動し、bSDDデータ構造への準拠を検証。 |
| **ユーザー／反響レビュー** | ユーザーからのリクエスト | コミュニティ＆bSIチーム | 無料 | bSDD のユーザは、コンテンツ所有者と bSDD チームに問題を報告したり、改善を提案したりするために、「変更要求」を提出することができる（ISO 12006-3:2022 に準拠）。 bSDD チームは、ライセンス違反に関する報告を調査する。 |
| **詳細な検証** | オーナーの要望による | bSIチームまたは代表者 | 有料 | コンテンツの品質を保証するためのオンデマンド有料サービス。 bSDDプラットフォーム内のデータの信頼性を高めるように設計されている。 手順は[チェックリスト](#detailed-verification-checklist)に記述されている。 |

\* The cost of the verification procedure depends on the amount of content, number of iterations, and complexity of the data dictionary. The service price is determined individually - please get in touch with the bSDD Team for a quote: [CONTACT FORM](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h?__hstc=265579920.1c41677ee7e38ddbd3a5a993f3a67a91.1729689591361.1738077297342.1738084047841.83&__hssc=265579920.2.1738084047841&__hsfp=2763741192).

> Disclaimer: the verification checklist is not exhaustive — additional aspects may be verified. The checklist might also change over time to enhance quality. To obtain a 'verified badge', a data dictionary must comply with the latest version of the checklist.


## Detailed verification checklist

| コード | 項目 | コード | 項目 |
|-------------------|---------------------------------------------|-------------------|--------------------------------------------------|
| [GEN-01](#gen-01) | 必須項目 | [CLS-03](#cls-03) | クラスの階層 |
| [GEN-02](#gen-02) | 英語版があること | [CLS-04](#cls-04) | シンクレティックなクラスは避ける |
| [GEN-03](#gen-03) | 翻訳は正確でなければならない | [CLS-05](#cls-05) | 禁止接頭辞 'Ifc' |
| [GEN-04](#gen-04) | 名称は明確で解釈しやすいものでなければならない | [PRP-01](#prp-01) | 数値プロパティのメタデータ |
| [GEN-05](#gen-05) | 一貫した命名規則に従う | [PRP-02](#prp-02) | IFCプロパティの重複を避ける |
| [GEN-06](#gen-06) | 正しいタイプの使用 | [PRP-03](#prp-03) | 禁止接頭辞 'PSET_' |
| [GEN-07](#gen-07) | データ辞書のガバナンス | [PRP-04](#prp-04) | プロパティの適切なデータ型 |
| [GEN-08](#gen-08) | 所有権の確認 | [PRP-05](#prp-05) | シングル・アスペクト物件 |
| [GEN-09](#gen-09) | 循環的な定義を避ける | [PRP-06](#prp-06) | 不必要な許容値を避ける |
| [GEN-10](#gen-10) | 不正確な定義を避ける | [PRP-07](#prp-07) | 許容される値は意味のあるものでなければならない |
| [GEN-11](#gen-11) | 否定的な定義は避ける | [CPR-01](#cpr-01) | ClassPropertyでは、アクティブなbSDDプロパティのみを使用する。 |
| [GEN-12](#gen-12) | 独自のURIは情報を提供しなければならない | [CPR-02](#cpr-02) | ClassPropertyはPropertySet名を持つべきである。 |
| [DCT-01](#dct-01) | 辞書は'Active'でなければならない | [REL-01](#rel-01) | RelationTypeの循環関係を避ける |
| [DCT-02](#dct-02) | 辞書名は誤解を招くものであってはならない | [REL-02](#rel-02) | RelationTypeの不正なクラス型を避ける |
| [CLS-01](#cls-01) | クラスはIFCに正しくマッピングされるべきである。 | [REL-03](#rel-03) | 関係は有意義でなければならない |
| [CLS-02](#cls-02) | 循環的な依存関係を避ける |  |  |

**GEN (General), DCT (Dictionary), CLS (Class), PRP (Property), ALV (AllowedValue), CPR (ClassProperty), REL (Relations)*

## General

### GEN-01 
**Required fields**

While it is possible to publish in bSDD without some fields filled, the requirements for verification are set higher. The dictionary, classes and properties must at least provide the fields from both rows below correspondingly: 

|  | 辞書 | クラス | プロパティ |
| ----- | ----- | ----- | ----- | 
| bSDDによって要求される | `OrganizationCode`、`DictionaryCode`、`DictionaryName`、`DictionaryVersion`、`LanguageIsoCode` | `Code`, `Name`, `ClassType` | `Code`, `Name`, `DataType` |
| 検証のための追加要件 | `QualityAssuranceProcedure`, `ChangeRequestEmailAddress`, `License`, `LicenseUrl` | `定義`, `RelatedIfcEntityNamesList` | `Definition`、`Example`、`Dimension`（数値の場合）、`PropertyValueKind` |

Additionally, `ClassProperty` should have a value of its `PropertySet`.

### GEN-02
**Must have English version**

As per ISO 12006-3:2022, the dictionary should include an English version of all the relevant content for all translatable fields. See bSDD documentation for a list of translatable fields. The existence of other language translations is optional.

### GEN-03
**Translations should be accurate**

The translations are optional, but when they exist, all the translations should be precise and faithful to the original content. Translations can not extend the explanations or remove any part of the original sentences. 

Example:

| ENG（オリジナル） | ドイツ語（翻訳） |  |
| ---- | ----- | ----- |
| _壁とは、空間を区切ったり、分断したりする垂直の建造物を意味する。_ | _部屋を分離または分割するための垂直構造... 注：ISO 6707-1によると、垂直構造は、通常、石積みまたはコンクリートで作られています。_ | ❌ FAIL: ドイツ語訳にはISOに言及する文が追加されている。 |

### GEN-04
**Names should be clear and easy to interpret**

Unlike codes, the name of each item must be clear and help users understand the concept to enhance usability.

Notes:

- Avoid adding prefixes to each item in the dictionary, as this can complicate search and filtering.
- Try to avoid acronyms, as they may vary between languages and can have different meanings in different contexts.
- Avoid using abstract or generic placeholders like Class1, Class2, etc., which do not provide meaningful information.

Examples:

- ❌ Name: 'Class 20-18.7' - doesn't convey the actual meaning of the class.
- ❌ Name: 'FR-MR' - an acronym that could stand for many things.
- ❌ Name: 'ABC_Wall' - unnecessary prefix.

### GEN-05
**Follow a consistent naming convention**

Names and codes should follow consistent naming conventions. While no specific naming convention is required, using a consistent style for names and codes improves searchability and readability.

Notes:

- Common naming conventions include: Pascal case (_CustomClass_), sentence case (_Custom class_), title case (_Custom Class_), snake case (_custom_class_), and kebab case (_custom-class_).
- Whitespace, dots, dashes, and underscores are acceptable for use in both names and codes.
- It is recommended that the codes are also easily recognizable, as they are the pieces of information that get stored in the data and are displayed by most of the software without integration with the bSDD. The reason for having both is that names can be translated, unliked the codes, and some software doesn't allow special characters or whitespaces in the codes (e.g. 'Łączna Wysokość').

Examples:

- ❌ Codes: 'CLS03', 'CLS04', 'CLPRP-01' - last code with a dash separator, unlike the others
- ❌ Names: 'Load Capacity' (title case), 'Power zone' (sentence case), 'ZoneCategories' (pascal case) - not consistent naming convention.
- ❌ Code: '74ts8bifnc74e7toe8n' - hard to interpret or identify in IFC data
- ✔️ Code 1: 'IsExternal', Name 1: 'is external', Code 2: 'AirTerminal', Name 2: 'air terminal' - both codes and names follow consistent naming schemas, and the codes are also interpretable.

### GEN-06
**Use of correct types**

Ensure that each item is assigned the appropriate type.

Examples:

- ✔️ 'Cement' is a `Class` with ClassType: `Material`.
- ✔️ 'Volume' is a `Property` (it should also have adequate Dimension: 3 0 0 0 0 0 0, and DataType: Real) 

### GEN-07
**Governance of the data dictionary**
🚧 TBC...

### GEN-08
**Ownership verification**
新規組織登録 

- The organization must be legitimate and have an active website.
- The contact email should be a professional, domain-specific address (for example, `name@organization.com`).
- Clearly state the purpose of the dictionary during registration. The purpose must align with bSDD's acceptable use (for example, not a product catalogue, project data, or unrelated content).
- Email verification will be conducted to make sure the author has access to such email address. The verification can be repeated periodically to ensure responsiveness. 
- Organizations should report any changes around ownership (for example, website URL change, contact email update, ownership transfer, change of dictionary purpose)

### GEN-09
**Avoid circular definitions**
ISO 704:2022 6.5.2 に従い、定義は、定義している用語（内側の円）を繰り返したり、定義している用語 （外側の円）を繰り返す場合は、説明に別の用語を使用してはならない。

Examples:
- ❌ Wall Thickness - Thickness of a wall measured between the wall faces.
- ✔️ Wall Thickness - Distance between faces of a wall.

### GEN-10
**Avoid inaccurate definitions**
ISO 704:2022 6.5.3 に従い、定義は正確でなければならない。

Examples:
- ❌ Column - usually vertical structural member. (too broad, could also mean wall)
- ❌ Column - vertical structural member supporting a roof. (too narrow, could also support floor slabs or else)
- ✔️ Column - usually vertical structural member of slender form.

### GEN-11
**Avoid negative definitions**
ISO 704:2022 6.5.4に従い、定義は、ある概念が何であるかではなく、何でないかを記述すべきである。

Examples:
- ❌ Slanted column - A column that is not vertical.
- ✔️ Slanted column - A column at an angle.

### GEN-12
**Own URIs must provide information**
デフォルトでは、bSDD は構文に従って URI 識別子を生成する：`https://identifier.buildingsmart.org/uri/<organisation>/<dictionary>/<version>/...`パブリッシャーは、独自のカスタムURIを代わりに提供するオプションを持っています。 URIが既存のページにつながっているかどうか、そのページに名前や定義などの基本情報が含まれているかどうかをチェックすることで検証されます。

## 辞書

### DCT-01 
**辞書は'Active'でなければならない**

辞書のステータスが「アクティブ」であることを確認する。これにより、内容が変更されないことが保証される。 

プレビュー」ステータスのまま検証を申請することは可能ですが、検証後の改善を除き、検証申請後の変更は認められません。検証済みバッジは、肯定的なレビューが行われ、ステータスが'Active'に変更された後にのみ付与されます。

### DCT-02 
**辞書名は誤解を招くものであってはならない**

辞書の名称は独創的でなければならず、その内容と目的を明確かつ正確に記述しなければならない。誤解を招いたり、他の辞書や団体との関連を示唆するものであってはならない。他の辞書や団体の名称は含めないでください。

例を挙げよう： 

- ❌ "Uniclass4Infra" - 辞書がNBSによって発行された公式ユニクラスの一部であるかのようにユーザーを誤解させる可能性がある。
- IFCの用語は、buildingSMARTによるIFC規格の公式出版物のために予約されているため。
- ⚠️ "Revit Classification" - まず権利者（この場合はオートデスク社）の許可を得ることをお勧めします。

## クラス

### CLS-01
**クラスはIFCに正しくマッピングされるべきである。**

各クラスは、「RelatedIfcEntities」（インポートファイルの「RelatedIfcEntityNamesList」）を使用して、IFCに適切にマッピングする必要があります。

注釈

- クラスを抽象クラス、型、関係、メジャーにマッピングしないでください。
- USERDEFINED」と「NOTDEFINED」型の使用は避ける。
- クラスを「プロキシ」にマッピングする前に、利用可能なオプションを徹底的に検索して、既存の適切なIFCエンティティがないことを確認してください。

### CLS-02
**循環的な依存関係を避ける**

ParentClassCode'で定義された親子クラス関係は、循環依存関係のないツリー構造を形成しなければならない。

例を挙げよう：
- AクラスはBの親、BはCの親、CはAの親。

### CLS-03
**クラスの階層**

複数の階層レベルを区別できる場合、それらはフラットなリストとしてモデル化されるべきではなく、明確で論理的な階層構造で構成されるべきである。

例を挙げよう： 

- 角柱'、'丸柱'、'角柱'は平らなリスト。
- ✔️ 'Column'は'Round Column'と'Rectangular Column'の親である。

### CLS-04
**シンクレティックなクラスは避ける**

マテリアル、クラス、プロパティなど、複数のアスペクトを1つのクラスにまとめたクラスは作成しないでください。

例を挙げよう： 

- 外部スチールドア」-クラス、材質、特性に関する情報を1つの定義にまとめているため、正しくない。
- ✔️ Class：Door'、Material: 'Steel'、IsExternal：'True'。

### CLS-05
**禁止接頭辞 'Ifc'**

接頭辞'Ifc'はIFC標準のために予約されている。また、'1fc'や'_Ifc'のような接頭辞の類似形にもすべて適用されます。その他の形はすべて許容されます (例: 'AbcWall')。

## プロパティ

### PRP-01
**数値プロパティのメタデータ**

プロパティが数値の場合`DataType`は`Integer`または`Real`を指定しなければならない。`Dimension`.その`Unit`はオプションで、常にSI単位とみなされるが、存在する場合はDimensionと一致しなければならない。 

例を挙げよう：
- ✔️ Dimension: '1 0 -1 0 0 0 0', Unit: 'm/s' - 速度プロパティの正しい指定。
- ✔️ Dimension: '0 0 0 0 0 0 0 0' - 無次元プロパティ (それでも Dimension は指定される)。
- ❌ 寸法: '1 0 0 0 0 0'、'単位: 'h' - 寸法(長さ)と単位(時間)の不一致。
- ❌ 単位：'W' - 寸法なし。

割り当てられた単位が寸法に正しく対応していることを確認してください。ディメンジョンと単位の不一致は、混乱やエラーの原因になります。

注釈

- Propertyの単位は、すべて同じDimensionに一致する必要があります。ClassProperty 内の単位は、Property の Dimension と一致する必要があります。
- 物理量の場合、以下のように寸法を指定する。[国際数量システム](https://en.wikipedia.org/wiki/International_System_of_Quantities)ISO 80000-1で定義されている。順番は`length`,`mass`,`time`,`electric current`,`thermodynamic temperature`,`amount of substance`そして`luminous intensity`. 

例を挙げよう： 

- プロパティに「1 1 -2 0 0 0 0」というディメンション値がある。`Units`キロニュートン」や「ニュートン」はリストにあってもよいが、「ミリメートル」はあってはならない。
- 寸法値「1 0 0 0 0 0」は、単位「キログラム」に割り当ててはならない。(正しい寸法は「0 1 0 0 0 0 0」、長さ＝0、質量＝1、時間＝0、電流＝0、熱力学的温度＝0、物質量＝0、光度＝0）。
- 速度（m/s）は「1 0 -1 0 0 0 0」と表記される。


### PRP-02
**IFCプロパティの重複を避ける**

IFC 辞書内に既に近接一致プロパティが存在する場合、そのプロパティは再作成するのではなく、 辞書内で参照されるべきである。こうすることで、一貫性のある用語の使用が増え、モデルのバリエーションが制限される。プロパティは独立したオブジェクトであるため、プロパティセットの命名に落胆しないでください。 

IFCに近いものが存在しない場合のみ、新しいプロパティを考案すること。他の有効な辞書や検証済みの辞書のプロパティを再利用することも推奨されます。既存のプロパティの特殊化である新しいプロパティを追加する場合（例えば、'Net Weight Dry'は'Net Weight'の特殊化である可能性がある）、IFCの既存のプロパティとの関係を提供する。使用方法`IsSimilarTo`リレーションシップのタイプ。

### PRP-03
**禁止接頭辞 'PSET_'**

接頭辞「PSET_」はIFC標準のために予約されている。P5ET_」や「.PSET_」のような類似の形式にも適用される。PSETの後に他の文字が続いてもよい（例えば'ePSET_')。 

新しいセットの命名には、接頭辞として「cPSET_」（「c」はcustom/created）を使用するのが一般的です。既存のIFCセットを拡張する新しいプロパティを提案する場合は、「ePSET_」（'e'はextend）を使用します。 

### PRP-04
**プロパティの適切なデータ型**

プロパティのデータ型はその定義に従わなければならず、明確性を確保し、値を適切な型に制限する。プロパティのデータ型は以下のいずれかでなければならない：`Boolean`,`Character`,`Integer`,`Real`,`String`,`Time`.

例を挙げよう： 

- プロパティが'True'か'False'しかとれない場合、データ型は次のようになります。`Boolean`ではない。`String`.

### PRP-05
**シングル・アスペクト物件**

複数のアスペクトを1つのプロパティにまとめないでください。各プロパティは、明確で適切な分類を行うために、1つのアスペクトのみを明確に表す必要があります。

例を挙げよう： 

- 鉄骨シングル」、「木枠シングル」、「鉄骨ダブル」、「木枠ダブル」のような許容値リストを持つプロパティ「窓のタイプ」は、2つのプロパティに分割されるべきである。

### PRP-06
**不必要な許容値を避ける**

許容値は、プロパティが定義され、数えられる数のオプションを持つ場合にのみ使用されるべきです。許容値は`Boolean`または可能なすべての`Integers`を特定の範囲内で使う（代わりにmin/max inc/exclusiveを使う）。

例を挙げよう： 

- ❌ 許容値：'Oui'、'Non'(フランス語ではYes/No) - 代わりに`Boolean`データ型を直接使用する。
- ❌ 許容値：'1'、'2'、'3' - 代わりに以下を使う`Integer`MinInclusive=1、MaxInclusive=3のデータ型。

### PRP-07
**許容される値は意味のあるものでなければならない**

について`AllowedValues`不動産の価値は、明確で明確なものでなければならない。代替案の組み合わせや混合を表す値を含めることは避ける。

例を挙げよう： 

- プロパティ「Color」の許容値：✔️ 'red', ✔️ 'green', ❌ 'gradient' (色の組み合わせを表すので不適切)。

## クラスプロパティ

### CPR-01
**ClassPropertyでは、アクティブなbSDDプロパティのみを使用する。**

に関連するプロパティ`ClassProperty`は、同じ辞書またはbSDDで見つかった別の辞書で定義されなければならない。`Active`.そうでなければ、不変性と検索性を確保するのは難しい。

### CPR-02
**ClassPropertyはPropertySet名を持つべきである。**

プロパティ・セットには、適切かつ一貫した名前を付けるべきである。

## 関係

### REL-01 
**RelationTypeの循環関係を避ける**

クラスとプロパティの関係は、循環的な依存関係を避け、階層構造の明瞭性を確保しなければならない。

例を挙げよう：

- A 'IsParentOf' B, B 'IsParentOf' C, C 'IsParentOf' A.
- A 'IsPartOf' B、B 'IsPartOf' A。
- A 'IsPartOf' B、A 'HasPart' C、C 'IsEqualTo' A。

### REL-02 
**RelationTypeの不正なクラス型を避ける**

クラス間の関係が論理的に一貫しており、適切なクラス・タイプに正しく割り当てられていることを確認する。

例を挙げよう：

- クラス 'A' 'HasMaterial' GroupOfProperties 'B'.(マテリアルではない)
- ❌ 材料 'A' 'IsParentOf' クラス 'B'。(マテリアルは他のマテリアルの親にしかなれません)

### REL-03
**関係は意味のあるものでなければならない**

クラスやプロパティ間の関係は、論理的で目的にかなったものでなければならない。

例を挙げよう： 

- ❌`IsChildOf`Column'クラスと'Concrete'クラスの関係 - 非論理的。
- ✔️`IsChildOf`ラウンドカラム'と'カラム'クラスの関係。
