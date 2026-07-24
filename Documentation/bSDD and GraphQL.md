# bSDD と GraphQL
## 通知
命名規則について、いくつかの変更を加えました：

1. "ドメイン"--&gt;"辞書"

1. "分類"--&gt;"クラス"

1. "NamespaceUri"--&gt;"Uri"

1. "IncludeChilds"--&gt;"IncludeChildren"

一貫性を保つため、GraphQL API 内の名前も変更されました。  
ただし、少なくとも2024年4月までは、従来の名称も引き続きサポートします。

## GraphQLの簡単な紹介
通常の'APIはかなり静的です。リクエストを行うと、あらかじめ定義されたデータセットが返されます。さらに情報が必要な場合は、おそらく別のAPI呼び出しを行う必要があります。そして、必要なデータをすべて取得するまで、さらに別の呼び出しを繰り返すことになるでしょう。 GraphQLはこの問題を解決するために設計されています。これは、必要なデータを指定できるクエリ言語です。

GraphQLに関する詳細については、例えば以下のサイトをご覧ください：
- https://dev.to/davinc/graphql-for-beginners-3f1a
- https://www.freecodecamp.org/news/a-beginners-guide-to-graphql-60e43b0a41f5/

状況によってはGraphQLを使用したほうが効率的である場合もありますが、それでもなお、通常のAPIが最も効率的な解決策となるケースは数多くあります。

## bSDD GraphQL エンドポイント
bSDD API には GraphQL エンドポイントも用意されており、テスト環境にはプレイグラウンドも用意されています：

プレイグラウンド：https://test.bsdd.buildingsmart.org/graphiql/ GraphQLエンドポイントのテスト：https://test.bsdd.buildingsmart.org/graphql/ セキュリティ保護されたGraphQLエンドポイントのテスト：https://test.bsdd.buildingsmart.org/graphqls/



本番環境の GraphQL セキュアエンドポイント：https://api.bsdd.buildingsmart.org/graphqls/

セキュリティ保護されたAPIへのアクセス方法については、[bSDD APIドキュメント](bSDD%20API.md)を参照してください。セキュリティ保護されたGraphQLエンドポイントへのアクセスも、同様の方法で実行できます。

## データクエリの例
-- 利用可能な言語の一覧を取得する：
```
{
  languages {
    isocode
  }
}
```
----

-- 国コードの一覧を取得する：
```
{
  countries {
    code
  }
}
```
----

これらのクエリを1つにまとめることができます：
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

-- 辞書内のクラスを検索する：
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

-- 辞書形式のプロパティを持つすべてのクラスを取得する：

注意：クラスが多数含まれる辞書の場合、このクエリの実行には長い時間がかかります
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
クエリ変数セクションでは、以下の変数を定義します：
```
{
  "dictionaryUri": "https://identifier.buildingsmart.org/uri/sbe/swedishmaterials/1",
  "uri": "https://identifier.buildingsmart.org/uri/sbe/swedishmaterials/1/class/ACDE"
}
```
## メタデータクエリの例
GraphQL では、GraphQL スキーマに対してクエリを実行することもできます（これは"イントロスペクション"とも呼ばれます）。これを利用すると、たとえば、利用可能なフィールドやクエリを取得することができます：
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
イントロスペクションのその他の例については、https://graphql.org/learn/introspection/ をご覧ください。
