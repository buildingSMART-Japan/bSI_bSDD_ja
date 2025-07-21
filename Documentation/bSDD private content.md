### bSDDのプライベート辞書とは何ですか？
プライベート辞書は、指定されたユーザーのみがアクセスすることができる。 内容を見るには、ログインし、辞書の所有者から許可を得る必要がある。 

プライベート辞書は**有料機能**この機能にご興味のある方は、以下までご連絡ください。[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).  

### 辞書を非公開にするには？
アップロード権限を持つ組織ユーザーは、JSONファイルに行を追加することで、辞書をプライベートにすることができる：`IsPrivate: true,` **最初のアップロードで**その後のアップロードでこの設定を変更することはできません。

辞書を非公開（または再び公開）にするもう1つの方法は、bSDD管理サイトを通じて手動で設定を変更することである：
→ "Dictionaries" → 'Make dictionary private' button for the desired dictionary. Such a dictionary needs to be uploaded as public first.

![イメージ](https://github.com/buildingSMART/bSDD/assets/22922395/771ce6f5-45ab-4704-ad36-ba2670664654)


### 誰が私のプライベート辞書にアクセスできますか？
1. 組織ユーザー "としてリストアップされた人々（電子メールアドレス）（どのような権限であっても、組織ユーザーのリストに入っているだけでその組織のすべてのプライベート辞書にアクセスできる）。
2. アクセスは辞書ごとに許可されます。**ない**辞書のバージョンごと）：電子メールを提供して1人にアクセス権を与えるか、ホスト名（たとえば「buildingsmart.org」）を提供すると、そのホストの電子メールを持つすべての人が辞書にアクセスできる。

![イメージ](https://github.com/buildingSMART/bSDD/assets/22922395/8792271b-724e-4993-b400-b61b2ee263c0)

![イメージ](https://github.com/buildingSMART/bSDD/assets/22922395/517fc34e-020f-4e91-9b67-83a132a9e0e4)

### プライベートデータ辞書にアクセスするにはどうすればよいですか？
プライベート辞書データへのアクセスが許可されているユーザーとしてログインし、使用しているアプリケーショ ンがそれをサポートしている場合にのみ、プライベート辞書データにアクセスできます。

例えば、Swaggerページ（Production: https://app.swaggerhub.com/apis-docs/buildingSMART/Dictionaries/v1 / Test: https://test.bsdd.buildingsmart.org/swagger）を介してコンテンツにアクセスするには、セキュリティで保護されたAPIを認証して使用する必要があります。セキュリティで保護されていないAPIを介してデータにアクセスすることは可能ですが、Swaggerはそれをサポートしていません（セキュリティで保護されていないAPIの場合、swaggerはあなたの'トークン'を送信しないため、サーバはあなたが誰であるかを知りません）。

> 現在、検索サイトから個人情報にアクセスすることはできません（Production: https://search.bsdd.buildingsmart.org/ / Test: https://search-test.bsdd.buildingsmart.org）。
