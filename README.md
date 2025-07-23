> ## ⚠️ 注意
>
> - buildingSMART が公開している **bSDD リポジトリ** の直下にある **`README.md`** と  
>   **`Documentation/` フォルダ以下の `.md` ファイル** を対象に、差分を自動検知して  
>   **DeepL API** で機械翻訳した内容を掲載しています。  
> - **現在は試験運用中** につき、翻訳フローやドキュメント内容が今後変更される可能性があります。  
> - 用語の整合性チェックやレビューは未実施のため、**誤訳や不自然な表現** が含まれる場合があります。  
>   正確な情報が必要な際は、必ず原文もご確認ください。


[![Official repository by buildingSMART International](https://img.shields.io/badge/buildingSMART-Official%20Repository-orange.svg)](https://www.buildingsmart.org/)

<img src="Documentation/graphics/bSDD_logo.png"
     alt="bSDD logo"
     style="width: 200px" />

**The buildingSMART Data Dictionary (bSDD)** is an online service for hosting data dictionaries containing classifications, their properties, allowed values, units, translations, etc. It provides a standardized workflow to improve data quality and information consistency.

Read more at bSDD project page: https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/

### Overview

At the heart of bSDD is a canonical database, where all dictionaries can be related to each other. The main way to access the bSDD is through its [APIs (Application Programming Interfaces)](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1). This is how most BIM software and other apps can use the data stored in the bSDD. Apart from that, there is [the bSDD Search page](https://search.bsdd.buildingsmart.org/), where people can look up the content. Authors can publish content to bSDD through [the API](https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1) or [the bSDD Manage portal](https://manage.bsdd.buildingsmart.org/). To upload, please register your organisation using [the organisation registration form](https://bsi-technicalservices.atlassian.net/servicedesk/customer/portal/3/group/4/create/25).

<img src="https://github.com/buildingSMART/bSDD/assets/22922395/0b581c14-fd16-402f-baa8-c55eac500eff"
     alt="bSDD diagram"
     style="width: 500px" />

### Quick links

* [bSDD project page](https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/)
* [bSDD Search page]()
* [bSDD Manage portal]()
* [bSDD API Swagger page]()
* [bSDD updates forum]()
* [bSDD data structure](/Documentation/bSDD%20JSON%20import%20model.md)
* [bSDD JSON template](/Model/Import%20Model/bsdd-import-model.json) / [bSDD Excel template](/Model/Import%20Model/spreadsheet-import)
* [Tools integrating bSDD](https://technical.buildingsmart.org/resources/software-implementations/?filter_5%5B%5D=bSDD%20read%20API&filter_5%5B%5D=bSDD%20submit%2Fmanage&filter_5%5B%5D=bSDD%20IFC%20export%20(including%20URIs)&filter_1=&gv_search=&mode=any). This is a self-managed list, so feel free to add missing ones.
* [How to upload your data into the bSDD?](/Documentation/bSDD%20import%20tutorial.md)

### For developers

📢 We inform about planned and recently implemented bSDD updates in this forum topic:
[bSDD技術アップデート](https://forums.buildingsmart.org/t/bsdd-tech-updates/4889).

* **API documentation** https://github.com/buildingSMART/bSDD/blob/master/Documentation/bSDD%20API.md
* **API interactive documentation** on Swagger: https://app.swaggerhub.com/apis/buildingSMART/Dictionaries/v1

We also provide a **TEST** environment where the latest features are rolled out first and tested. If you want to check it out, here are the equivalent pages (not to be used by end-users!):
* **TEST API documentation** on Swagger: https://test.bsdd.buildingsmart.org/swagger/
* **TEST GraphQL** environment UI: [GraphQL UI](https://test.bsdd.buildingsmart.org/graphiql)
および関連する検索/管理ページ：
* **TESTサーチ**page: https://search-test.bsdd.buildingsmart.org/
* **テスト管理**ポータル：https://manage-test.bsdd.buildingsmart.org/

## お問い合わせ

ご質問、ご提案がございましたら、お気軽にお問い合わせください：[お問い合わせフォーム](https://share.hsforms.com/1RtgbtGyIQpCd7Cdwt2l67A2wx5h).

bSDDは私たちの活動のひとつです。[戦略的プロジェクト](https://www.buildingsmart.org/about/strategic-projects/)つまり、buildingSMARTインターナショナルは、bSDDの改善のための資金を提供するために、業界のスポンサーを募っているのである。
