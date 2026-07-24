# IFCおよび IDS における bSDD の参照
外部参照（bSDDなど）のクラスをIFCモデルのオブジェクトに関連付けるには、以下のドキュメントを参照してください。

使用する主なIFCコンセプトテンプレートは、「[分類の関連付け](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Classification_Association/content.html)」です。

主な関係主体は以下の通りです：
- [*IfcClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm)
- [*IfcClassificationReference*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm)
- [*IfcRelAssociatesClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesClassification.htm)

次のセクションでは、bSDDデータモデルと、クラスに使用されるIFCの概念との間のマッピング規則について説明します。これを補足するため、IFCファイルおよびbSDD辞書ファイルの抜粋（✂️）を例として掲載しています。クリックすると開きます。


## openBIMワークフロー
buildingSMARTデータディクショナリは、多くのopenBIMワークフローにおいて重要な構成要素です。これによって、とりわけ次のようなことが可能になります：
- さまざまな規格を活用して、**OpenBIMモデルを充実させる**
- データのコンプライアンス確認
- 情報提供仕様書（IDS）の概念を提示する
- IFC規格を拡張する
- その他にもさまざまな情報が掲載されています。詳細は、[bSDDのウェブサイト](https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/)をご覧ください。

## bSDD -IFCのマッピング
以下の概念について、マッピングルールが定義されています：

- [ IFCおよび IDS における bSDD の参照](#referencing-bsdd-in-ifc-and-ids)
	- [openBIMワークフロー](#openbim-workflows)
	- [bSDD -IFCのマッピング](#bsdd---ifc-mapping)
		- [1. bSDD辞書](#1-bsdd-dictionary)
		- [2. bSDDクラス（オブジェクト）](#2-bsdd-class-objects)
		- [3. bSDDの資料](#3-bsdd-materials)
		- [4. bSDDの特性](#4-bsdd-properties)

---
<h3 id="dictionary">1. bSDD辞書</h3>

**bSDDにおいて**、辞書（別名：クラスシステム）とは、ある組織が所有・管理する、オブジェクトの定義、プロパティ、およびマテリアルを標準化した集合体です。1つの組織は、1つまたは複数の辞書を所有することができます。

 **IFCでは**、[*IfcClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm) を使用して辞書情報が取得されます。以下に、さまざまなIFCバージョンに対するマッピング規則を示します。

|  | bSDD | IFC4x3_ADD2 | IFC4 | IFC2x3 | IDS1.0 |
|--------------------|------------------------------|---------------------------------|-------------------------------|-------------------------------|---------|
| **辞書名** | 辞書名 | IfcClassification.Name | IfcClassification.Name | IfcClassification.Name | ids:分類.システム |
| **辞書の出典** | *辞書のURI* | IfcClassification.Specification | IfcClassification.Location | ❌ （IfcClassification.Source を回避策として使用できます） | ids:分類.uri |
| **辞書版** | 辞書バージョン | IfcClassification.Edition | IfcClassification.Edition | IfcClassification.Edition | ❌ (uri)* |
| **辞書の所有者** | 組織コード | IfcClassification.Source | IfcClassification.Source | IfcClassification.Source | ❌ (uri)* |
| **辞書の日付** | 発売日 | IfcClassification.EditionDate | IfcClassification.EditionDate | IfcClassification.EditionDate | ❌ (uri)* |

_\* IDSは、bSDDのコンテンツをコピーするのではなく、URIを使用して参照しています。そのため、URIリンクにアクセスすれば、引き続きその情報にアクセスできます。なお、URIには以下の情報などが含まれています：uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/...```."_

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

<h3 id="class">2. bSDD クラス（オブジェクト）</h3>

**bSDDでは**、クラスは任意の（抽象的な）オブジェクト（例：[*IfcWall*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWall.htm)）、抽象的な概念（例：*原価計算*）、またはプロセス（例：*設置）*であることができます。

 **IFCでは**、クラス情報は[*IfcClassificationReference*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm) を使用して記述されます。以下に、IFCの各バージョンに対するマッピング規則を示します。

|  | bSDD | IFC4x3_ADD2およびIFC4 | IFC2x3 | IDS1.0 |
|---------------------------|--------------------------------------|-------------------------------------------|------------------------------------------|-------|
| **クラス名** | *クラスの*名前 | IfcClassificationReference.Name | IfcClassificationReference.Name | ❌ (URI経由)* |
| **クラスコード** | *クラスの*コード | IfcClassificationReference.Identification | IfcClassificationReference.ItemReference | ids:分類.値 |
| **クラス識別子** | *クラスの*URI | IfcClassificationReference.Location | IfcClassificationReference.Location | ids:分類.uri |

_\* IDSは、bSDDのコンテンツをコピーするのではなく、URIを使用して参照しています。そのため、URIリンクにアクセスすることで、引き続きその情報にアクセスすることができます。なお、URIには以下の情報の多くが含まれています：uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<ClassCode>```."_

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

<details><summary>✂️ IFC4x3_ADD2 & IFC4</summary>
	
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

<h3 id="material">3. bSDDの資料</h3>

**bSDDでは**、マテリアルは'Material'型のクラスで定義されます。主な違いは、IFCモデルのマッピングルールにあります。**タイプ'Material'のbSDDクラスは**、[*IFC_PH*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)_1_39D0226Cにリンクされ、そのIfcMaterialは、さらに[*さまざまなIfcObjectに*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm)リンクされる必要があります。
 
 **IFCおよび** [*IfcMaterial は*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)、[*IfcRelAssociatesMaterial*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesMaterial.htm)関係を通じてオブジェクトに関連付けられています。ただし、1つの要素に複数の材料が関連付けられている場合、レイヤーセット、プロファイル、または構成要素（含有率）を通じてこの関係を定義する方法は数多くあります。詳細については、「[材料の関連付け](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/content.html)」、特に「[材料構成要素セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Constituent_Set/content.html)」、「[材料レイヤーセットの使用](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Layer_Set_Usage/content.html)」、「[材料プロファイルセットの使用](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Profile_Set_Usage/content.html)」、「[材料セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Set/content.html)」、[「単一材料](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Single/content.html)」を参照してください。

以下は、IFCの各バージョンにおけるマッピング規則です。

|  | bSDD | IFC4x3_ADD2およびIFC4 | IFC2x3 | IDS1.0 |
|---------------------------------------------------|--------------------------------------------------------------------|-------------------------|-----------|-----|
| **材料名** | Class(Material).**Name** | IfcMaterial.**Name**およびIfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**Name** | IfcMaterial.**Name** | ❌ (uri)* |
| **材料コード** | Class(Material).**Code** | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**識別** | IfcMaterialClassificationRelationship.IfcClassificationReference.**アイテム参照** | ids:material.value |
| **材料識別子** | Class(Material).**Uri** | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**場所** | IfcMaterialClassificationRelationship.IfcClassificationReference.**所在地** | ids:material.uri |

_\* IDSは、bSDDの内容をコピーするのではなく、URIを使用して参照しています。そのため、URIリンクにアクセスすることで、引き続きその情報にアクセスすることができます。なお、URIには以下の情報の多くが含まれています：uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<MaterialCode>```."_

**スニペット**

*bSDDのスニペットについては、[bSDDのクラス（オブジェクト）](#2-bsdd-class-objects)を参照してください*。

<details><summary>✂️ IFC4x3_ADD2 & IFC4</summary>

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

**bSDDでは**、クラス（オブジェクト）は複数のプロパティを持つことができ、また、1つのプロパティは一部のクラス（オブジェクト）に属することができます。

 **IFCでは**、プロパティ情報は[*IfcProperty*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)を使用して取得され（[*IfcPropertySet*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySet.htm) を使用してグループ化されます）。[*IfcPropertyは*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)抽象定義であるため、インスタンス化することはできません。その代わり、さまざまな形態をとることが可能であり、最も一般的なものは[*IfcPropertySingleValue*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySingleValue.htm)です。 

以下は、IFCの各バージョンにおけるマッピング規則です。

|  | bSDD | IFC4x3_ADD2 | IFC4およびIFC2x3 | IDS1.0 |
|------------------------------------------------|-------------------------------------------|----------------------------------------------|----------------------------------------------|-----------------------|
| **物件名** | PropertyCode*（ClassPropertyの）* | IfcPropertySingleValue.Name | IfcPropertySingleValue.Name | ids:property.baseName |
| **プロパティ識別子** | uri*（ClassProperty の）* | IfcPropertySingleValue.Specification | IfcPropertySingleValue.Description | ids:property.uri |
| **プロパティの事前定義値**（単一値） | 事前定義値*（ClassProperty の）* | IfcPropertySingleValue.NominalValue | IfcPropertySingleValue.NominalValue | ❌ (URI経由)* |
| **プロパティ単位**（単一値または列挙型） | 事前定義値*（プロパティまたはクラスプロパティの）* | IfcPropertySingleValue.Unit | IfcPropertySingleValue.Unit | ❌ (uri)* |
| **プロパティの許容値**（列挙型から） | AllowedValues*（プロパティまたはClassPropertyの）* | IfcPropertyEnumeratedValue.列挙値 | IfcPropertyEnumeratedValue.列挙値 | ❌ (uri)* |
| **PropertySet名** | PropertySet*（ClassPropertyの）* | IfcPropertySet.Name | IfcPropertySet.Name | - (uri経由)* |

_\* IDSは、bSDDの内容をコピーするのではなく、URIを使用して参照しています。そのため、URIリンクにアクセスすることで、引き続きその情報にアクセスすることができます。なお、URIには以下の情報の多くが含まれています：uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/prop/<PropertyCode>```."_

⚠️ **重要**bSDD では、プロパティは、それが割り当てられる可能性のあるクラス（オブジェクト）とは独立して存在します。したがって：


- `Property` の`AllowedValues` は、各プロパティのレベルで定義されます。
- `Property` の`PredefinedValues` は、各クラス（オブジェクト）のレベルで定義されます。
- プロパティとそのプロパティセットとの関係は、各クラス（オブジェクト）のレベルで定義されます。
- `AllowedValue`s は各クラス（オブジェクト）のレベルでも定義できます。その場合、`Property` のレベルで定義された`AllowedValue` は上書きされます。

bSDD に存在する、人間が読み取り可能で翻訳可能な「*Name」*は、IFC には反映されていません。そのため、*コードは* IFCデータセットで使用され、「*Name*」はbSDDから名前を読み取ることができるソフトウェアでのみ表示されることを覚えておくことが重要です。その理由は、ユーザーに表示される言語にかかわらず、データセットが一貫した用語に従う必要があるためです。 
 
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
