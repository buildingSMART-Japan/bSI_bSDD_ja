## bSDD API
bSDD API は、IFC や ETIM のような多くの辞書（規格）の`Class` と`Property` 情報を取得するメソッドを提供します。フロー例は以下の通りです：
* ユーザがクラスとそのプロパティを検索する画面を開く
* 画面を開いた後、アプリはAPIの "Dictionary "メソッドを呼び出し、利用可能な辞書のリストを取得する。このリストをユーザーに提示して選択させることができる。
* ユーザーは辞書を選択し、必要なクラスを検索するためにテキストを入力します。
* ユーザーがSearchを押すと、アプリがbSDD APIにリクエストを送る（"SearchList "メソッド）
* 結果はクラスのリストです。
* ユーザーは必要なものを選ぶことができる
* アプリは、bSDD APIにクラスの詳細とプロパティのリクエストを送信します（"Class "メソッド）。
* APIはクラスの詳細とプロパティを返し、アプリはそれをユーザーに表示します。

典型的なユースケースをSketchUpで実演しています。SketchUpの使用例とbSDDプラグインのビデオはhttps://vimeo.com/446417661/ff8b6605d3。

**bSDD API は定期的に更新される。**APIに破壊的な変更があった場合、私たちは新しいバージョンを作成し、変更が発生してから6ヶ月間は両方のバージョンをサポートします。既存のAPIへの追加は、通常、破壊的な変更を意味せず、同じバージョンに導入することができる。

## API契約とAPIのテスト
API契約情報は、[bSDD API contract, official releaseで](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1)入手できます。この情報はログインすることなく入手できます。APIメソッドをテストすることもできます。セキュリティで保護されたメソッドにはロックがかかっています。セキュリティで保護されたメソッドにアクセスするには、UIからAuthorizeボタンでログインする必要があります：

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/swagger-authorize2.png" alt="Swagger authorization" style="width: 550px" />

次のclient_idを入力してください： b222e220-1f71-4962-9184-05e0481a390d

"read "スコープのチェックをお忘れなく！

## https://identifier.buildingsmart.org
`Class` や`Property` のデータには、`Class` や`Property` の URI から直接アクセスすることもできます。例えば、ブラウザで https://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall に移動すると、そのクラスのデータが視覚的に表示されます。JSON形式の出力が必要な場合、"application/JSON "の "Accept "ヘッダを送信すると、JSON形式の結果が得られます。このJSON結果の内容は、HTML結果とは異なります！

重要：これらの識別子URIをシステム間通信に使用しないでください！まず第一に、サーバーからサーバーへ余計な「ホップ」が発生します。第二に、使用している API のバージョンを制御することができません。bSDD の新しいリリースが発行された後の結果は、リリース前の結果と異なるかもしれません。

&gt; 注: https://identifier.buildingsmart.org URLを直接呼び出してJSON形式のデータを取得することは、現在廃止されています。代わりにapi/Class/vXまたはapi/Property/vXを使用してください。

## bSDDテスト環境
bSDD には、bSDD の新しい開発をテストするための TEST 環境があります。内部使用のためのものですが、bSDD の API を使いたい開発者は、開発目的で TEST 環境を使うことを歓迎します。私たちはこの環境のSLAを持っていませんし、その内容をユーザに見せることも推奨していません。もしあなたがディクショナリ所有者で、データのチェックやアップロードプロセスのテストをしたい場合は、公式のbSDDをご利用ください。

## GraphQL
データはGraphQLでもアクセスできる。こちらで試すことができる：  
[GraphiQL TESTのプレイグラウンド](https://test.bsdd.buildingsmart.org/graphiql)。


GraphQLリクエストを送信するURLは以下の通り：
- 公式リリース：https://api.bsdd.buildingsmart.org/graphqls（セキュリティで保護されているため、末尾の "s "に注意）
- テスト版：https://test.bsdd.buildingsmart.org/graphql（セキュアではない）
- テスト版：https://test.bsdd.buildingsmart.org/graphqls (保護された)
Note: those URLs are not hyperlinks and do not work in a browser. You need to send a POST request with the query data (the GET request does not work).

ここには、セキュアな bSDD API にアクセスするためのサンプルコードがあります:[bSDD GraphQL examples](https://github.com/buildingSMART/bSDD/blob/master/Documentation/bSDD%20and%20GraphQL.md).これを実装する際にサポートが必要な場合は、お問い合わせください。
 
## クライアント開発者向け
### Httpヘッダー "(X-)User-Agent"
各 HTTP 呼び出しの HTTP ヘッダ "User-Agent" (または "X-User-Agent") に、アプリケーションの名前とバージョンを含めてください。これにより、bSDD の使用状況をよりよく追跡することができ、 bSDD API を使用しているあなたのアプリケーションに関する統計情報を提供することができます。望ましい形式は "application/version" で、たとえば "Autodesk.Revit/2024" などです。

### 安全なAPI
セキュリティで保護されたAPIを使用するクライアントを構築する場合は、クライアントIDを要求する必要があります。そのためには、私たちに電子メールを送信してください：
- クライアントアプリケーションの名前
- アプリケーションのタイプ：
  - ウェブアプリケーション
  - シングル・ページ・アプリケーション
  - iOS/macOS、Objective-C、Swift、Xamarin
  - アンドロイド - Java、Kotlin、Xamarin
  - モバイル/デスクトップ
- どの言語を使用していますか？(使用するライブラリによって設定すべきredirectUriが異なる場合があります)
- ウェブサイトまたはSPAの場合、リターンURLを指定します（ログインページは、ユーザーがログインした後、このURLにリダイレクトされます）。

セキュリティで保護されたAPIを使用せず、ウェブサイトやSPAから他のAPIを呼び出したい場合は、CORSを許可するウェブサイトのURLが必要です。  
セキュアでないAPIだけを呼び出すデスクトップ・クライアントを作成するのであれば、準備はできている。

### 認証
認証にはAzure Active Directory B2Cを使用する。  
現時点では、認証が必要なのはいくつかの方法のみです。これは変更される可能性があります。

Javascript、Java、Angular、React、Python、または.NETアプリケーションを開発している場合、Microsoft Authentication Library (MSAL)を使用すれば、buildingSMART Data Dictionary APIとの接続が最も簡単です。  
MSALの使用方法に関するすぐに使える例については、[Active directory B2Cコードサンプルを](https://docs.microsoft.com/en-us/azure/active-directory-b2c/code-samples)参照のこと。bSDD API固有の設定は、このドキュメントの次のセクションの1つにあります。更新しやすい設定ファイルに設定があることを確認してください。   
このリポジトリには、bSDD API (認証済み) にアクセスする小さな .NET コンソールアプリケーションのコードがあります[。](https://github.com/buildingSMART/bSDD/tree/master/Source%20code%20examples/CSharp-Client-Console-Demo)

反応：https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-react  
        https://github.com/Azure-Samples/ms-identity-javascript-react-tutorial/blob/main/1-Authentication/2-sign-in-b2c/README.md  
アングラー：https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-angular-auth-code  
Java: https://docs.microsoft.com/en-us/samples/azure-samples/ms-identity-java-webapp/ms-identity-java-webapp/   
Python: https://docs.microsoft.com/en-us/python/api/overview/azure/active-directory 

他の言語を使用して開発している場合でも、APIは標準のOpenAPI、OAuth2、OpenID Connectに従っているので、bSDD APIに接続することができます。

セキュリティで保護されたAPIにアクセスするには、まずユーザー登録が必要です。MSALを使用している場合、このために必要な特別なことは何もない。ユーザーは、ブラウザウィンドウ経由でログインするよう促されます。ユーザーがbuildingSMART APIのアカウントを持っていない場合は、サインアップすることができます：

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bs-signupsignin.png" alt="bSDD sign up / sign in" style="width: 350px" />

ユーザーはbuildingSMART Azure B2C Active Directoryに登録されます。  
現在、APIを使用するために必要な認証はない。

### 設定
これらは、Dekstopクライアントアプリのデモ用に使用できる設定です：
* テナント： "buildingsmartservices.onmicrosoft.com"
* AzureAdB2Chostname: "authentication.buildingsmart.org"
* ClientId: "4aba821f-d4ff-498b-a462-c2837dbbba70"
* RedirectUri: "com.onmicrosoft.bsddprototypeb2c.democonsoleapp://oauth/redirect"
* PolicySignUpSignIn："*b2c1asignupsignin_c*"
* PolicyEditProfile："*b2c1aprofileedit_c*"
* PolicyResetPassword: "*b2c1apasswordreset_c*"

* ApiScope : "https://buildingsmartservices.onmicrosoft.com/api/read"
* BsddApiUrl："https://test.bsdd.buildingsmart.org"

完全なB2CオーソリティのURLは、https://authentication.buildingsmart.org/tfp/buildingsmartservices.onmicrosoft.com/b2c_1a_signupsignin_c（「tfp」の部分に注目！）。

公式リリースを使用する場合は、上記以外の設定を使用する必要があります：
* ClientId:[CONTACT FORMを](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h)使用してクライアントIDをリクエストします。
* RedirectUri：どのようなアプリを、どのような技術で作っているかを教えてください。
* ApiScope : "https://buildingsmartservices.onmicrosoft.com/bsddapi/read"
* BsddApiUrl："https://api.bsdd.buildingsmart.org"


bSDD API を使用する Web アプリを開発する場合は、[CONTACT FORM](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h) までお知らせください。RedirectURI は Azure AD で設定する必要があります。

### 追加情報
認可フローの言語に依存しない記述：[認可コードフロー](https://docs.microsoft.com/en-us/azure/active-directory-b2c/authorization-code-flow)

さまざまな認証フローのハイレベル説明[AD B2C アプリケーション・タイプ](https://docs.microsoft.com/en-us/azure/active-directory-b2c/application-types)

Oauth2とOpenIdプロトコルの説明：[AD B2C プロトコルの概要](https://docs.microsoft.com/en-us/azure/active-directory-b2c/protocols-overview)

