# IFCおよびIDSにおけるbSDDの参照

外部参照（bSDD など）のクラスを IFC モデルのオブジェクトに関連付けるには、以下のドキュメントを使用します。

使用される主なIFCコンセプト・テンプレートは以下の通り：[分類協会](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Classification_Association/content.html)

主な関係主体は以下の通りである：
- [_ifcClassification_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm)
- [_IfcClassificationリファレンス_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm)
- [_IfcRelAssociates分類_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesClassification.htm)

次のセクションでは、bSDDデータモデルとIFCコンセプトのマッピングルールを示します。


## openBIMワークフロー
buildingSMARTデータディクショナリーは、多くのopenBIMワークフローにおける重要なコンポーネントです。 特に、以下のことが可能です：
- 様々な規格にアクセスできる**openBIMモデルを充実させる**
- コンプライアンスをチェックする
- 情報デリバリー仕様（IDS）の概念を提供する。
- IFC規格の拡張
- などなど、詳しくはこちらをご覧いただきたい：[bSDDウェブサイト](https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/)

## bSDD - IFCマッピング

マッピングルールは以下の概念について定義されている：

- [IFCおよびIDSにおけるbSDDの参照](#referencing-bsdd-in-ifc-and-ids)
	- [openBIMワークフロー](#openbim-workflows)
	- [bSDD - IFCマッピング](#bsdd---ifc-mapping)
		- [1. bSDD辞書](#1-bsdd-dictionary)
		- [2. bSDDクラス（オブジェクト）](#2-bsdd-classes-objects)
		- [3. bSDD材料](#3-bsdd-materials)
		- [4. bSDDの特性](#4-bsdd-properties)

---
<h3 id="dictionary">1. bSDD dictionary</h3>

**bSDDでは**ディクショナリ（別名、クラス・システム）とは、1つの組織が所有し維持する、オブジェクトの定義、プロパ ティ、および資料の標準化されたコレクションのことである。 1つの組織が1つ以上のディクショナリを所有することができる。

**IFCの場合**辞書情報は[_ifcClassification_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm)以下は、異なるIFCバージョンのマッピングルールです。

|  | bSDD | IFC4x3_ADD2 | IFC4 | IFC2x3 | IDS1.0 |
|--------------------|------------------------------|---------------------------------|-------------------------------|-------------------------------|---------|
| **辞書名** | 辞書名 | IfcClassification.名前 | IfcClassification.名前 | IfcClassification.名前 | ids:classification.system / (uri) |
| **辞書ソース** | *辞書のウリ* | IfcClassification.仕様 | IfcClassification.ロケーション | ❌ (IfcClassification.Sourceは回避策として使用可能) | ウリ |
| **辞書バージョン** | 辞書バージョン | IfcClassification.エディション | IfcClassification.エディション | IfcClassification.エディション | (ウリ) |
| **辞書の所有者** | 組織コード | IfcClassification.ソース | IfcClassification.ソース | IfcClassification.ソース | (ウリ) |
| **辞書日付** | リリース日 | IfcClassification.EditionDate。 | IfcClassification.EditionDate。 | IfcClassification.EditionDate。 | (ウリ) |

_\* IDS references bSDD using URI, instead of copying its content. Thanks to that, the information is still accessible by following the URI link. Note that the URI include many of those information: uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/...```."_

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

<h3 id="class">2. bSDD class (objects)</h3>

**bSDDでは**クラスは任意の（抽象）オブジェクト（例えば[_イフックウォール_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWall.htm))、抽象概念(例えば_原価計算_)またはプロセス(例えば_インストール"_.

**IFCの場合**クラス情報は[_IfcClassificationリファレンス_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm)以下は、異なるIFCバージョンのマッピングルールです。

|  | bSDD | IFC4x3_ADD2 & IFC4 | IFC2x3 | IDS1.0 |
|---------------------------|--------------------------------------|-------------------------------------------|------------------------------------------|-------|
| **クラス名** | クラス名 | IfcClassificationReference.名前 | IfcClassificationReference.名前 | (ウリ) |
| **クラスコード** | クラスのコード | IfcClassificationReference.Identification。 | IfcClassificationReference.ItemReference。 | (ウリ) |
| **クラス識別子** | クラスの | IfcClassificationReference.Location。 | IfcClassificationReference.Location。 | ウリ |

_\* IDS references bSDD using URI, instead of copying its content. Thanks to that, the information is still accessible by following the URI link. Note that the URI include many of those information: uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<ClassCode>```."_

**スニペット**
<details><summary>✂️ bSDD class</summary>
    
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

<h3 id="material">3. bSDD materials</h3>

**bSDDでは**主な違いは、IFCモデルのマッピング・ルールにあります。 IFCモデルのマッピング・ルールは、次のとおりです。**タイプ'Material'のbSDDクラス**にリンクされていなければならない。[_Ifcマテリアル_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)そして、そのリンクは様々な[_IfcObject_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm).
 
**IFCの場合**,[_Ifcマテリアル_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)を通じてオブジェクトに関連付けられる。[_IfcRelAssociates資料_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesMaterial.htm)しかし、1つの要素に複数の素材が関連付けられている場合、レイヤーセット、プロファイル、または構成要素（含有率）を通じて、この関係を定義する方法が数多く考えられます。 続きを読む[素材協会](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/content.html)特にそうだ：[素材構成セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Constituent_Set/content.html),[マテリアルレイヤーセット使用法](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Constituent_Set/content.html),[素材プロファイルセットの使用法](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Profile_Set_Usage/content.html),[素材セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Set/content.html),[素材 シングル](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Single/content.html).

以下は、異なるIFCバージョンのマッピングルールです。

|  | bSDD | IFC4x3_ADD2 & IFC4 | IFC2x3 | IDS1.0 |
|---------------------------------------------------|--------------------------------------------------------------------|-------------------------|-----------|-----|
| **材料名** | クラス(素材).**名前 | IfcMaterial.**Name** & IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**Name | IfcMaterial.**Name | (ウリ) |
| **材料コード** | クラス（素材）.**コード | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**Identification。 | IfcMaterialClassificationRelationship.IfcClassificationReference.**ItemReference。 | (ウリ) |
| **材料識別子** | クラス(素材).**Uri | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**ロケーション | IfcMaterialClassificationRelationship.IfcClassificationReference.**ロケーション | ウリ |

_\* IDS references bSDD using URI, instead of copying its content. Thanks to that, the information is still accessible by following the URI link. Note that the URI include many of those information: uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<MaterialCode>```."_

**スニペット**

_bSDDのスニペットについては[bSDDクラス（オブジェクト）](#2.-bSDD-classes-(objects))_

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


<h3 id="property">4. bSDD properties</h3>

**bSDDでは**クラス（オブジェクト）は複数のプロパティを持つことができ、プロパティは多くのクラス（オブジェクト）の一部になることができる。

**IFCの場合**プロパティ情報は[_IfcProperty_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)(でグループ化されている[_IfcPropertySet_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySet.htm)).[_IfcProperty_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)は抽象的な定義であり、インスタンス化できないことを意味する。 代わりに、この定義にはさまざまな形式があり、最も一般的なものは次のとおりである。[_IfcPropertySingleValue_](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySingleValue.htm). 

以下は、異なるIFCバージョンのマッピングルールです。

|  | bSDD | IFC4x3_ADD2 | IFC4 & IFC2x3 | IDS1.0 |
|------------------------------------------------|-------------------------------------------|----------------------------------------------|----------------------------------------------|-----------------------|
| **物件名** | プロパティコード *(クラスプロパティの) | IfcPropertySingleValue.Name | IfcPropertySingleValue.Name | (ウリ) |
| **プロパティの識別子** | uri *(クラスプロパティの) | IfcPropertySingleValue.仕様 | IfcPropertySingleValue.Description。 | ウリ |
| プロパティ事前定義値**（単一値） | 定義済み値 *(of ClassProperty) | IfcPropertySingleValue.NominalValue。 | IfcPropertySingleValue.NominalValue。 | (ウリ) |
| プロパティ単位**（単一値または列挙から） | PredefinedValue *（Property または ClassProperty の）定義済み値。 | IfcPropertySingleValue.Unit。 | IfcPropertySingleValue.Unit。 | (ウリ) |
| プロパティの許容値**（列挙より） | AllowedValues *（Property または ClassProperty の）値。 | IfcPropertyEnumeratedValue .EnumerationValues | IfcPropertyEnumeratedValue .EnumerationValues | (ウリ) |
| **プロパティセット名** | プロパティセット *(of ClassProperty) | IfcPropertySet.Name | IfcPropertySet.Name | (ウリ) |

_\* IDS references bSDD using URI, instead of copying its content. Thanks to that, the information is still accessible by following the URI link. Note that the URI include many of those information: uri="```http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/prop/<PropertyCode>```."_

⚠️**重要**
In bSDD, properties exist independently of the class (object) they might be assigned to. Therefore: 

- について`AllowedValues`の`Property`は各プロパティのレベルで定義される。
- について`PredefinedValues`の`Property`は各クラス（オブジェクト）のレベルで定義される。
- プロパティとそのプロパティ・セットの関係は、各クラス（オブジェクト）のレベルで定義される。
- `AllowedValue`を各クラス（オブジェクト）のレベルでも定義することができます。 この場合`AllowedValue`のレベルで定義されている。`Property`が上書きされる。 

人間が読め、翻訳可能な_名称_bSDDに存在するものは、IFCには反映されない。_コード_はIFCデータセットで使用される。_名称_この理由は、ユーザーに表示される言語に関係なく、データセットが一貫した用語に従う必要があるからである。 
 
**スニペット**
<details><summary>✂️ bSDD property</summary>
    
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
