
### DocuSign LoanCo サンプルアプリケーション

LoanCoは、アプリケーションがDocuSign eSignature APIとやりとりする一般的な方法を示すサンプルローンアプリです。 さまざまなスイッチ（認証、組み込み署名、テンプレート）を変更して、追加のプラットフォームおよびAPI機能を表示し、独自のソリューションに簡単に追加できます。LoanCoは、3つの異なるローンワークフローを提供し、プラットフォームを通じて利用可能なさまざまな機能とワークフローを示しています。

#### 要件

- [Free Developer Sandbox](https://secure.docusign.com/signup/develop)
- [Node.js](https://nodejs.org/en/)


#### インストール 

    git clone <repo> 
    cd <repo directory>
    npm install
    npm start


#### 実行 

    npm start
    

#### 設定 

> DocuSignには、アプリを認証する複数の方法があります。この例（ユーザー名 / パスワード / インテグレーターキーをローカルに保存し、カスタム`X-DocuSign-Authentication` ヘッダーに設定して送信する）は、[レガシー認証](https://docs.docusign.com/esign/guide/authentication/legacy_auth.html)と呼ばれています。また、[OAuth2] (https://docs.docusign.com/esign/guide/authentication/auth_server.html) Authorization Code GrantメソッドとImplicit Grantメソッドを使用して認証することもできます。

環境変数を使用して構成を設定します。これらの変数は、ルートの `.env`ファイルに格納することができます(`dotenv`パッケージが使用されます) 

    DOCUSIGN_ENVIRONMENT=demo  // use "www" for production  
    DOCUSIGN_USERNAME=         // account email address  
    DOCUSIGN_PASSWORD=         // account password
    DOCUSIGN_IK=               // Integrator Key 
    EMPLOYEE_EMAIL=            // used for final recipient of Personal Loan
    EMPLOYEE_NAME=             // used for final recipient of Personal Loan
    LOCAL_RETURN_URL=http://localhost/   // change to the correct return url, with a trailing slash
    BRAND_ID=                  // not required, use to show a different Brand for the Sailboat example 
    GOOGLE_MAPS_API_KEY=       // required for Sailboat example to work
    GOOGLE_ANALYTICS=          // UA-XYZ-1
    DEFAULT_EMAIL=             // for autofilling email input fields
    FORCE_HTTPS=               // force https by setting to true
    USE_LOCAL_CERTS=           // Start HTTPS listening with ./sslcerts by true. if false, HTTP server only


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
https://www.docusign.com/devcenter

__API レシピ (code walkthroughs)__  
https://www.docusign.com/developer-center/recipes

__API Documentation__  
https://docs.docusign.com/  

__API Explorer__  
https://apiexplorer.docusign.com/  



#### ライセンス 

The DocuSign LoanCo Sample App is licensed under the MIT [License](LICENSE).



