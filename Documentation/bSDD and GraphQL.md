# bSDD and GraphQL

## Notification

We've applied several changes in naming:

1. "Domain" --> "Dictionary"
2. "Classification" --> "Class"
3. "NamespaceUri" --> "Uri"
4. "IncludeChilds" --> "IncludeChildren"

To be consistent, names in our GraphQL API have also been changed.
しかし、少なくとも2024年4月までは旧ネーミングをサポートする。

## Short intro on GraphQL

A 'regular' API is quite static: you do a request and it returns a predefined set of data. If you need some more info you probably need to do another API call. And then maybe another call until you have got all the data you want. GraphQL is designed to overcome that issue: it is a query language with which you can specify the data you need.

For more info on GraphQL have a look at, for example:
- https://dev.to/davinc/graphql-for-beginners-3f1a
- https://www.freecodecamp.org/news/a-beginners-guide-to-graphql-60e43b0a41f5/

For some scenario's using GraphQL can be more efficient, but there are still lots of scenario's where a regular API is the most efficient solution.

## bSDD GraphQL endpoints

The bSDD API also provides a GraphQL endpoint and the test environment also has a playground:

Playground: https://test.bsdd.buildingsmart.org/graphiql/
テスト用GraphQLエンドポイント：https://test.bsdd.buildingsmart.org/graphql/
テスト用GraphQLセキュアエンドポイント：https://test.bsdd.buildingsmart.org/graphqls/

本番用GraphQLセキュアエンドポイント：https://api.bsdd.buildingsmart.org/graphqls/

セキュアなAPIにアクセスする方法については、ドキュメントhttps://github.com/buildingSMART/bSDD/blob/master/Documentation/bSDD%20API.md を参照してください。セキュアなGraphQLエンドポイントにアクセスする場合も同じです。

## データクエリの例

-- 利用可能な言語のリストを取得する：
```
{
  languages {
    isocode
  }
}
```
----

-- 国番号のリストを取得する：
```
{
  countries {
    code
  }
}
```
----

これらのクエリを1つにまとめることができる：
```
{
  languages {
    isocode
  }

  countries {
    code
  }
}
```
----

-- 辞書内のクラスを検索します：
```
{
  dictionary(uri : "https://identifier.buildingsmart.org/uri/sbe/swedishmaterials/1") {
    uri
    copyrightNotice
    languageCode
    classSearch(searchText: "asfaltbetong", languageCode: "sv-SE") {
      name
      uri
      synonyms
      relatedIfcEntityNames
      properties {
        name
        isRequired
        pattern
      }
    }
  }
}
```
----

-- 辞書のすべてのクラスとそのプロパティを取得します：

注意: このクエリは、多くのクラスを持つ辞書の実行に時間がかかります。
```
{
  dictionary(uri : "https://identifier.buildingsmart.org/uri/bs-agri/fruitvegs/1.0") {
    name
    version
    uri
    copyrightNotice
    languageCode
    status
    releaseDate
    license
    licenseUrl
    moreInfoUrl
    
    classSearch {
      code
      name
      uri
      definition
      documentReference
      synonyms
      relatedIfcEntityNames
      properties {
        code
        name
        uri
        description
        definition
        documentReference
        isRequired
        dataType
        example
        dimension
        physicalQuantity
        pattern
        allowedValues {
          code
          value
        }
        units
      }
    }
  }
}
```
----

-- 変数を使用して、クラスの詳細を取得する：
```
query ($dictionaryUri: String!, $uri: String!) {
  dictionary(uri: $dictionaryUri) {
    name
    uri
    class(uri: $uri, includeChildren: true) {
      activationDateUtc
      childs {
        name
        uri
      }
      classType
      code
      countriesOfUse
      countryOfOrigin
      creatorLanguageCode
      deActivationDateUtc
      definition
      deprecationExplanation
      documentReference
      name
      uri
      properties {
        name
        uri
      }
      relatedIfcEntityNames
      relations {
        relatedClassName
        relatedClassUri
        relationType
      }
      replacedObjectCodes
      replacingObjectCodes
      revisionDateUtc
      status
      subdivisionsOfUse
      synonyms
      uid
      versionDateUtc
      versionNumber
      visualRepresentationUri
    }
  }
}
```
クエリ変数セクションでは、変数を定義する：
```
{
  "dictionaryUri": "https://identifier.buildingsmart.org/uri/sbe/swedishmaterials/1",
  "uri": "https://identifier.buildingsmart.org/uri/sbe/swedishmaterials/1/class/ACDE"
}
```
## メタデータ・クエリーの例

GraphQLでは、GraphQLスキーマに対してクエリーを実行することもできます（「イントロスペクション」とも呼ばれます）。 これを使用して、たとえば利用可能なフィールドやクエリーを取得することができます：
```
{
  __schema {
    types {
      name
      fields {
        name
        description
      }
    }
  }
}

query availableQueries {
  __schema {
    queryType {
      fields {
        name
        description
        type {
          kind
          name
          fields {
            name
            description
          }
        }
      }
    }
  }
}
```
イントロスペクションの他の例は、https://graphql.org/learn/introspection/ で見ることができる。