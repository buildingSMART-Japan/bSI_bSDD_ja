# IFC 、IDSでbSDDを参照する。
外部参照（bSDD など）のクラスをIFC モデルのオブジェクトに関連付けるには、以下の文書を使用する。

主なIFC コンセプトテンプレートは以下の通り。

主な関係主体は以下の通りである：
- [*IfcClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm)
- [*IfcClassificationReference*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm)
- [*IfcRelAssociatesClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesClassification.htm)

次のセクションでは、bSDDデータモデルとIFC の概念との間のマッピングルールを示す。これをサポートするために、IFC ファイルと bSDD 辞書ファイルのスニペット(✂️)が例として報告されています。


## openBIMワークフロー
buildingSMARTデータディクショナリーは、多くのopenBIMワークフローにおける重要なコンポーネントです。特に以下のことが可能です：
- **openBIMモデルを充実さ**せるために、さまざまな標準にアクセスする。
- コンプライアンスをチェックする
- 情報デリバリー仕様（IDS）の概念を提供する。
- IFC 規格の拡大
- その他多くの情報は、[bSDDウェブサイトを](https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/)ご覧ください。

## bSDD -IFC マッピング
マッピングルールは以下の概念について定義されている：

- [ IFC 、IDSでbSDDを参照する。](#referencing-bsdd-in-ifc-and-ids)
	- [openBIMワークフロー](#openbim-workflows)
	- [bSDD -IFC マッピング](#bsdd---ifc-mapping)
		- [1. bSDD辞書](#1-bsdd-dictionary)
		- [2. bSDDクラス（オブジェクト）](#2-bsdd-classes-objects)
		- [3. bSDD材料](#3-bsdd-materials)
		- [4. bSDDの特性](#4-bsdd-properties)

---
<h3 id="dictionary">1. bSDD辞書</h3>

**bSDDでは**、ディクショナリ（別名、クラスシステム）とは、1つの組織が所有し維持する、オブジェクトの定義、プロパティ、およびマテリアルの標準化されたコレクションである。1つの組織は、1つ以上の辞書を所有することができる。

 **IFC では**、辞書情報は [*IfcClassification*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassification.htm).以下は、IFC のバージョンごとのマッピング規則である。

|  | <nobr>bSDD</nobr> | <nobr>IFC4x3</nobr>_ADD2（エーディーツー） | <nobr>IFC4</nobr> | <nobr>IFC2x3</nobr> | <nobr>IDS1</nobr>.0 |
|--------------------|------------------------------|---------------------------------|-------------------------------|-------------------------------|---------|
| **辞書名**　　　　 | 辞書名　　　　 | IfcClassification.Name | IfcClassification.Name | IfcClassification.Name | ids:classification.system／（Uri）*。 |
| **辞書ソース** | *辞書の uri* | IfcClassification.Specification | IfcClassification.Location | ❌ (IfcClassification.Source は回避策として使える) | uri |
| **辞書バージョン** | 辞書バージョン | IfcClassification.Edition | IfcClassification.Edition | IfcClassification.Edition | (Uri*) |
| **辞書の所有者** | 組織コード | IfcClassification.Source | IfcClassification.Source | IfcClassification.Source | (Uri*) |
| **辞書日付** | リリース日 | IfcClassification.EditionDate | IfcClassification.EditionDate | IfcClassification.EditionDate | (Uri*) |

Uri* IDSは、bSDDの内容をコピーする代わりに、Uriを使ってbSDDを参照する。そのおかげで、Uriのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/...``."_URIには、多くの情報が含まれていることに注意。

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

**bSDD では**、クラスは任意の (抽象的な) オブジェクト (たとえば [*IfcWall*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWall.htm))、抽象概念 (例:*Costing*)、またはプロセス (例:*Installation*)。

 **IFC では**、クラス情報は [*IfcClassificationReference*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcClassificationReference.htm).以下は、IFC のバージョン別のマッピング・ルールです。

|  | <nobr>bSDD</nobr> | <nobr>IFC4x3</nobr>ADD2とIFC4 | <nobr>IFC2x3</nobr> | <nobr>IDS1</nobr>.0 |
|---------------------------|--------------------------------------|-------------------------------------------|------------------------------------------|-------|
| **クラス名**　　　 | *クラス*名　　　 | IfcClassificationReference.Name | IfcClassificationReference.Name | (Uri*)　　 |
| **クラスコード** | *クラスの*コード | IfcClassificationReference.Identification | IfcClassificationReference.ItemReference | (Uri*) |
| **クラス識別子** | *クラスの*uri | IfcClassificationReference.Location | IfcClassificationReference.Location | uri |

Uri* IDSは、bSDDの内容をコピーする代わりに、Uriを使ってbSDDを参照する。そのおかげで、Uriのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<ClassCode>``."_URIには、多くの情報が含まれていることに注意してください。

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

**bSDD では**、材料は 'Material' タイプのクラスで定義されます。主な違いは、IFC モデルのマッピングルールです。**bSDDの'Material'型のクラスは**、'**Material**'型にリンクされなければなりません。 [*IfcMaterial*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)にリンクされなければなりません。 [*IfcObject*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm).
 
 **IFC では**、、 [*IfcMaterial*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcMaterial.htm)は [*IfcRelAssociatesMaterial*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelAssociatesMaterial.htm)関係によってオブジェクトと関連付けられる。しかし、1つの要素に複数の素材が関連付けられている場合、レイヤーセット、プロファイル、または構成要素（コンテンツの割合）を通して、この関係を定義する方法が数多く考えられます。詳しくはこちら：[素材の関連](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/content.html)、特に[素材構成要素セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Constituent_Set/content.html)、[素材レイヤーセットの使用法](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Constituent_Set/content.html)、[素材プロファイルセットの使用法](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Profile_Set_Usage/content.html)、[素材セット](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Set/content.html)、[素材シングル](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/concepts/Object_Association/Material_Association/Material_Single/content.html)。

以下は、IFC バージョン別のマッピングルールである。

|  | <nobr>bSDD</nobr> | <nobr>IFC4x3</nobr>ADD2とIFC4 | <nobr>IFC2x3</nobr> | <nobr>IDS1</nobr>.0 |
|---------------------------------------------------|--------------------------------------------------------------------|-------------------------|-----------|-----|
| **材料名**　　　　 | クラス(素材).**名前** | IfcMaterial.**Name**&amp;IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference.**Name** | IfcMaterial**名前** | (Uri*)　　 |
| **材料コード** | クラス（素材）.**コード** | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference**身分証明書** | IfcMaterialClassificationRelationship.IfcClassificationReference.**ItemReference** | (Uri*) |
| **材料識別子** | クラス（材料）.**Uri** | IfcExternalReferenceRelationship.RelatingReference.IfcClassificationReference**所在地** | IfcMaterialClassificationRelationship.IfcClassificationReference**所在地** | uri |

Uri* IDSは、bSDDの内容をコピーする代わりに、Uriを使ってbSDDを参照する。そのおかげで、Uriのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/class/<MaterialCode>``."_URIには、多くの情報が含まれていることに注意してください。

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

 **IFC では**、プロパティ情報は [*IfcProperty*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)(そして [*IfcPropertySet*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySet.htm)). [*IfcProperty*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcProperty.htm)は抽象的な定義であり、インスタンス化することはできません。その代わり、さまざまな形式があります。 [*IfcPropertySingleValue*](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySingleValue.htm). 

以下は、IFC バージョン別のマッピングルールである。

|  | <nobr>bSDD</nobr> | <nobr>IFC4x3</nobr>_ADD2（エーディーツー） | IFC4 &amp; <nobr>IFC2x3</nobr> | <nobr>IDS1</nobr>.0 |
|------------------------------------------------|-------------------------------------------|----------------------------------------------|----------------------------------------------|-----------------------|
| **物件名**　　　　 | プロパティコード*（ClassPropertyの）* | IfcPropertySingleValue.Name | IfcPropertySingleValue.Name | (Uri*)　　 |
| **プロパティの識別子** | Uri*(ClassPropertyの)* | IfcPropertySingleValue.Specification | IfcPropertySingleValue.Description | uri |
| **プロパティ事前定義値**（単一値） | *(ClassPropertyの)*定義済み値 | IfcPropertySingleValue.NominalValue | IfcPropertySingleValue.NominalValue | (Uri*) |
| **プロパティ単位**（単一値または列挙から） | *(PropertyまたはClassPropertyの)*定義済み値。 | IfcPropertySingleValue.Unit | IfcPropertySingleValue.Unit | (Uri*) |
| **プロパティの許容値**（列挙から） | AllowedValues *（Property または ClassProperty の）*。 | IfcPropertyEnumeratedValue 列挙値 | IfcPropertyEnumeratedValue 列挙値 | (Uri*) |
| **プロパティセット名** | プロパティセット*（ClassPropertyの）* | IfcPropertySet.Name | IfcPropertySet.Name | (Uri*) |

Uri* IDSは、bSDDの内容をコピーする代わりに、Uriを使ってbSDDを参照する。そのおかげで、Uriのリンクをたどっても情報にアクセスできる。uri="``http://identifier.buildingsmart.org/uri/<OrganizationCode>/<DictionaryCode>/<DictionaryVersion>/prop/<PropertyCode>``."_URIには、多くの情報が含まれていることに注意してください。

⚠️ **重要**  
bSDD では、プロパティはクラス (オブジェクト) とは無関係に存在する。したがって 

- `Property` の`AllowedValues` は、各プロパティのレベルで定義される。
- `Property` の`PredefinedValues` は、各クラス（オブジェクト）のレベルで定義される。
- プロパティとそのプロパティ・セットの関係は、各クラス（オブジェクト）のレベルで定義される。
- `AllowedValue`は、各クラス（オブジェクト）のレベルでも定義できる。この場合、`Property` のレベルで定義された`AllowedValue` は上書きされます。

bSDDに存在する人間が読みやすく翻訳可能な*Nameは*、IFC には反映されていない。そのため、*Codeは* IFC のデータセットで使われ、*Nameは*bSDDから名前を読み取ることのできるソフトウェアによってのみ表示されるということを覚えておくことが重要である。その理由は，ユーザーに表示される言語に関係なく，データセットが一貫した用語に従う必要があるからである． 
 
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
