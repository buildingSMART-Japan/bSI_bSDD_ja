# bSDDとGraphQL
## お知らせ
ネーミングもいくつか変更した：

1. "ドメイン"--&gt;"辞書"

1. "分類"→"クラス"

1. "NamespaceUri"--&gt;"Uri"

1. "IncludeChilds"--&gt;"IncludeChildren"

一貫性を持たせるため、GraphQL APIの名前も変更された。  
しかし、少なくとも2024年4月までは旧ネーミングをサポートする。

## GraphQL入門
通常の'APIは非常に静的である。リクエストを行うと、定義済みのデータセットが返ってくる。さらに情報が必要な場合は、おそらく別のAPIコールをする必要がある。そして、必要なデータがすべて得られるまで、また別の呼び出しが必要になるかもしれない。GraphQLはこの問題を克服するために設計された。必要なデータを指定できるクエリー言語である。

GraphQLの詳細については、例えば以下を参照のこと：
- https://dev.to/davinc/graphql-for-beginners-3f1a
- https://www.freecodecamp.org/news/a-beginners-guide-to-graphql-60e43b0a41f5/

シナリオによってはGraphQLを使用する方が効率的な場合もあるが、通常のAPIが最も効率的なソリューションであるシナリオもまだたくさんある。

## bSDD GraphQLエンドポイント
bSDD APIはGraphQLエンドポイントも提供しており、テスト環境にはプレイグラウンドもある：

遊び場：https://test.bsdd.buildingsmart.org/graphiql/  
テスト用GraphQLエンドポイント：https://test.bsdd.buildingsmart.org/graphql/  
テスト用GraphQLセキュアエンドポイント：https://test.bsdd.buildingsmart.org/graphqls/

本番用GraphQLセキュアエンドポイント：https://api.bsdd.buildingsmart.org/graphqls/

セキュアなAPIへのアクセス方法については、ドキュメントhttps://github.com/buildingSMART/bSDD/blob/master/Documentation/bSDD%20API.md。セキュアなGraphQLエンドポイントへのアクセスも同じです。

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
GraphQLでは、GraphQLスキーマに対してクエリーを実行することもできます（Introspectionとしても"知られています）。それを使って、たとえば利用可能なフィールドやクエリを取得することができます：
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