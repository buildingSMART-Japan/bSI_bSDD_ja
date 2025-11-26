このチュートリアルでは、[bSDD Manage ポータルを](https://manage.bsdd.buildingsmart.org/)使用して bSDD コンテンツを公開し、管理する方法を説明します。

## 最初の辞書の出版
<h3 id="register">1.組織の登録</h3>

bSDDの各データ辞書は、登録された組織に代わって公開されます。初めてアップロードする場合は、bSDDに組織を登録し、その組織にログインするために使用した電子メールアドレスを接続する必要があります。そのためには、[組織登録フォームに](https://bsi-technicalservices.atlassian.net/servicedesk/customer/portal/3/group/4/create/25)記入してください。

bSDD ハウスキーピングの一環として、各リクエストを手作業でレビューしています。返信があり次第、次のステップに進むことができます。

> 組織を登録せずに bSDD の実験だけを行いたいですか？あなたの組織を DEMO 組織に追加することができます。この件やその他のご要望については、こちらまでご連絡ください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).

<h3 id="prepare">2.コンテンツを準備する</h3>

bSDD へのデータアップロードの主な形式は、適切に構造化された JSON ファイルである。[データモデルのドキュメントでは](https://technical.buildingsmart.org/services/bsdd/data-structure/)、そのようなファイルが何を含み、どのように構造化すべきかを指定しています。

このようなファイルは、[JSONテンプレートを](https://github.com/buildingSMART/bSDD/blob/master/Model/Import%20Model/bsdd-import-model.json)コピーして手動で作成するか、[Excelテンプレートの説明を](https://github.com/buildingSMART/bSDD/tree/master/Model/Import%20Model/spreadsheet-import)使用して作成することができます。あるいは、[bSDDのデータ辞書を管理し、アップロードするためのサードパーティツールの](https://technical.buildingsmart.org/resources/software-implementations/?filter_5=bSDD+submit%2Fmanage&amp;mode=any)いずれかを使用してください。

#### 一般的なガイドライン
- 必要な属性をすべて記入してください。
- 一部のコンテンツに分割してアップロードすることはできません。1つの辞書のすべてのクラスとプロパティは、1つのファイルでなければなりません。
- 翻訳を別のファイルで管理し、公開する。
- 1つの辞書に多くのデータを入れようとしないでください。
- 使いやすさを向上させるために、新しいクラスをIFC エンティティにリンクします。こうすることで、ソフトウェアはIFC でクラスをどのように表現するかを知ることができます。
- 既存のプロパティを複製するのではなく、コンテンツに追加します。
- クラスにプロパティを割り当てるときは、モデル内でどのように構造化するかを知るために'プロパティセット'名を付けます（Pset_'という接頭辞の使用は避けてください）。これは、IFC に限定されます)
- 命名規則とガイドライン - 辞書名は一意である必要がある。一般的すぎる名称の使用は避ける。他の辞書と衝突する名前は避ける。例えば、接頭辞が'Ifc のクラスは作成しないでください。他の辞書の内容を複製することは避けてください。ライセンスによっては、再配布や改変を認めていないものもあります。コンテンツを自分の辞書にリンクして再利用することは、良い習慣です。例えば、他の辞書のプロパティを自分のクラスに追加することができます。
- 辞書コード - 辞書コードは、bSDD内で一意である必要がある。辞書コードは、すべてのリソースのUriを生成するために使用されるので、短く、できれば空白を含まないべきである。

**もっと読む** データ辞書作成のグッドプラクティスについて [: https://technical.buildingsmart.org/services/bsdd/guidelines/](https://technical.buildingsmart.org/services/bsdd/guidelines/)

<h3 id="upload">3.アップロード</h3>

[bSDD Manageポータルに](https://manage.bsdd.buildingsmart.org/)アクセスします。bSDDのbuildingSMARTアカウントをまだお持ちでない場合は、今すぐサインアップを"選択し、そうでない場合は"サインインを"選択します。

> あるいは、[bSDD](https://technical.buildingsmart.org/resources/software-implementations/?filter_5=bSDD+submit%2Fmanage&amp;mode=any) [API](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1) と統合された[bSDD のデータ辞書を管理し、アップロードするためのサードパーティツールの](https://technical.buildingsmart.org/resources/software-implementations/?filter_5=bSDD+submit%2Fmanage&amp;mode=any)ひとつを使用する。

> 注意: bSDD 管理ポータルが起動時にエラーを表示したり、スピナーアイコンが表示され続けたりする場合は、Ctrl-F5 を押してクッキーを更新してみてください。それでもうまくいかない場合は、ブラウザの"シークレット"ウィンドウまたは"プライベート"ウィンドウを開き、bSDD 管理ポータルに移動してみてください。それでもうまくいかない場合は、お問い合わせください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).

辞書タブを開き、所属する組織を選択してください。所属している組織が1つであれば、すぐにリストに表示されます。

ファイル選択"ボタンを使用して、辞書JSONファイルをロードする。

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/bSDD%20management%20portal.png" alt="bSDD manage" style="width: 800px" />

まず、ファイルにエラーがないかどうかを確認するか、テストアップロード'オプションを選択してテスト用にアップロードするオプションがあります。テストアップロードは、コンテンツが2ヶ月後にbSDDから自動的に削除されることを意味し、間違いを防ぐためにステータスを'アクティブ'に設定することはできません。

> 注意: bSDD を試してみたいだけなら、`TEST` アップロードのオプションを提供しています。これは初心者のための安全なオプションです。`TEST` としてアップロードされたコンテンツは有効化できず、2ヶ月後に自動的に削除されます。

"選択したファイルをアップロードする"

各インポートの前に、まず'検証のみ行うか'オプションを使用することをお勧めします。これにより、ファイルのインポートを試みることなく、エラーや警告が通知されます。

**重要**既存のファイルと同じバージョン番号の新しいファイルをアップロードすると、コンテンツが置き換わります（ステータスが`Preview` の場合のみ、その他のコンテンツは不変です[。）](#the-lifecycle-of-a-dictionary)

準備が整い、プラットフォームがエラーを返さなければ、"選択したファイルのアップロードを"クリックします"。

ファイルのインポートが完了すると、より詳細なインポートレポートがメールで届きます。最大15分かかる場合があります。インポートルーチンがエラーを発見した場合は、メールに記載されます。

**重要**アップロードすると、コンテンツが一般公開されます。一般に公開したくないもの、十分な許可を得ていないものは公開しないでください。 

> 注意：特定のユーザーだけに辞書の可視性を制限することは可能です。ただし、これはbSDDの有料機能です。[プライベート辞書について](https://technical.buildingsmart.org/services/bsdd/private-dictionaries/)もっと読む。

> 注: 上記で説明したすべての手順は、[bSDD API の](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1)統合を使用して自動化することもできます。

<h2 id="dictionary-lifecycle">辞書のライフサイクル</h2>

bSDDで新しい辞書バージョンを公開すると、その辞書は常に最初は`Preview` のステータスになる。この段階で、コンテンツを**再アップロードして**修正したり、そのバージョンを**アクティブに**したり、恒久的に**削除**したりすることができる。

<img src="https://raw.githubusercontent.com/buildingSMART/bSDD/master/Documentation/graphics/Content_lifecycle_workflow.jpg" alt="Lifecycle workflow" />

**⚠️ ひとたびコンテンツが有効化されると、それは不変の Uri* を取得する。つまり、コンテンツは永久に bSDD に残り、削除されることはない**。ステータスを`Inactive` に変更することは可能であり、それはもはや使用されるべきではないことを示すが、ページは依然として存在し、コンテンツを表示する。辞書のバージョンを有効にする前に、この点を考慮してください。

<h2 id="dictionary-reupload">新しい辞書バージョンの発行</h2>

初めて公開する場合と同様に、適切に構造化されたJSONファイルをロードし、「アップロード」をクリックすることで、新しい辞書バージョンをアップロードすることもできます。

<h2 id="dictionary-status">辞書ステータスの変更</h2>

辞書の少なくとも1つのバージョンがアップロードされるとすぐに、各バージョンの名前、バージョン番号、およびその他のプロパティを含む行がテーブルに表示されます。`action` をクリックすると、JSONファイルをコンピュータに**ダウンロード**したり、**ステータスを** `Active` に**変更**したり、バージョンを**削除**したりすることができます（どちらのオプションも、ステータスが`Preview` の場合にのみ利用できます）。

このオプションを有効にすると、ユーザーは辞書をプライベートなものに変更し、そのようなコンテンツにアクセスできるユーザーのリストを指定できる。プライベート辞書は有料オプションです。詳しくはこちらをご覧ください：[プライベート辞書](https://technical.buildingsmart.org/services/bsdd/private-dictionaries/)。

> つまり、bSDD APIを実装したサードパーティのソフトウェアでも、同じ結果を得ることが可能です。 
