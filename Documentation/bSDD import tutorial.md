このチュートリアルでは、bSDD コンテンツの公開と管理の方法について説明します。[bSDD 管理ポータル](https://manage.bsdd.buildingsmart.org/).

## 最初の辞書の出版

<h3 id="register">1. Register your organisation</h3>

bSDDの各データディクショナリは、登録された組織に代わって公開されます。 初めてアップロードする場合は、bSDDに組織を登録し、その組織にログインするために使用した電子メールアドレスを接続する必要があります。 そのためには、以下のフォームに記入してください。<a href="https://bsi-technicalservices.atlassian.net/servicedesk/customer/portal/3/group/4/create/25">団体登録フォーム</a>.

bSDD ハウスキーピングの一環として、各リクエストを手作業でレビューしており、数日かかることがあります。 返信を受け取り次第、次のステップに進むことができます。

> 組織を登録せずに、bSDD の実験だけを行いたいですか？ デモ組織に追加することができます。 この件やその他のご要望については、こちらまでご連絡ください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).

<h3 id="prepare">2. Prepare the content</h3>

bSDD へのデータアップロードの主な形式は、適切に構造化された JSON ファイルです。[データモデル・ドキュメント](https://technical.buildingsmart.org/services/bsdd/data-structure/)そのようなファイルが何を含み、どのように構成されるべきかを指定する。

このようなファイルを手動で作成するには<a href="https://github.com/buildingSMART/bSDD/blob/master/Model/Import%20Model/bsdd-import-model.json">JSONテンプレート</a>または<a href="https://github.com/buildingSMART/bSDD/tree/master/Model/Import%20Model/spreadsheet-import">エクセルテンプレートの説明</a>のいずれかを使用する。<a href="https://technical.buildingsmart.org/resources/software-implementations/?filter_5=bSDD+submit%2Fmanage&amp;mode=any">bSDDのデータ辞書を管理しアップロードするためのサードパーティツール</a>.

#### 一般的なガイドライン

- 必要な属性をすべて記入してください。
- コンテンツを分割してアップロードすることはできません。 1つの辞書のすべてのクラスとプロパティは、1つのファイルでなければなりません。
- 翻訳を別のファイルで管理し、公開する。
- 1つの辞書に多くのデータを入れようとしないでください。
- 新しいクラスをIFCエンティティにリンクすることで、ユーザビリティが向上します。 これにより、ソフトウェアがIFCでクラスをどのように表現するかを知ることができます。
- 既存のプロパティを複製するのではなく、コンテンツに追加します。
- クラスにプロパティを割り当てる場合は、モデル内でどのように構造化するかを知るために「プロパティセット」名を付けます（接頭辞「Pset_」の使用は避けてください。 これはIFCのみに限定されます）。
- 命名規則とガイドライン - 辞書名は一意である必要があります。 一般的すぎる名前の使用は避けてください。 他の辞書と競合する名前は避けてください。 たとえば、接頭辞が 'Ifc' のクラスは作成しないでください。 他の辞書の内容を複製することは避けてください。 ライセンスによっては、再配布や変更を許可していないものもあります。 コンテンツを辞書にリンクして再利用することは、良い習慣です。 たとえば、他の辞書のプロパティをクラスに追加することができます。 
- 辞書コード - 辞書コードは、bSDD内で一意である必要がある。 辞書名で認識できるものを選ぶ。 辞書コードは、すべてのリソースのURIを生成するために使用されるので、短く、できれば空白を含まないものであるべきである。 

**もっと読む**データ辞書を作成するためのグッドプラクティスについて：[https://technical.buildingsmart.org/services/bsdd/guidelines/](https://technical.buildingsmart.org/services/bsdd/guidelines/)

<h3 id="upload">3. Upload</h3>

こちらへ[bSDD 管理ポータル](https://manage.bsdd.buildingsmart.org/)まだbSDD buildingSMARTアカウントをお持ちでない場合は、"Sign up now "を、そうでない場合は、"Sign in "を選択してください。

> または<a href="https://technical.buildingsmart.org/resources/software-implementations/?filter_5=bSDD+submit%2Fmanage&amp;mode=any">bSDDのデータ辞書を管理しアップロードするためのサードパーティツール</a>と統合されている。<a href="https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1">bSDD API</a>.

> 注意: bSDD 管理ポータルが起動時にエラーを表示したり、スピナーアイコンが表示され続ける場合は、Ctrl-F5 を押してクッキーを更新してみてください。 それでもうまくいかない場合は、ブラウザの "シークレット" または "InPrivate" ウィンドウを開き、bSDD 管理ポータルに移動してみてください。 それでもうまくいかない場合は、お問い合わせください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).

辞書タブを開き、所属する組織を選択してください。 所属する組織が1つであれば、すぐにリストに表示されます。

ファイルを選択」ボタンを使用して、辞書JSONファイルをロードする。

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD%20management%20portal.png" alt="bSDD manage" style="width: 800px" />

テストアップロードは、コンテンツが2ヶ月後にbSDDから自動的に削除されることを意味し、間違いを防ぐためにステータスを「アクティブ」に設定することはできません。

> 注：bSDDの実験だけを行いたい場合は、オプションとして`TEST`としてアップロードされるため、初心者には安全なオプションです。`TEST`有効化することはできず、2ヶ月後に自動的に削除されます。

選択したファイルをアップロードする」を押す

各インポートの前に、まず「検証のみ行うか」オプションを使用することをお勧めします。これにより、ファイルをインポートしようとせずに、エラーや警告を通知することができます。

**重要**既存のファイルと同じバージョン番号の新しいファイルをアップロードすると、コンテンツが置き換わります（ステータスが`Preview`他のすべてのコンテンツが不変であるように[続きを読む](#the-lifecycle-of-a-dictionary)).

準備が整い、プラットフォームがエラーを返さなければ、"選択したファイルをアップロード "をクリックする。

ファイルのインポートが完了すると、より詳細なインポートレポートがEメールで届きます。 15分ほどかかる場合があります。 インポートルーチンがエラーを発見した場合は、Eメールに記載されます。

**重要**アップロードすることで、コンテンツが一般公開されます。 一般公開したくないものや、十分な許可を得ていないものは公開しないでください。 

> 注：特定のユーザーだけに辞書の可視性を制限することが可能です。 ただし、これはbSDDの有料機能です。 詳細を読む[プライベート辞書](https://technical.buildingsmart.org/services/bsdd/private-dictionaries/).

> 注：上記で説明したすべてのステップは、以下を使用して自動化することもできる。<a href="https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1">bSDD API</a>を統合した。

<h2 id="dictionary-lifecycle">The lifecycle of a dictionary</h2>

新しい辞書のバージョンをbSDDで公開する場合、その辞書は常に初期状態で`Preview`この段階では**再アップロード**コンテンツを修正する、**アクティブ化**または永久に**削除**それだ。

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/Content_lifecycle_workflow.jpg" alt="Lifecycle workflow" />

**⚠️ ひとたびコンテンツが有効化されると、そのコンテンツは不変の URI を取得する。つまり、そのコンテンツは永久に bSDD に留まり、削除されることはない。**に変更することは可能である。`Inactive`辞書のバージョンを有効にする前に、そのことを考慮してください。

<h2 id="dictionary-reupload">Publishing a new dictionary version</h2>

初めて公開する場合と同様に、適切に構造化されたJSONファイルをロードし、「アップロード」をクリックすることで、新しい辞書バージョンをアップロードすることもできます。

<h2 id="dictionary-status">Changing the dictionary status</h2>

少なくとも1つのバージョンの辞書がアップロードされるとすぐに、各バージョンの名前、バージョン番号、およびその他のプロパティを持つ行がテーブルに表示されます。 をクリックすることで、各バージョンのプロパティが表示されます。`action`あなたは、次のことができる。**ダウンロード**JSONファイルをコンピューターに保存します、**ステータス変更**への`Active`あるいは**削除**バージョン（どちらのオプションもステータスが`Preview`).

このオプションを有効にすると、ユーザーは辞書をプライベートなものに変更し、そのようなコンテンツにアクセスできるユーザーのリストを指定することができます。 プライベート辞書は有料オプションです。 詳しくはこちらをご覧ください：[プライベート辞書](https://technical.buildingsmart.org/services/bsdd/private-dictionaries/).

> つまり、bSDD APIを実装したサードパーティのソフトウェアでも同じ結果を得ることが可能です。 
