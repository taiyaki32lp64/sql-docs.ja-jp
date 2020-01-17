---
title: Azure Key Vault を使用する拡張キー管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 9591b483380d8bfcaea8404cccfa0279d3bcc035
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957199"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Azure Key Vault を使用する拡張キー管理 (SQL Server)
  Azure Key Vault [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用の[!INCLUDE[msCoName](../../../includes/msconame-md.md)]コネクタを[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用すると、暗号化キーを保護するための[拡張キー管理 &#40;EKM&#41;](extensible-key-management-ekm.md)プロバイダーとして Azure Key Vault サービスを利用できます。  
  
 このトピックの内容:  
  
-   [EKM の使用](#Uses)  
  
-   [手順 1:SQL Server で使用する Key Vault の設定](#Step1)  
  
-   [手順 2:SQL Server コネクタのインストール](#Step2)  
  
-   [手順 3:EKM プロバイダーを Key Vault に使用する SQL Server の構成](#Step3)  
  
-   [例 A:Key Vault からの非対称キーを使用した透過的データ暗号化](#ExampleA)  
  
-   [例 B:Key Vault からの非対称キーを使用したバックアップの暗号化](#ExampleB)  
  
-   [例 C:Key Vault からの非対称キーを使用した列レベルの暗号化](#ExampleC)  
  
##  <a name="Uses"></a>EKM の使用  
 組織では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化を使用して秘密データを保護できます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]暗号化には、 [Transparent Data Encryption &#40;TDE&#41;](transparent-data-encryption.md)、[列レベルの暗号化](/sql/t-sql/functions/cryptographic-functions-transact-sql)(CLE)、および[バックアップの暗号化](../../backup-restore/backup-encryption.md)が含まれます。 これらのすべてのケースでは、対称なデータ暗号化キーを使用してデータが暗号化されます。 対称なデータ暗号化キーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に格納されたキーの階層で暗号化することにより、さらに保護されます。 それに対して、EKM プロバイダーのアーキテクチャでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の外側にある外部暗号化サービス プロバイダーに格納された非対称キーを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でデータの暗号化キーを保護できるようにします。 EKM プロバイダーのアーキテクチャを使用すると、さらにセキュリティ層を追加し、組織の中でキーとデータの管理を分離できます。  
  
 Azure Key Vault 用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタを使用すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は暗号化キーを保護する EKM プロバイダーとして拡張性、パフォーマンス、および可用性の高い Key Vault サービスを利用できます。 Key Vault サービスは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure Virtual Machines 上の [!INCLUDE[msCoName](../../../includes/msconame-md.md)] インストール環境で使用したり、オンプレミス サーバー用に使用したりすることが可能です。 また、資格情報コンテナー サービスでは、厳密な管理および監視下にあるハードウェア セキュリティ モジュール (HSM) を使用し、非対称暗号化キーをより高いレベルで保護するオプションも提供します。 資格情報コンテナーの詳細については、「 [Azure Key Vault](https://go.microsoft.com/fwlink/?LinkId=521401)」を参照してください。  
  
 次の図は、Key Vault を使用した EKM のプロセス フローについてまとためものです。 図の中にプロセス手順番号が示されていますが、図の後に示す設定手順の番号と対応しているわけではありません。  
  
 ![Azure Key Vault を使用した SQL Server EKM](../../../database-engine/media/ekm-using-azure-key-vault.png "Azure Key Vault を使用した SQL Server EKM")  
  
##  <a name="Step1"></a>手順 1: SQL Server で使用する Key Vault を設定する  
 次の手順では、暗号化キーを保護するために [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] で使用する資格情報コンテナーを設定する方法について説明します。 コンテナーは、組織内で既に使用中になっていることもあります。 資格情報コンテナーが存在しない場合は、暗号化キーを管理するように指名された組織内の Azure 管理者がコンテナーを作成し、コンテナー内に非対称キーを生成し、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によるキー使用を許可します。 Key Vault サービスについて習熟するため、「 [Azure Key Vault の使用を開始する](https://go.microsoft.com/fwlink/?LinkId=521402)」と、PowerShell の「 [Azure Key Vault のコマンドレット](https://docs.microsoft.com/powershell/module/azurerm.keyvault) 」をご確認ください。  
  
> [!IMPORTANT]  
>  複数の Azure サブスクリプションがある場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を含むサブスクリプションを使用する必要があります。  
  
1.  **コンテナーを作成します。**「 [Azure Key Vault の概要](https://go.microsoft.com/fwlink/?LinkId=521402)」の「 **Key vault を作成する**」セクションの手順に従って、コンテナーを作成します。 コンテナーの名前を記録しておきます。 このトピックでは、" **ContosoKeyVault** " という資格情報コンテナー名を使用します。  
  
2.  **次のように、資格情報コンテナーに非対称キーを生成します。** キーコンテナー内の非対称キーは、暗号化キーを[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]保護するために使用されます。 資格情報コンテナーから出て行くのは非対称キーの公開部分だけで、秘密の部分がコンテナーからエクスポートされることはありません。 非対称キーを使用するすべての暗号化操作は、Azure Key Vault に委任され、資格情報コンテナーのセキュリティで保護されます。  
  
     非対称キーを生成して資格情報コンテナーに格納する方法がいくつかあります。 外部からキーを生成し、キーを .pfx ファイルとして資格情報コンテナーにインポートします。 または、Key Vault の API を使用してキーを直接資格情報コンテナーに作成します。  
  
     
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタでは、非対称キーを 2048 ビット RSA にする必要があり、キー名に使用できるのは文字 "a ～ z"、"A ～ Z"、"0 ～ 9"、および "-" です。 このドキュメントでは、非対称キーの名前を **ContosoMasterKey**とします。 これは、キーに実際に使用する一意の名前で置き換えてください。  
  
    > [!IMPORTANT]  
    >  実稼働のシナリオでは、非対称キーをインポートする方法を強くお勧めします。管理者は、キーをキー エスクロー システムに預託できるからです。 資格情報コンテナー内で非対称キーを作成する方法の場合、秘密キーは資格情報コンテナーの外に出ることがないため、エスクローに預託することができません。 重要なデータの保護に使用するキーはエスクローに預託してください。 非対称キーを紛失すると、データが永久的に復元不能になります。  
  
    > [!IMPORTANT]  
    >  資格情報コンテナーでは、同じ名前を付けたキーの複数のバージョンがサポートされます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタで使用するキーは、バージョン管理したりロールしたりするべきではありません。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化に使用するキーをロールしたいと管理者が考える場合は、コンテナー内に別の名前で新しいキーを作成し、DEK を暗号化するために使用してください。  
  
     資格情報コンテナーにキーをインポートする方法、および資格情報コンテナー内でキーを作成する方法 (実稼働環境では推奨されません) の詳細については、「 **Azure Key Vault の使用を開始する**[」の「キーまたは秘密キーを資格情報コンテナーに追加する](https://go.microsoft.com/fwlink/?LinkId=521402)」セクションをご覧ください。  
  
3.  **SQL Server に使用する Azure Active Directory サービスプリンシパルを取得します。** 組織が Microsoft クラウドサービスにサインアップすると、Azure Active Directory が取得されます。 
  **が資格情報コンテナーにアクセスする時に (Azure Active Directory に対して自身を認証するために) 使用する** サービス プリンシパル [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を Azure Active Directory 内に作成します。  
  
    -   
  **
  ** で暗号化を使用するよう構成するときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理者が資格情報コンテナーにアクセスするために、1 つのサービス プリンシパル [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が必要になります。  
  
    -   
  **
  ** の暗号化で使用するラップ解除キーを取得するために [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] が資格情報コンテナーにアクセスするときに、もう 1 つのサービス プリンシパル [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が必要になります。  
  
     アプリケーションを登録してサービス プリンシパルを生成する方法の詳細については、「 **Azure Key Vault の使用を開始する** 」の「 [アプリケーションを Azure Active Directory に登録する](https://go.microsoft.com/fwlink/?LinkId=521402)」セクションをご覧ください。 この登録プロセスからは、Azure Active Directory の **サービス プリンシパル** ごとに、 **アプリケーション ID**( **クライアント ID** とも呼ばれる) および **認証キー**( **シークレット**とも呼ばれる) が返されます。 `CREATE CREDENTIAL`ステートメントで使用する場合は、**クライアント ID**からハイフンを削除する必要があります。 以下のスクリプトで使用するために、これらの情報を記録しておきます。  
  
    -   **Sysadmin**ログインの**サービスプリンシパル**: **CLIENTID_sysadmin_login**および**SECRET_sysadmin_login**  
  
    -   の**サービスプリンシパル** [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine**および**SECRET_DBEngine**。  
  
4.  **サービスプリンシパルが Key Vault にアクセスするためのアクセス許可を付与します。****CLIENTID_sysadmin_login**と**CLIENTID_DBEngineService**の両方のプリンシパルには、key vault での**get**、 **list**、 **wrapKey**、および**unwrapKey**権限が必要です。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を通してキーを作成する予定の場合は、資格情報コンテナーでの **create** 権限も付与する必要があります。  
  
    > [!IMPORTANT]  
    >  ユーザーは、この資格情報コンテナーに対しては、少なくとも **wrapKey** および **unwrapKey** 操作が必要です。  
  
     資格情報コンテナーに権限を付与する操作の詳細については、「 **Azure Key Vault の使用を開始する**[」の「キーまたはシークレットを使用できるようにアプリケーションを承認する](https://go.microsoft.com/fwlink/?LinkId=521402)」セクションご覧ください。  
  
     Azure Key Vault のドキュメントへのリンク  
  
    -   [Azure Key Vault とは](https://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [Azure Key Vault を使ってみる](https://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   PowerShell の [Azure Key Vault コマンドレット](https://docs.microsoft.com/powershell/module/azurerm.keyvault) のリファレンス  
  
##  <a name="Step2"></a>手順 2: SQL Server コネクタをインストールする  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタのダウンロードとインストールは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンピューターの管理者が行います。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタは、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?LinkId=521700)からダウンロードして入手できます。  " **SQL Server Connector for Microsoft Azure Key Vault**" を検索して、詳細やシステム要件、インストール方法を確認し、コネクタのダウンロードを選択し、 **[実行]** を使用してインストールを開始します。 ライセンスを確認し、ライセンスに同意して続行します。  
  
 既定では、コネクタは **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**にインストールされています。 この場所は、セットアップ中に変更することができます。 (変更した場合は、以下のスクリプトを調整してください。)  
  
 インストールを完了すると、以下のものがコンピューターにインストールされています。  
  
-   **Microsoft.azurekeyvaultservice.ekm.dll**: これは、CREATE cryptographic provider ステートメントを使用してに[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]登録する必要のある暗号化 EKM プロバイダー dll です。  
  
-   **Azure Key Vault SQL Server コネクタ**: これは、暗号化 EKM プロバイダーが Key Vault と通信できるようにする Windows サービスです。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタのインストールでは、必要に応じて、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化で使用するサンプル スクリプトをダウンロードすることもできます。  
  
##  <a name="Step3"></a>手順 3: Key Vault に EKM プロバイダーを使用するように SQL Server を構成する  
  
###  <a name="Permissions"></a>許可  
 このプロセス全体を完了するには、CONTROL SERVER 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。 特定のアクションで必要な権限は次のとおりです。  
  
-   暗号化サービス プロバイダーを作成するには、CONTROL SERVER 権限、または **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
-   構成オプションを変更して RECONFIGURE ステートメントを実行するには、ALTER SETTINGS サーバーレベル権限が与えられている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
-   資格情報を作成するには、ALTER ANY CREDENTIAL 権限が必要です。  
  
-   ログインに資格情報を追加するには、ALTER ANY LOGIN 権限が必要です。  
  
-   非対称キーを作成するには、CREATE ASYMMETRIC KEY 権限が必要です。  
  
###  <a name="TsqlProcedure"></a>暗号化サービスプロバイダーを使用するように SQL Server を構成するには  
  
1.  EKM を使用するように [!INCLUDE[ssDE](../../../includes/ssde-md.md)] を構成し、暗号化サービス プロバイダーを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に登録 (作成) します。  
  
    ```sql
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
  
    -- Create a cryptographic provider, using the SQL Server Connector  
    -- which is an EKM provider for the Azure Key Vault. This example uses   
    -- the name AzureKeyVault_EKM_Prov.  
  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO
    ```  
  
2.  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理者ログインのための [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資格情報をセットアップします。これは、資格情報コンテナーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化のシナリオをセットアップして管理するために使用します。  
  
    > [!IMPORTANT]  
    >  `CREATE CREDENTIAL`の**IDENTITY**引数には、key vault 名が必要です。 `CREATE CREDENTIAL`の**secret**引数では、 * \<クライアント ID>* (ハイフンなし) と* \<シークレット>* をスペースなしで一緒に渡す必要があります。  
  
     次の例では、**クライアント ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) はハイフンを削除し、文字列`EF5C8E094D2A4A769998D93440D8115D`として入力し、**シークレット**は*SECRET_sysadmin_login*文字列で表されます。  
  
    ```sql
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     `CREATE CREDENTIAL`引数に変数を使用し、プログラムでクライアント ID からハイフンを削除する例については、「 [CREATE CREDENTIAL &#40;transact-sql&#41;](/sql/t-sql/statements/create-credential-transact-sql)」を参照してください。  
  
3.  以前に手順 1 のセクション 3 で説明したように非対称キーをインポートした場合は、次の例のようにキー名を提供して、キーを開きます。  
  
    ```sql
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     実稼働環境には推奨されませんが (キーをエクスポートできないため)、資格情報コンテナーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]から直接、非対称キーを作成することもできます。 事前にキーをインポートしなかった場合は、次のスクリプトを使用して、テスト用に資格情報コンテナーに非対称キーを作成します。 スクリプトを実行し、 **sysadmin_ekm_cred** 資格情報を使用してログインのプロビジョニングを行います。  
  
    ```sql
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  エラーを受信したユーザー**は、プロバイダーから公開キーをエクスポートできません。プロバイダーエラーコード: 2053。** では、key vault での**get**、 **list**、 **wrapKey**、および**unwrapKey**のアクセス許可を確認する必要があります。  
  
 詳細については、次のトピックを参照してください。  
  
-   [sp_configure &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [Transact-sql&#41;&#40;暗号化サービスプロバイダーを作成する](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [Transact-sql&#41;&#40;の資格情報の作成](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE 非対称キー &#40;Transact-sql&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [Transact-sql&#41;&#40;ログインの作成](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>例  
  
###  <a name="ExampleA"></a>例 A: Key Vault からの非対称キーを使用して Transparent Data Encryption する  
 上記の手順を完了した後、資格情報とログインを作成し、資格情報コンテナー内の非対称キーで保護されたデータベース暗号化キーを作成します。 データベース暗号化キーは、データベースを TDE で暗号化するために使用します。  
  
 データベースを暗号化するには、データベースに対する CONTROL 権限が必要です。  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>EKM と資格情報コンテナーを使用して TDE を有効にするには  
  
1.  データベースの読み込み中に資格情報コンテナー EKM にアクセスするために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が使用する [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 資格情報を作成します。  
  
    > [!IMPORTANT]  
    >  `CREATE CREDENTIAL`の**IDENTITY**引数には、key vault 名が必要です。 `CREATE CREDENTIAL`の**secret**引数では、 * \<クライアント ID>* (ハイフンなし) と* \<シークレット>* をスペースなしで一緒に渡す必要があります。  
  
     次の例では、**クライアント ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) はハイフンを削除し、文字列`EF5C8E094D2A4A769998D93440D8115D`として入力し、**シークレット**は*SECRET_DBEngine*文字列で表されます。  
  
    ```sql
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が TDE のために使用する [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ログイン名を作成し、それに資格情報を追加します。 この例では、 [手順 3 のセクション 3](#Step3) の説明に従って以前にマスター データベースにインポートまたは作成した、資格情報コンテナーに格納されている CONTOSO_KEY 非対称キーを使用します。  
  
    ```sql
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  TDE に使用するデータベース暗号化キー (DEK) を作成します。 DEK は、SQL Server でサポートされている任意のアルゴリズムまたはキーの長さを使用して作成できます。 DEK は、資格情報コンテナー内の非対称キーによって保護されます。  
  
     この例では、 [手順 3 のセクション 3](#Step3) の説明に従って以前にインポートまたは作成した、資格情報コンテナーに格納されている CONTOSO_KEY 非対称キーを使用します。  
  
    ```sql
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_128   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
     詳細については、次のトピックを参照してください。  
  
    -   [Transact-sql&#41;&#40;データベース暗号化キーを作成する](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a>例 B: Key Vault からの非対称キーを使用してバックアップを暗号化する  
 
  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]以降では、バックアップの暗号化がサポートされています。 次の例では、資格情報コンテナー内の非対称キーで保護したデータ暗号化キーによって暗号化したバックアップを作成し、復元します。  
  
```sql
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 復元のサンプル コードです。  
  
```sql
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 バックアップオプションの詳細については、「 [backup &#40;transact-sql&#41;](/sql/t-sql/statements/backup-transact-sql)」を参照してください。  
  
###  <a name="ExampleC"></a>例 C: Key Vault からの非対称キーを使用した列レベルの暗号化  
 次の例では、資格情報コンテナー内の非対称キーによって保護された対称キーを作成します。 その後、その対称キーを使用してデータベース内のデータを暗号化します。  
  
 この例では、 [手順 3 のセクション 3](#Step3) の説明に従って以前にインポートまたは作成した、資格情報コンテナーに格納されている CONTOSO_KEY 非対称キーを使用します。 この非対称キーを `ContosoDatabase` データベースで使用するには、CREATE ASYMMETRIC KEY ステートメントをもう一度実行して、 `ContosoDatabase` データベースにキーへの参照を提供する必要があります。  
  
```sql
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;暗号化サービスプロバイダーを作成する](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [Transact-sql&#41;&#40;の資格情報の作成](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE 非対称キー &#40;Transact-sql&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-sql&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [拡張キー管理 &#40;EKM&#41;](extensible-key-management-ekm.md)   
 [EKM を使用して TDE を有効にする](enable-tde-on-sql-server-using-ekm.md)   
 [バックアップの暗号化](../../backup-restore/backup-encryption.md)   
 [暗号化されたバックアップの作成](../../backup-restore/create-an-encrypted-backup.md)  
