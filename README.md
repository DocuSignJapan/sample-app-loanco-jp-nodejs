
### DocuSign LoanCo サンプルアプリケーション

LoanCoは、アプリケーションがDocuSign eSignature APIとやりとりする一般的な方法を示すサンプルローンアプリです。 さまざまなスイッチ（認証、組み込み署名、テンプレート）を変更して、追加のプラットフォームおよびAPI機能を表示し、独自のソリューションに簡単に追加できます。LoanCoは、3つの異なるローンワークフローを提供し、プラットフォームを通じて利用可能なさまざまな機能とワークフローを示しています。

#### 要件

- [Free Developer Sandbox](https://go.docusign.com/sandbox/productshot?elq=16799)
- [Node.js](https://nodejs.org/en/)


#### インストール 

    git clone <repo> 
    cd <repo directory>
    npm install
    npm start


#### 実行 

    npm start
    

#### 設定 

> DocuSign has multiple ways of authenticating your app. This example is using Code Grant, which requires us to store a ClientSecret in addition to the Integration Key. read more about different authentication methods at https://developers.docusign.com/esign-rest-api/guides/authentication


    DOCUSIGN_ENVIRONMENT=demo  // use "www" for production  
	DOCUSIGN_IK=               // Integration Key 
    DOCUSIGN_CLIENT_SECRET=    // Client Secret Key 
    EMPLOYEE_EMAIL=            // used for final recipient of Personal Loan
    EMPLOYEE_NAME=             // used for final recipient of Personal Loan
    LOCAL_RETURN_URL=http://localhost/   // change to the correct return url, with a trailing slash
    BRAND_ID=                  // not required, use to show a different Brand for the Sailboat example 
    GOOGLE_MAPS_API_KEY=       // required for Sailboat example to work
    GOOGLE_TAG_MANAGER=        // GTM-XYZ
    DEFAULT_EMAIL=             // for autofilling email input fields
    FORCE_HTTPS=               // force https by setting to true


##### テンプレート 

テンプレートは現在自動的には作成されません。自動車ローンテンプレートを作成するには、次の手順を実行します:

1. サンドボックス環境にログインし、テンプレートタブを開く: https://appdemo.docusign.com/templates  
1. "新規ボタン"を押し、"テンプレートのアップロード"をクリック 
1. "pdfs/template-auto-loan.json"ファイルをアップロードし、作成されたテンプレートをクリック
1. テンプレート名の横に表示されている"(i)"アイコン("Information"アイコン)をクリックし、"コピー"リンクをクリックして、テンプレートIDを取得 
1. エディタで"pdfs/template-auto-loan.json"ファイルを開き、その中に設定されているテンプレートIDを上記で取得したテンプレートIDで上書き 
1. `npm start`コマンドを実行し、サンプルアプリを再起動

> Todo: 初回起動時、本アプリは自動車ローン向けテンプレートを作成しようとします。このテンプレートは、`pdfs/template-auto-loan.json`で定義済みです。 


#### Herokuへのデプロイ

いくつかの前提条件:

- ローカル環境にHeroku Toolbelt/CLIがインストール済みである  
- レポジトリからローカルにクローン後、`.env`ファイルに環境変数を定義済み 
- heroku-condigコマンドをインストールし、Herokuにローカルで定義している環境変数と値を送信 (`heroku plugins:install heroku-config`)  


コマンド:  

    git clone <repo>
    cd <repo directory>

    # <fill out fields in .env file>

    # create heroku app
    heroku create    

    # test locally
    heroku local

    # push up .env file to heroku config (heroku plugins:install heroku-config)
    heroku config:push

    # push repo up to heroku 
    git push heroku master

    # view online
    heroku open
    


#### 発生しうるエラー  

    { 
        errorCode: 'ACCOUNT_LACKS_PERMISSIONS',
        message: 'This Account lacks sufficient permissions. Document Visibility has been specified.  This account does not have document visibility turned on.' 
    }

https://admindemo.docusign.com/sending-settings の設定にそって、http://imgur.com/j4VD6nd の設定を変更


    {
        errorCode: 'PLAN_ITEM_NOT_ENABLED',
        message: 'A requested plan item is not enabled for this account. Plan item: AllowRequireWetSign' 
    }

サポート(support@docusign.com)に連絡し、 お使いのアカウントで"Allow Require Wet Sign"機能を有効化するよう依頼して下さい。それから、https://admindemo.docusign.com/signing-settings の"Recipients"セクション以下にそって、http://imgur.com/a/mJ5WC の設定を変更して下さい。



#### APIツールとリンク

__Developer Center__  
https://developers.docusign.com

__API Code Examples__  
https://developers.docusign.com/esign-rest-api/code-examples

__API Documentation__  
https://developers.docusign.com/esign-rest-api/reference

__API Explorer__  
https://apiexplorer.docusign.com/  



#### ライセンス 

The DocuSign LoanCo Sample App is licensed under the MIT [License](LICENSE).



