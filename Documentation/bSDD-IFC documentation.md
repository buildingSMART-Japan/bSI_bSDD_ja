# IFCおよびIDSでbSDDを参照する
外部参照（bSDD など）のクラスをIFCモデル内のオブジェクトに関連付けるには、以下のドキュメントを使用します。

主に使用されるIFCコンセプト・テンプレートは次のとおりです。

主な関係主体は以下の通りである：
- [*IfcClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm)
- [*IfcClassificationReference*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm)
- [*IfcRelAssociatesClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesClassification.htm)

次のセクションでは、bSDDデータモデルとIFC概念との間のマッピングルールを示す。これをサポートするために、IFCファイルとbSDD辞書ファイルのスニペット(✂️)を例として報告する。


## openBIMワークフロー
buildingSMARTデータディクショナリーは、多くのopenBIMワークフローにおける重要なコンポーネントです。特に以下のことが可能です：
- **openBIMモデルを充実さ**せるために、さまざまな標準にアクセスする。
- コンプライアンスをチェックする
- 情報デリバリー仕様（IDS）の概念を提供する。
- IFC規格の拡張
- その他多くの情報は、[bSDDウェブサイトを](https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/)ご覧ください。

## bSDD -IFCマッピング
マッピングルールは以下の概念について定義されている：

- [ IFCおよび IDS で bSDD を参照。](#referencing-bsdd-in-ifc-and-ids)
	- [openBIMワークフロー](#openbim-workflows)
	- [bSDD -IFCマッピング](#bsdd---ifc-mapping)
		- [1. bSDD辞書](#1-bsdd-dictionary)
		- [2. bSDDクラス（オブジェクト）](#2-bsdd-classes-objects)
		- [3. bSDD材料](#3-bsdd-materials)
		- [4. bSDDの特性](#4-bsdd-properties)

---
<h3 id="dictionary">1. bSDD辞書</h3>

**bSDDでは**、ディクショナリ（別名、クラスシステム）とは、1つの組織が所有し維持する、オブジェクトの定義、プロパティ、およびマテリアルの標準化されたコレクションである。1つの組織は、1つ以上の辞書を所有することができる。

 **IFCでは**、辞書情報は[*IfcClassificationを*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm)使用して取り込まれる。以下は、IFCのバージョン別のマッピング・ルールです。

|  | bSDD | IFC4x3_ADD2 | IFC4 | IFC2x3 | IDS1.0 |
|--------------------|------------------------------|---------------------------------|-------------------------------|-------------------------------|---------|
| **辞書名** | 辞書名 | IfcClassification.Name | IfcClassification.Name | IfcClassification.Name | ids:分類システム |
| **辞書ソース** | *辞書の Uri *。* | IfcClassification.Specification | IfcClassification.Location | ❌ (IfcClassification.Sourceは回避策として使用可能) | ids:classification.uri。 |
| **辞書バージョン** | 辞書バージョン | IfcClassification.Edition | IfcClassification.Edition | IfcClassification.Edition | ❌ (uri経由)*。 |
| **辞書の所有者** | 組織コード | IfcClassification.Source | IfcClassification.Source | IfcClassification.Source | ❌ (uri経由)*。 |
| **辞書日付** | リリース日 | IfcClassification.EditionDate | IfcClassification.EditionDate | IfcClassification.EditionDate | ❌ (uri経由)*。 |

Uri* IDSは、bSDDの内容をコピーする代わりに、URIを使ってbSDDを参照する。そのおかげで、URIのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/...``."_URIには、多くの情報が含まれていることに注意。

**スニペット**
<details><summary>✂️ bSDD</summary>
    
```
{
    "OrganizationCode": "text",
    "DictionaryCode": "text",
    "DictionaryVersion": "text",
    "DictionaryName": "text",
    "ReleaseDate": null,
    "Status": "text",
    "MoreInfoUrl": "text",
    "UseOwnUri": false,
    "DictionaryUri": "text",
    "LanguageIsoCode": "text",
    "LanguageOnly": false,
    "License": "text",
    "LicenseUrl": "text",
    "QualityAssuranceProcedure": "text",
    "QualityAssuranceProcedureUrl": "text",
    "Classes": [], 
    "Properties": []
  }
```
</details>

<details><summary>✂️ IFC4x3_ADD2 <a href="https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm">(IfcClassification)</a></summary>
	
    /* 			 Source,   Edition, EditionDate,  Name,                Description,            Specification,                                                      ReferenceTokens  */
    #1=IFCCLASSIFICATION('Molio',  '1.0',   '2023-08-27', 'CCI Construction',  'List of codes...',    'https://identifier.buildingsmart.org/uri/molio/cciconstruction/1.0', ('.'));
</details>

<details><summary>✂️ IFC4 <a href="https://standards.buildingsmart.org/IFC/RELEASE/IFC4/ADD2_TC1/HTML/">(IfcClassification)</a></summary>

    /*  		 Source,   Edition, EditionDate,  Name,                Description,            Location,                                                      ReferenceTokens   */
    #1=IFCCLASSIFICATION('Molio',  '1.0',   '2023-08-27', 'CCI Construction',  'List of codes...',    'https://identifier.buildingsmart.org/uri/molio/cciconstruction/1.0', ('.'));
</details>

<details><summary>✂️ IFC2x3 <a href="https://standards.buildingsmart.org/IFC/RELEASE/IFC2x3/TC1/HTML/ifcexternalreferenceresource/lexical/ifcclassification.htm">(IfcClassification)</a></summary>

    /*  		 Source,   Edition, EditionDate,  Name    */
    #1=IFCCLASSIFICATION('Molio',  '1.0',   '2023-08-27', 'CCI Construction');
</details>
    

---

<h3 id="class">2. bSDDクラス（オブジェクト）</h3>

**bSDD では**、クラスは、任意の（抽象的な）オブジェクト（[*IfcWall*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWall.htm) など）、抽象概念（*原価計算など*）、またはプロセス（*設置など*）である。

 **IFCでは**、クラス情報は[*IfcClassificationReferenceを*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm)使用して取り込まれます。以下は、IFCのバージョン別のマッピング・ルールです。

|  | bSDD | IFC4x3_ADD2&amp;IFC4 | IFC2x3 | IDS1.0 |
|---------------------------|--------------------------------------|-------------------------------------------|------------------------------------------|-------|
| **クラス名** | *クラス*名 | IfcClassificationReference.Name | IfcClassificationReference.Name | ❌ (uri経由)*。 |
| **クラスコード** | *クラスの*コード | IfcClassificationReference.Identification | IfcClassificationReference.ItemReference | ids:分類.値 |
| **クラス識別子** | *クラスの*Uri***。 | IfcClassificationReference.Location | IfcClassificationReference.Location | ids:classification.uri。 |

Uri* IDSは、bSDDの内容をコピーする代わりに、URIを使ってbSDDを参照する。そのおかげで、URIのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<ClassCode>``."_URIには、多くの情報が含まれていることに注意してください。

**スニペット**
<details><summary>✂️ bSDDクラス</summary>
    
```
{
	"Code": "text",
	"Uid": "text",
	"OwnedUri": "text",
	"Name": "text",
	"Definition": "text",
	"Status": "text",
	"ActivationDateUtc": "2022-05-12T00:00:00+02:00",
	"RevisionDateUtc": null,
	"VersionDateUtc": "2022-05-12T00:00:00+02:00",
	"DeActivationDateUtc": null,
	"VersionNumber": null,
	"RevisionNumber": null,
	"ReplacedObjectCodes": [],
	"ReplacingObjectCodes": [],
	"DeprecationExplanation": "text",
	"CreatorLanguageIsoCode": "text",
	"VisualRepresentationUri": "text",
	"CountriesOfUse": [],
	"SubdivisionsOfUse": [],
	"CountryOfOrigin": "text",
	"DocumentReference": "text",
	"Synonyms": [],
	"ReferenceCode": "text",
	"ClassRelations": [
	  {
		"RelationType": "text",
		"RelatedClassUri": "text",
		"RelatedClassName": "text",
		"Fraction": null
	  }
	],
	"ClassType": "text",
	"ParentClassCode": "text",
	"RelatedIfcEntityNamesList": [],
	"ClassProperties": [
	  {
		"AllowedValues": [
		  {
			"Uri": "text",
			"Code": "text",
			"Value": "text",
			"Description": "text",
			"SortNumber": null
		  }
		],
		"Code": "text",
		"Description": "text",
		"IsRequired": null,
		"IsWritable": null,
		"MaxExclusive": null,
		"MaxInclusive": null,
		"MinExclusive": null,
		"MinInclusive": null,
		"Pattern": "text",
		"PredefinedValue": "text",
		"PropertyCode": "text",
		"PropertyUri": "text",
		"PropertySet": "text",
		"PropertyType": "text",
		"SortNumber": null,
		"Symbol": "text",
		"Unit": "text"
	  }
	]
}
```
</details>

<details><summary>✂️ IFC4x3_ADD2& IFC4</summary>
	
    /*  		 Source,   Edition, EditionDate,  Name,                Description,            Specification,                                                      ReferenceTokens   */
    #1=IFCCLASSIFICATION('Molio',  '1.0',   '2023-08-27', 'CCI Construction',  'List of codes...',    'https://identifier.buildingsmart.org/uri/molio/cciconstruction/1.0', ('.'));
    
    /*  			  Location,                                                                        Identification, Name,             ReferencedSource, Description,           Sort   */
    #2=IFCCLASSIFICATIONREFERENCE('https://identifier.buildingsmart.org/uri/molio/cciconstruction/1.0/class/L-BD', 'L-BD',         'Wall structure', #1,               'structural system...', $);

    /*         GlobalId,                 OwnerHistory, Name, Description, ObjectType, ObjectPlacement, Representation, Tag, PredefinedType   */
    #3=IFCWALL('3t3TDZl_D9NOIWB0BSjzJI', $,            $,    $,           $,          $,               $,              $,   $);
    
    /*  			      GlobalId,                 OwnerHistory, Name, Description, RelatedObjects, RelatingClassification  */
    #4=IFCRELASSOCIATESCLASSIFICATION('2t3TDZl_D9NOIWB0BSjzJI', $,            $,    $,           (#3),           #2);
</details>

<details><summary>✂️ IFC2x3</summary>
    
	
    /*  		  Source,   Edition, EditionDate,  Name   */
    #1=IFCCLASSIFICATION('Molio',  '1.0',   '2023-08-27', 'CCI Construction');
    
    /*   			  Location,                                                                        ItemReference, Name,             ReferencedSource  */
    #2=IFCCLASSIFICATIONREFERENCE('https://identifier.buildingsmart.org/uri/molio/cciconstruction/1.0/class/L-BD', 'L-BD',        'Wall structure', #1);

    /*         GlobalId,                 OwnerHistory, Name, Description, ObjectType, ObjectPlacement, Representation, Tag   */
    #3=IFCWALL('3t3TDZl_D9NOIWB0BSjzJI', $,            $,    $,           $,          $,               $,              $);
    
    /* 				      GlobalId,                 OwnerHistory, Name, Description, RelatedObjects, RelatingClassification    */
    #4=IFCRELASSOCIATESCLASSIFICATION('2t3TDZl_D9NOIWB0BSjzJI', $,            $,    $,           (#3),           #2);
</details>

<details><summary>✂️ IDS1.0</summary>
	
```
<ids:classification uri="https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.1/class/apple" cardinality="required" instructions="Those objects must be classified as apples.">
  <ids:value>
	<ids:simpleValue>apple</ids:simpleValue>
  </ids:value>
  <ids:system>
	<ids:simpleValue>fruitvegs</ids:simpleValue>
  </ids:system>
</ids:classification>
```
</details>

---

<h3 id="material">3. bSDD材料</h3>

**bSDD では**、材料は 'Material' タイプのクラスで定義されます。主な違いは、IFCモデルのマッピングルールです。**材料'タイプのbSDDクラスは**、[*IfcMaterialに*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)リンクする必要があり、[*IfcObjectに*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm)リンクします。
 
 **IFCでは**、[*IfcMaterial*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)は[*IfcRelAssociatesMaterial の*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesMaterial.htm)関係を通じてオブジェクトと関連付けられます。ただし、1つの要素に複数の材料が関連付けられている場合は、レイヤーセット、プロファイル、または構成要素（含有率）を通じて、この関係を定義する方法が数多く考えられます。詳しくはこちら：[素材の関連](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/content.html)、特に[素材構成要素セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Constituent_Set/content.html)、[素材レイヤーセットの使用法](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Constituent_Set/content.html)、[素材プロファイルセットの使用法](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Profile_Set_Usage/content.html)、[素材セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Set/content.html)、[素材シングル](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Single/content.html)。

以下は、IFCのバージョン別のマッピング・ルールです。

|  | bSDD | IFC4x3_ADD2&amp;IFC4 | IFC2x3 | IDS1.0 |
|---------------------------------------------------|--------------------------------------------------------------------|-------------------------|-----------|-----|
| **材料名** | クラス(素材).**名前** | IfcMaterial.**Name**&amp;IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**Name** | IfcMaterial.**Name** | ❌ (uri経由)*。 |
| **材料コード** | クラス（素材）.**コード** | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**識別情報** | IfcMaterialClassificationRelationship.IfcClassificationReference.**Itemリファレンス** | ids:材料.値 |
| **材料識別子** | クラス(材料).**Uri** | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**場所** | IfcMaterialClassificationRelationship.IfcClassificationReference.**Location** | ids:材料.uri |

Uri* IDSは、bSDDの内容をコピーする代わりに、URIを使ってbSDDを参照する。そのおかげで、URIのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<MaterialCode>``."_URIには、多くの情報が含まれていることに注意してください。

**スニペット**

*bSDDのスニペットについては、[bSDDのクラス（オブジェクト）を見て](#2.-bSDD-classes-(objects)ください。)*

<details><summary>✂️ IFC4x3_ADD2& IFC4</summary>

    /*    		 Source, Edition, EditionDate,  Name,                Description,            Specification,                                                      ReferenceTokens   */
    #1=IFCCLASSIFICATION('bs-agri',  '1.1',     '2022-12-26', 'Fruit and vegetables', 'Demonstration dictionary', 'https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.1', ('.'));
    
    /*  			  Location,                                                                   Identification, Name,     ReferencedSource, Description,           Sort   */
    #2=IFCCLASSIFICATIONREFERENCE('https://identifier.buildingsmart.org/uri/sbe/swedishmaterials/1/class/CE--', 'CE--',         'Betong', #1,               'kompositmaterial...', $);

    /*   	    Name,    Description,          Category   */
    #3=IFCMATERIAL('Betong','kompositmaterial...','concrete');
    
    /*  				 Name,     Description,          RelatingReference, RelatedResourceObjects  */
    #4=IFCEXTERNALREFERENCERELATIONSHIP('Betong', 'kompositmaterial...', #2,                (#3));

</details>

<details><summary>✂️ IFC2x3</summary>
    
    /* 			 Source, Edition, EditionDate, Name 		    */
    #1=IFCCLASSIFICATION('bs-agri',  '1.1',    '2022-12-26', 'Fruit and vegetables');
    
    /*  			  Location,                                                                   ItemReference, Name,     ReferencedSource */
    #2=IFCCLASSIFICATIONREFERENCE('https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.1/class/fiber', 'fiber',        'Fiber', #1);
     IfcClassificationReference( $,**ItemReference**,$,$)
     
    /*              Name      */
    #3=IFCMATERIAL('Fiber');
    
    /*  				     MaterialClassifications, ClassifiedMaterial  */
    #4=IFCMATERIALCLASSIFICATIONRELATIONSHIP(#2,                      #3);

</details>

<details><summary>✂️ IDS1.0</summary>

```
<ids:material uri="https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.1/class/fiber" cardinality="required" instructions="The material should be called fiber.">
  <ids:value>
	<ids:simpleValue>fiber</ids:simpleValue>
  </ids:value>
</ids:material>
```
</details>

--- 


<h3 id="property">4. bSDDの特性</h3>

**bSDD では**、1 つのクラス (オブジェクト) は複数のプロパティを持つことができ、1 つのプロパティは多くのクラス (オブジェクト) の一部になることができる。

 **IFCでは**、プロパティ情報は[*IfcPropertyを*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)使用して取り込まれます（そして[*IfcPropertySetを*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySet.htm)使用してグループ化されます）。[*IfcPropertyは*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)抽象定義であり、インスタンス化することはできません。[*IfcPropertySingleValueが*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySingleValue.htm)最も一般的です。 

以下は、IFCのバージョン別のマッピング・ルールです。

|  | bSDD | IFC4x3_ADD2 | IFC4&amp;IFC2x3 | IDS1.0 |
|------------------------------------------------|-------------------------------------------|----------------------------------------------|----------------------------------------------|-----------------------|
| **物件名** | プロパティコード*（ClassPropertyの）* | IfcPropertySingleValue.Name | IfcPropertySingleValue.Name | ids:property.baseName |
| **プロパティの識別子** | uri*(ClassPropertyの)**。 | IfcPropertySingleValue.Specification | IfcPropertySingleValue.Description | ids:property.uri。 |
| **プロパティ事前定義値**（単一値） | *(ClassPropertyの)*定義済み値 | IfcPropertySingleValue.NominalValue | IfcPropertySingleValue.NominalValue | ❌ (uri経由)*。 |
| **プロパティ単位**（単一値または列挙から） | *(PropertyまたはClassPropertyの)*定義済み値。 | IfcPropertySingleValue.Unit | IfcPropertySingleValue.Unit | ❌ (uri経由)*。 |
| **プロパティの許容値**（列挙から） | AllowedValues *（Property または ClassProperty の）*。 | IfcPropertyEnumeratedValue.EnumerationValues | IfcPropertyEnumeratedValue.列挙値 | ❌ (uri経由)*。 |
| **プロパティセット名** | プロパティセット*（ClassPropertyの）* | IfcPropertySet.Name | IfcPropertySet.Name | - (uri経由)*。 |

Uri* IDSは、bSDDの内容をコピーする代わりに、URIを使ってbSDDを参照する。そのおかげで、URIのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/prop/<PropertyCode>``."_URIには、多くの情報が含まれていることに注意してください。

⚠️ **重要**bSDD では、プロパティは、それらが割り当てられているクラス (オブジェクト) とは無関係に存在します。したがって


- `Property` の`AllowedValues` は、各プロパティのレベルで定義される。
- `Property` の`PredefinedValues` は、各クラス（オブジェクト）のレベルで定義される。
- プロパティとそのプロパティ・セットの関係は、各クラス（オブジェクト）のレベルで定義される。
- `AllowedValue`は、各クラス（オブジェクト）のレベルでも定義できる。この場合、`Property` のレベルで定義された`AllowedValue` は上書きされます。

IFCでは、bSDDに存在する人間が読みやすく翻訳可能な*名前は*反映されません。そのため、*コードは* IFCデータセットで使用され、*名前は*bSDDから名前を読み取ることができるソフトウェアによってのみ表示されることを覚えておくことが重要です。この理由は、ユーザーに表示される言語に関係なく、データセットが一貫した用語に従う必要があるからである。 
 
**スニペット**
<details><summary>✂️ bSDD プロパティ</summary>
    
```
{
	"Code": "text",
	"Uid": "text",
	"OwnedUri": "text",
	"Name": "text",
	"Definition": "text",
	"Status": "text",
	"ActivationDateUtc": "2022-05-12T00:00:00+02:00",
	"RevisionDateUtc": null,
	"VersionDateUtc": "2022-05-12T00:00:00+02:00",
	"DeActivationDateUtc": null,
	"VersionNumber": null,
	"RevisionNumber": null,
	"ReplacedObjectCodes": [],
	"ReplacingObjectCodes": [],
	"DeprecationExplanation": "text",
	"CreatorLanguageIsoCode": "text",
	"VisualRepresentationUri": "text",
	"CountriesOfUse": [],
	"SubdivisionsOfUse": [],
	"CountryOfOrigin": "text",
	"DocumentReference": "text",
	"Description": "text",
	"Example": "text",
	"ConnectedPropertyCodes": [],
	"PhysicalQuantity": "text",
	"Dimension": "text",
	"DimensionLength": null,
	"DimensionMass": null,
	"DimensionTime": null,
	"DimensionElectricCurrent": null,
	"DimensionThermodynamicTemperature": null,
	"DimensionAmountOfSubstance": null,
	"DimensionLuminousIntensity": null,
	"MethodOfMeasurement": "text",
	"DataType": "text",
	"PropertyValueKind": "text",
	"MinInclusive": null,
	"MaxInclusive": null,
	"MinExclusive": null,
	"MaxExclusive": null,
	"Pattern": "text",
	"IsDynamic": false,
	"DynamicParameterPropertyCodes": [],
	"Units": [],
	"AllowedValues": [
	  {
		"Uri": "text",
		"Code": "text",
		"Value": "text",
		"Description": "text",
		"SortNumber": null
	  }
	],
	"TextFormat": "text",
	"PropertyRelations": [
	  {
		"RelationType": "text",
		"RelatedPropertyUri": "text",
		"RelatedPropertyName": "text"
	  }
	]
}
```
</details>

<details><summary>✂️ IFC2x3</summary>
    
    /*                         Name,       Description, 							  NominalValue, Unit */
    #1=IFCPROPERTYSINGLEVALUE("EF021146", "https://identifier.buildingsmart.org/uri/etim/etim/9.0/prop/EF021146", $,            $);

</details>

</details>

<details><summary>✂️ IFC4x3_ADD2</summary>
    
    /*                         Name,       Specification, 							  NominalValue, Unit */
    #1=IFCPROPERTYSINGLEVALUE("EF021146", "https://identifier.buildingsmart.org/uri/etim/etim/9.0/prop/EF021146", $,            $);

</details>

<details><summary>✂️ IDS1.0</summary>

```
<ids:property dataType="IFCLABEL" uri="http://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3/prop/manufacturer" cardinality="required" instructions="One of the two manufacturers must be specified.">
  <ids:propertySet>
	<ids:simpleValue>Pset_ManufacturerTypeInformation</ids:simpleValue>
  </ids:propertySet>
  <ids:baseName>
	<ids:simpleValue>Manufacturer</ids:simpleValue>
  </ids:baseName>
  <ids:value>
	<xs:restriction base="xs:string">
	  <xs:enumeration value="Manufacturer 1" />
	  <xs:enumeration value="Manufacturer 2" />
	</xs:restriction>
  </ids:value>
</ids:property>
```
</details>
