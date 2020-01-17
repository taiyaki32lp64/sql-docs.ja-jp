---
title: Azure Key Vault を使用した TDE 拡張キー管理を設定する
description: SQL Server コネクタ for Microsoft Azure Key Vault をインストールし、構成するための手順。
ms.custom: seo-lt-2019
ms.date: 09/12/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 1ccffc653225645de94355707ae2116982d2deb4
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557535"
---
# <a name="sql-server-tde-extensible-key-management-using-azure-key-vault---setup-steps"></a>Azure Key Vault を使用する SQL Server TDE 拡張キー管理 - 設定手順
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  以下の手順では、Azure Key Vault 用の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタのインストールと構成について説明します。  
  
## <a name="before-you-start"></a>開始前の準備  
 SQL Server で Azure Key Vault を使用するには、次の前提条件を満たす必要があります。  
  
-   Azure サブスクリプションを所有していること。  
  
-   最新の [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) (5.2.0 以降) がインストールされていること。  

-   Azure Active Directory を作成する。  

-   「[Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)」を読んで、Azure Key Vault を使用した EKM の保存の原理について熟知していること。  

-   実行中の SQL Server のバージョンに基づいて、適切なバージョンの Visual Studio C++ 再頒布可能パッケージをインストールしておくこと。
  
SQL Server のバージョン  |再頒布可能パッケージのインストール リンク    
---------|--------- 
2008、2008 R2、2012、2014 | [Visual Studio 2013 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual Studio 2015 の Visual C++ 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>パート I: Azure Active Directory サービス プリンシパルをセットアップする  
 SQL Server のアクセス権を Azure Key Vault に付与するためには、Azure Active Directory (AAD) にサービス プリンシパル アカウントが必要です。  
  
1.  [Azure Portal](https://ms.portal.azure.com/) に移動してサインインします。  
  
2.  アプリケーションを Azure Active Directory に登録します。 アプリケーションを登録する詳しい手順については、 **Azure Key Vault のブログ記事** の「 [Get an identity for the application (アプリケーションの ID を取得する)](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)」セクションを参照してください。  
  
3.  この後の手順のために、 **クライアント ID** と **クライアント シークレット** をコピーします。Key Vault へのアクセス権を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に付与するときに使用します。  
  
 ![ekm-client-id](../../../relational-databases/security/encryption/media/ekm-client-id.png "ekm-client-id")  
  
 ![ekm-key-id](../../../relational-databases/security/encryption/media/ekm-key-id.png "ekm-key-id")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>パート II: Key Vault とキーを作成する  
 ここで作成される Key Vault とキーは、SQL Server データベース エンジンが暗号化キーを保護するために使用します。  
  
> [!IMPORTANT]  
>  Key Vault が作成されるサブスクリプションは、Azure Active Directory サービス プリンシパルの作成先と同じ既定の Azure Active Directory に存在している必要があります。 SQL Server コネクタのサービス プリンシパルを作成する際に既定の Active Directory ではない Active Directory を使用する場合、Key Vault を作成する前に、Azure アカウントの既定の Active Directory を変更する必要があります。 既定の Active Directory を別の Active Directory に変更する方法については、SQL Server コネクタの [FAQ](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)を参照してください。  
  
1.  **PowerShell を開いてサインインする**  
  
     [最新の Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) (5.2.0 以降) をインストールして起動します。 次のコマンドを使用して Azure アカウントにサインインします。  
  
    ```powershell  
    Connect-AzAccount  
    ```  
  
     このステートメントからは次の情報が返されます。  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  複数のサブスクリプションの中から資格情報コンテナーで使用する特定のサブスクリプションを指定する場合は、 `Get-AzSubscription` でサブスクリプションを表示し、 `Select-AzSubscription` で正しいサブスクリプションを選択します。 指定しなかった場合、いずれかのサブスクリプションが PowerShell によって既定で選択されます。  
  
2.  **新しいリソース グループを作成する**  
  
     Azure Resource Manager で作成されるすべての Azure リソースは、リソース グループに属している必要があります。 そこで、Key Vault の従属先となるリソース グループを作成します。 この例では、`ContosoDevRG` を使用します。 すべての Key Vault 名はグローバルに **一意** であるため、リソース グループと Key Vault には独自の一意の名前を選択します。  
  
    ```powershell  
    New-AzResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     このステートメントからは次の情報が返されます。  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  `-Location parameter`については、コマンド `Get-AzureLocation` を使用して、この例とは別の場所を指定する方法を確認します。 さらに詳しい情報が必要な場合は、次のように入力します。 `Get-Help Get-AzureLocation`  
  
3.  **キー コンテナーの作成**  
  
     `New-AzKeyVault` コマンドレットには、リソース グループ名、Key Vault 名、地理的位置を指定する必要があります。 たとえば、 `ContosoDevKeyVault`という名前の Key Vault の場合、次のように入力します。  
  
    ```powershell  
    New-AzKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     Key Vault の名前を記録しておきます。  
  
     このステートメントからは次の情報が返されます。  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :   
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,   
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
4.  **Azure Active Directory サービス プリンシパルが Key Vault にアクセスするための権限を付与する**  
  
     Key Vault の使用を他のユーザーやアプリケーションに承認することができます。   
    このケースでは、パート I で作成した Azure Active Directory サービス プリンシパルを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを承認してみましょう。  
  
    > [!IMPORTANT]  
    >  Azure Active Directory サービス プリンシパルには、Key Vault に対して少なくとも `get`、`wrapKey`、および `unwrapKey` の権限が必要です。  
  
     **パラメーターには、以下のように、パート I でコピーした** クライアント ID `ServicePrincipalName` を使用します。 `Set-AzKeyVaultAccessPolicy` は、メッセージを伴わずに実行されます。正常に実行されたとしても何も出力されません。  
  
    ```powershell  
    Set-AzKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, wrapKey, unwrapKey  
    ```  
  
     権限を確認するには、 `Get-AzKeyVault` コマンドレットを呼び出します。 このステートメントから返された出力結果の "Access Policies" に、この Key Vault にアクセスできるもう 1 つのテナントとして AAD アプリケーションの名前が表示されます。  
  
       
5.  **Key Vault に非対称キーを生成する**  
  
     Azure Key Vault には、2 とおりの方法でキーを生成できます。1) 既存のキーをインポートする方法と、2) 新しいキーを作成する方法です。  
                  
      > [!NOTE]
        >  SQL Server は、2048 ビットの RSA キーのみをサポートします。
        
    ### <a name="best-practice"></a>ベスト プラクティス:
    
    すばやいキー復旧を確保し、Azure 以外のデータにアクセスできるようにするには、次のベスト プラクティスをお勧めします。
 
    1. ローカル HSM デバイス上で暗号化キーをローカルに作成します。 (SQL Server によってサポートされるように、必ず非対称の RSA 2048 キーを作成してください)。
    2. 暗号化キーを Azure Key Vault にインポートします。 その方法については、以下の手順を参照してください。
    3. 初めて Azure Key Vault でキーを使用する前に、Azure Key Vault キーのバックアップを作成します。 Backup-AzureKeyVaultKey コマンドの詳細については、[こちら](/sql/relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault)をご覧ください。
    4. キーに何らかの変更を加える場合 (ACL の追加、タグの追加、キー属性の追加など) は常に、新しい Azure Key Vault キーのバックアップを作成してください。

        > [!NOTE]  
        >  キーのバックアップは、任意の場所に保存できるファイルを返す Azure Key Vault キー操作です。

    ### <a name="types-of-keys"></a>キーの種類:
    Azure Key Vault で生成できて SQL Server で動作するキーは 2 種類あります。 どちらも非対称の 2048 ビット RSA キーです。  
  
    -   **ソフトウェアによる保護:** ソフトウェアで処理され、保存状態で暗号化されます。 ソフトウェアによって保護されたキーに対する操作は、Azure Virtual Machines 上で行われます。 運用環境で使用されるキーには推奨されません。  
  
    -   **HSM による保護:** より強力なセキュリティを確保するために、ハードウェア セキュリティ モジュール (HSM) によってキーを作成、保護します。 キーのバージョンごとに約 1 ドルのコストがかかります。  
  
        > [!IMPORTANT]  
        >  SQL Server コネクタを使用する場合、キー名に使用できる文字は、"a ～ z"、"A ～ Z"、"0 ～ 9"、"-" に限られます。また、26 文字が長さの上限となります。   
        > Azure Key Vault に格納されている同じ名前でバージョンが異なるキーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタでは使用できません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって使用されている Azure Key Vault キーをローテーションするには、[ SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)に関するページの「キーのロールオーバー」の手順を参照してください。  

    ### <a name="import-an-existing-key"></a>既存のキーをインポートする   
  
    ソフトウェアによって保護された 2048 ビットの RSA キーが既にある場合は、そのキーを Azure Key Vault にアップロードしてもかまいません。 たとえば .PFX ファイルが `C:\\` ドライブに `softkey.pfx` という名前で保存されており、これを Azure Key Vault にアップロードする場合は、次のように入力して、変数 `securepfxpwd` に .PFX ファイルのパスワード `12987553` を設定します。  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString -String '12987553' `  
      -AsPlainText -Force  
    ```  
  
    次に、.PFX ファイルからキーをインポートするために、次のように入力できます。このファイルは、Key Vault サービスでハードウェア (推奨) によってキーを保護するファイルです。  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > 実稼働のシナリオでは、非対称キーをインポートする方法を強くお勧めします。管理者は、キーをキー エスクロー システムに預託できるからです。 資格情報コンテナー内で非対称キーを作成する方法の場合、秘密キーは資格情報コンテナーの外に出ることがないため、エスクローに預託することができません。 重要なデータの保護に使用するキーはエスクローに預託してください。 非対称キーを紛失すると、データが永久的に失われます。  

    ### <a name="create-a-new-key"></a>新しいキーを作成する
    #### <a name="example"></a>例:  
    または、新しい暗号化キーを Azure Key Vault に直接作成し、ソフトウェアまたは HSM で保護することもできます。  この例では、ソフトウェアによって保護されるキーを `Add-AzureKeyVaultKey cmdlet` で作成します。  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    このステートメントからは次の情報が返されます。  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  
 > [!IMPORTANT]  
 > Key Vault は、同じ名前を持った複数バージョンのキーをサポートしていますが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタで使用するキーについては、複数のバージョンを使用したりロールオーバーしたりすることは避けてください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化に使用するキーをロールしたいと管理者が考える場合は、コンテナー内に別の名前で新しいキーを作成し、DEK を暗号化するために使用してください。  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>パート III:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタをインストールする  
 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?LinkId=521700)から SQL Server コネクタをダウンロードします。 (この作業は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンピューターの管理者が行う必要があります。)  

> [!NOTE]  
>  1\.0.0.440 以前のバージョンは置き換えられ、実稼働環境ではサポートされなくなりました。 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=45344)にアクセスし、[[SQL Server コネクタのメンテナンスとトラブルシューティング]](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) ページの "SQL Server コネクタのアップグレード" に示されている手順を使用して、バージョン 1.0.1.0 以降にアップグレードしてください。

> [!NOTE]  
> バージョン 1.0.5.0 では、サムプリントのアルゴリズムについて破壊的変更があります。 バージョン 1.0.5.0 にアップグレードした後、データベースの復元でエラーが発生する可能性があります。 サポート技術情報の記事 [447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0) をご覧ください。
  
 ![ekm-connector-install](../../../relational-databases/security/encryption/media/ekm-connector-install.png "ekm-connector-install")  
  
 既定では、コネクタは C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault にインストールされます。 この場所は、セットアップ中に変更することができます。 (変更した場合は、以下のスクリプトを調整してください。)  
  
 コネクタ用のインターフェイスはありませんが、正常にインストールされた場合はコンピューターに **Microsoft.AzureKeyVaultService.EKM.dll** がインストールされます。 これは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ステートメントを使用して `CREATE CRYPTOGRAPHIC PROVIDER` に登録する必要のある暗号化 EKM プロバイダー DLL です。  
  
 SQL Server コネクタのインストールでは、必要に応じて、SQL Server の暗号化で使用するサンプル スクリプトをダウンロードすることもできます。  
  
 SQL Server コネクタのエラー コードの説明、構成設定、またはメンテナンス タスクを確認するには、このトピック末尾の付録を参照してください。  
  
-   [A.SQL Server コネクタのメンテナンス手順](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C.SQL Server コネクタのエラー コードの説明](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>パート IV:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を構成する  
 このセクションの各操作に最低限必要な権限レベルについては、「[B. よく寄せられる質問](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB) 」を参照してください。  
  
1.  **sqlcmd.exe または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio を起動する**  
  
2.  **EKM を使用するように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を構成する**  
  
     次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを実行して、EKM プロバイダーを使用するための構成を [!INCLUDE[ssDE](../../../includes/ssde-md.md)] に対して行います。  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **に EKM プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタを登録 (作成) する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     -- Azure Key Vault の EKM プロバイダーである [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタを使用して暗号化サービス プロバイダーを作成します。    
    この例では、 `AzureKeyVault_EKM_Prov`という名前を使用しています。  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  ファイル パスは 256 文字以内で指定してください。  
  
  
4.  **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインから Key Vault を使用するための [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の資格情報を設定する**  
  
     Key Vault のキーを使用して暗号化を実行する各ログインに対し、資格情報を追加する必要があります。 その例を次に示します。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化環境をセットアップして管理するために Key Vault を使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理者のログイン。  
  
    -   その他、Transparent Data Encryption (TDE) をはじめとする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化機能を有効にする可能性のある [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン。  
  
     資格情報とログインとの間には一対一の対応関係が存在します。 つまり、各ログインには一意の資格情報が必要です。  
  
     [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを以下のように変更します。  
  
    -   `IDENTITY` 引数 (`ContosoDevKeyVault`) を編集し、Azure Key Vault を参照するようにします。
        - **グローバル Azure** を使用している場合は、`IDENTITY` 引数をパート II で使用した実際の Azure Key Vault の名前に置き換えます。
        - **プライベート Azure クラウド** ( Azure Government、Azure China、Azure Germany など) を使用している場合は、 `IDENTITY` 引数をパート II のステップ 3 で返された Vault URI に置き換えます。 Vault URI に "https://" は含めないでください。   
    -   `SECRET` 引数の最初の部分を、パート I で使用した Azure Active Directory の **クライアント ID** に置き換えます。この例の **クライアント ID** は `EF5C8E094D2A4A769998D93440D8115D`です。  
  
        > [!IMPORTANT]  
        >  **クライアント ID**のハイフンは削除してください。  
  
    -   `SECRET` 引数の 2 番目の部分を、パート I で使用した **クライアント シークレット** に置き換えます。この例のパート 1 で使用した **クライアント シークレット** は `Replace-With-AAD-Client-Secret`です。 完成した `SECRET` 引数は、 *ハイフンを含まない*アルファベットと数字とから成る長い文字列になります。  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     **CREATE CREDENTIAL** 引数に変数を使用し、クライアント ID からのハイフンの削除をプログラムで行う方法の例については、「[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)」をご覧ください。  
  
5.  **で Azure Key Vault のキーを開く [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     新しいキーを作成したか、パート II での説明に従って非対称キーをインポートしたかにかかわらず、キーを開く必要があります。 次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトにご利用のキー名を指定することで、キーを開きます。  
  
    -   `CONTOSO_KEY` の部分は、実際に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でキーに割り当てる名前に置き換えます。  
  
    -   `ContosoRSAKey0` の部分は、Azure Key Vault 内の実際のキーの名前に置き換えます。  
  
    ```sql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>次の手順  
  
以上で基本的な構成は完了です。「 [SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)」を参照してください。   
  
## <a name="see-also"></a>参照  
 [Azure Key Vault を使用する拡張キー管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
