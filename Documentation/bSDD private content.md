### What is a private dictionary in bSDD?
A private dictionary can only be accessed by designated users. To see the content, they need to be logged in and have permission from the dictionary owner. 

Private dictionaries are **a paid feature** of bSDD, priced individually. If you are interested in this feature, please contact [CONTACT FORM](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).  

### How to make a dictionary private?
Organization users with upload rights can make a dictionary Private by adding a line to their JSON files: `IsPrivate: true,` **in the first upload** of a dictionary. Subsequent uploads cannot change this setting.

Another option to make a dictionary private (or public again) is by manually changing the setting via the bSDD Management site:
→ このような辞書は、最初に公開辞書としてアップロードされる必要がある。

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
