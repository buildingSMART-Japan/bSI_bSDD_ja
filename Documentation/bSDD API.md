## bSDD API
bSDD API は、以下のメソッドを提供します。`Class`そして`Property`IFCやETIMのような多くの辞書（規格）の情報。 フローの例は以下の通り：
* ユーザがクラスとそのプロパティを検索する画面を開く
* 画面を開いた後、アプリはAPIの "Dictionary "メソッドを呼び出し、利用可能な辞書のリストを取得する。 このリストをユーザーに提示して選択させることができる。
* ユーザーは辞書を選択し、必要なクラスを検索するためにテキストを入力します。
* ユーザーがSearchを押すと、アプリがbSDD APIにリクエストを送る（"SearchList "メソッド）
* 結果はクラスのリストです。
* ユーザーは必要なものを選ぶことができる
* アプリは、bSDD APIにクラスの詳細とプロパティのリクエストを送信します（"Class "メソッド）。
* APIはクラスの詳細とプロパティを返し、アプリはそれをユーザーに表示します。

典型的な使用例はSketchUpで実演されている。 SketchUpの使用例とbSDDプラグインのビデオはhttps://vimeo.com/446417661/ff8b6605d3。

**bSDD API は定期的に更新される。**APIに破壊的な変更があった場合、新しいバージョンを作成し、変更発生から6ヶ月間は両方のバージョンをサポートします。 既存のAPIへの追加は通常、破壊的な変更を意味せず、同じバージョンに導入することができます。

## API契約とAPIのテスト
API契約に関する情報は以下から入手できます。[bSDD API契約、正式リリース](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1)また、APIメソッドをテストすることもできます。 セキュリティで保護されたメソッドにはロックが付いています。 セキュリティで保護されたメソッドにアクセスするには、UIからAuthorizeボタンでログインする必要があります：

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/swagger-authorize2.png" alt="Swagger authorization" style="width: 550px" />

次のclient_idを入力してください： b222e220-1f71-4962-9184-05e0481a390d

リード」スコープのチェックをお忘れなく！

## https://identifier.buildingsmart.org
のデータにアクセスできる。`Class`または`Property`のURIを直接経由することもできる。`Class`または`Property`例えば、ブラウザでhttps://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3/class/IfcWall、そのクラスのデータが視覚的に表示されます。JSON形式で出力したい場合は、"application/JSON "を指定して "Accept "ヘッダを送信すると、JSON形式の結果が得られます。 このJSON形式の結果は、HTML形式の結果とは内容が異なります！

重要: これらの識別子 URI をシステム間の通信に使用しないでください! まず第一に、これはサーバからサーバへの余分な「ホップ」をもたらします。 第二に、あなたはそれが使用している API のバージョンを制御することができません。 bSDD の新しいリリースが公開された後と、公開される前とでは、結果が異なるかもしれません。

> 注： https://identifier.buildingsmart.org URLを直接呼び出してJSON形式のデータを取得することは、現在廃止されています。 代わりにapi/Class/vXまたはapi/Property/vXを使用してください。

## bSDDテスト環境

bSDDには、bSDDの新しい開発をテストするためのTEST環境があります。 内部使用のためのものですが、bSDDのAPIを使用したい開発者は、開発目的のためにTEST環境を使用することを歓迎します。 私たちは、その環境のSLAを持っていませんし、その内容をユーザーに見せることをお勧めしません。 もしあなたが辞書の所有者で、データのチェックやアップロードプロセスのテストをしたい場合は、公式のbSDDを使用してください。

## GraphQL
データはGraphQL経由でもアクセスできる。 こちらで試すことができる：
[GraphiQL TEST playground](https://test.bsdd.buildingsmart.org/graphiql).


GraphQLリクエストを送信するURLは以下の通り：
- 公式リリース：https://api.bsdd.buildingsmart.org/graphqls（セキュリティで保護されているため、末尾の "s "に注意）
- テスト版：https://test.bsdd.buildingsmart.org/graphql（セキュアではない）
- テスト版：https://test.bsdd.buildingsmart.org/graphqls (保護された)
Note: those URLs are not hyperlinks and do not work in a browser. You need to send a POST request with the query data (the GET request does not work).

ここでは、セキュリティで保護された bSDD API にアクセスするためのコード例を示します：[bSDD GraphQLの例](https://github.com/buildingSMART/bSDD/blob/master/Documentation/bSDD%20and%20GraphQL.md)導入に際してサポートが必要な場合はお問い合わせください。
 
## クライアント開発者向け

### Httpヘッダー "(X-)User-Agent"
各 HTTP 呼び出しの HTTP ヘッダ "User-Agent" (または "X-User-Agent") に、アプリケーションの名前とバージョンを含めてください。 これにより、bSDD の使用状況をよりよく追跡し、bSDD API を使用するアプリケーションに関する統計情報を提供することができます。 好ましい形式は "application/version" です。

### 安全なAPI
セキュリティで保護されたAPIを使用するクライアントを構築する場合は、クライアントIDを要求する必要があります。 そのためには、電子メールを送信してください：
- クライアントアプリケーションの名前
- アプリケーションのタイプ：
  - ウェブアプリケーション
  - シングル・ページ・アプリケーション
  - iOS/macOS、Objective-C、Swift、Xamarin
  - アンドロイド - Java、Kotlin、Xamarin
  - モバイル/デスクトップ
- どの言語を使用していますか？ (使用するライブラリによって、設定するredirectUriが異なる場合があります)
- ウェブサイトまたはSPAの場合、リターンURLを指定します（ログインページは、ユーザーがログインした後、このURLにリダイレクトされます）。

セキュアAPIを使用せず、ウェブサイトやSPAから他のAPIを呼び出したい場合は、CORSを許可するウェブサイトのURLが必要です。
If you're creating a desktop client that only calls the non-secured APIs, you're ready to go.

### 認証
認証にはAzure Active Directory B2Cを使用する。
At this moment, you need to authenticate only a few methods. This might change.

Javascript、Java、Angular、React、Python、または.NETアプリケーションを開発している場合、Microsoft Authentication Library (MSAL)を使用すれば、buildingSMART Data Dictionary APIとの接続が最も簡単です。
See [Active directory B2C code samples](https://docs.microsoft.com/en-us/azure/active-directory-b2c/code-samples) for ready-to-use examples on how to use the MSAL. You can find the bSDD API-specific settings in one of the next sections of this document. Make sure you have the settings in an easy-to-update settings file. 
You can find the code for a small .NET console application that accesses the bSDD API (authenticated) in this repository: [.NET console example](https://github.com/buildingSMART/bSDD/tree/master/Source%20code%20examples/CSharp-Client-Console-Demo).

反応：https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-react
        https://github.com/Azure-Samples/ms-identity-javascript-react-tutorial/blob/main/1-Authentication/2-sign-in-b2c/README.md
Angular: https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-angular-auth-code
Java: https://docs.microsoft.com/en-us/samples/azure-samples/ms-identity-java-webapp/ms-identity-java-webapp/ 
Python: https://docs.microsoft.com/en-us/python/api/overview/azure/active-directory 

他の言語を使用して開発している場合でも、APIは標準のOpenAPI、OAuth2、OpenID Connectに従っているので、bSDD APIに接続することができます。

セキュリティで保護されたAPIにアクセスするには、まずユーザー登録が必要です。 MSALを使用している場合、このために必要な特別なことは何もありません。 ユーザーは、ブラウザウィンドウ経由でログインするよう促されます。 ユーザーがbuildingSMART APIアカウントを持っていない場合、サインアップすることができます：

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bs-signupsignin.png" alt="bSDD sign up / sign in" style="width: 350px" />

ユーザーはbuildingSMART Azure B2C Active Directoryに登録されます。
Currently there’s no further authorization required to be able to use the API.

### 設定
これらは、Dekstopクライアントアプリのデモ用に使用できる設定です：
* テナント： "buildingsmartservices.onmicrosoft.com"
* AzureAdB2Chostname: "authentication.buildingsmart.org"
* ClientId: "4aba821f-d4ff-498b-a462-c2837dbbba70"
* RedirectUri: "com.onmicrosoft.bsddprototypeb2c.democonsoleapp://oauth/redirect"
* PolicySignUpSignIn: "b2c_1a_signupsignin_c"
* PolicyEditProfile: "b2c_1a_profileedit_c"
* PolicyResetPassword："b2c_1a_passwordreset_c"

* ApiScope : "https://buildingsmartservices.onmicrosoft.com/api/read"
* BsddApiUrl: "https://test.bsdd.buildingsmart.org"

完全なB2CオーソリティのURLは、https://authentication.buildingsmart.org/tfp/buildingsmartservices.onmicrosoft.com/b2c_1a_signupsignin_c（「tfp」の部分に注目！）。

公式リリースを使用する場合は、上記以外の設定を使用する必要があります：
* ClientId: クライアントIDを要求する。[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h)
* RedirectUri：どのようなアプリを、どのような技術で作っているかを教えてください。
* ApiScope : "https://buildingsmartservices.onmicrosoft.com/bsddapi/read"
* BsddApiUrl: "https://api.bsdd.buildingsmart.org"


bSDD API を使用するウェブアプリケーションを開発している場合は、ぜひお知らせください ([お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h)RedirectURIはAzure ADで設定する必要がある。

### 追加情報
認可フローの言語に依存しない記述：[認証コードの流れ](https://docs.microsoft.com/en-us/azure/active-directory-b2c/authorization-code-flow)

さまざまな認証フローを高レベルで説明する：[AD B2Cアプリケーションの種類](https://docs.microsoft.com/en-us/azure/active-directory-b2c/application-types)

Oauth2 と OpenId プロトコルの説明：[AD B2Cプロトコルの概要](https://docs.microsoft.com/en-us/azure/active-directory-b2c/protocols-overview)

