---
title: Azure Key Vault で SQL Server コネクタ暗号化を使用する
description: Azure Key Vault を使用した TDE、バックアップの暗号化、列レベルの暗号化など、一般的な暗号化機能で SQL Server コネクタを使用する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 09/12/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, using
- EKM, with SQL Server Connector
ms.assetid: 58fc869e-00f1-4d7c-a49b-c0136c9add89
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 0fc954228aff75940e66f976f19d1414118e1a8e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558514"
---
# <a name="use-sql-server-connector-with-sql-encryption-features"></a>SQL 暗号化機能への SQL Server コネクタの使用
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化に関して、Azure Key Vault の保護下にある非対称キーを使用した一般的な作業は、次の 3 つの領域に分けられます。  
  
-   Azure Key Vault からの非対称キーを使用した透過的データ暗号化  
  
-   Key Vault からの非対称キーを使用したバックアップの暗号化  
  
-   Key Vault からの非対称キーを使用した列レベルの暗号化  
  
 このトピックの手順に着手する前に、「 [Azure Key Vault を使用した拡張キー管理のセットアップ手順](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)」のトピックのパート I からパート IV を実行してください。  
 
> [!NOTE]  
>  1\.0.0.440 以前のバージョンは置き換えられ、実稼働環境ではサポートされなくなりました。 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=45344)にアクセスし、[[SQL Server コネクタのメンテナンスとトラブルシューティング]](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) ページの "SQL Server コネクタのアップグレード" に示されている手順を使用して、バージョン 1.0.1.0 以降にアップグレードしてください。  
  
## <a name="transparent-data-encryption-by-using-an-asymmetric-key-from-azure-key-vault"></a>Azure Key Vault からの非対称キーを使用した透過的データ暗号化

「Azure Key Vault を使用した拡張キー管理のセットアップ手順」のトピックのパート I からパート IV を終えたら、Azure Key Vault キーを使用し、データベースの暗号化キーを TDE で暗号化します。 PowerShell を使用したキーのローテーションの詳細については、「[PowerShell を使用して Transparent Data Encryption (TDE) 保護機能をローテーションする](/azure/sql-database/transparent-data-encryption-byok-azure-sql-key-rotation)」を参照してください。
 
資格情報とログインが必要となります。また、データベースに格納されるデータとログを暗号化するためのデータベース暗号化キーを作成する必要があります。 データベースを暗号化するには、データベースに対する **CONTROL** 権限が必要です。 次の図は、Azure Key Vault 使用下における暗号化キーの階層を示したものです。  
  
 ![ekm&#45;key&#45;hierarchy&#45;with&#45;akv](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-with-akv.png "|::ref1::|")  
  
1.  **データベース エンジンが TDE に使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の資格情報を作成する**  
  
     データベース エンジンは、データベースの読み込み時に、この資格情報を使用して Key Vault にアクセスします。 Key Vault に関して付与する権限を制限するために、パート I で、Azure Active Directory の **クライアント ID** と **シークレット** を [!INCLUDE[ssDE](../../../includes/ssde-md.md)]用にもう 1 つ作成することをお勧めします。  
  
     [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを以下のように変更します。  
  
    -   `IDENTITY` 引数 (`ContosoDevKeyVault`) を編集し、Azure Key Vault を参照するようにします。
        - **グローバル Azure** を使用している場合は、`IDENTITY` 引数をパート II で使用した実際の Azure Key Vault の名前に置き換えます。
        - **プライベート Azure クラウド** ( Azure Government、Azure China 21Vianet、Azure Germany など) を使用している場合は、`IDENTITY` 引数をパート II の手順 3 で返された Vault URI に置き換えます。 Vault URI に "https://" は含めないでください。   
  
    -   `SECRET` 引数の最初の部分を、パート I で使用した Azure Active Directory の **クライアント ID** に置き換えます。この例の **クライアント ID** は `EF5C8E094D2A4A769998D93440D8115D`です。  
  
        > [!IMPORTANT]  
        >  **クライアント ID**のハイフンは削除してください。  
  
    -   `SECRET` 引数の 2 番目の部分を、パート I で使用した **クライアント シークレット** に置き換えます。この例のパート 1 で使用した **クライアント シークレット** は `Replace-With-AAD-Client-Secret`です。 完成した `SECRET` 引数は、 *ハイフンを含まない*アルファベットと数字とから成る長い文字列になります。  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for global Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China 21Vianet
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
    ```  
  
2.  **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が TDE に使用する [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ログインを作成する**  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインを作成し、手順 1. で作成した資格情報を追加します。 この例の [!INCLUDE[tsql](../../../includes/tsql-md.md)] では、既にインポートされているキーを使用しています。  
  
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
  
3.  **データベース暗号化キー (DEK) を作成する**  
  
     DEK は、データベース インスタンス内のデータとログ ファイルを暗号化するキーです。このキーがさらに、Azure Key Vault の非対称キーで暗号化されます。 DEK [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でサポートされている任意のアルゴリズムまたはキーの長さを使用して作成できます。  
  
    ```sql  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
    ```  
  
4.  **TDE を有効にする**  
  
    ```sql  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON;  
    GO  
    ```  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]を使用し、オブジェクト エクスプローラーでデータベースに接続して、TDE が有効になっていることを確認します。 データベースを右クリックし、 **[タスク]** をポイントして、 **[データベース暗号化の管理]** をクリックします。  
  
     ![ekm&#45;tde&#45;object&#45;explorer](../../../relational-databases/security/encryption/media/ekm-tde-object-explorer.png "ekm-tde-object-explorer")  
  
     **[データベース暗号化の管理]** ダイアログ ボックスで、TDE が有効になっていることを確認し、DEK の暗号化に使用されている非対称キーを確認します。  
  
     ![ekm&#45;tde&#45;dialog&#45;box](../../../relational-databases/security/encryption/media/ekm-tde-dialog-box.png "ekm-tde-dialog-box")  
  
     代わりに、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを実行してもかまいません。 暗号化の状態が "3" である場合、データベースが暗号化済みであることを示します。  
  
    ```sql  
    USE MASTER  
    SELECT * FROM sys.asymmetric_keys  
  
    -- Check which databases are encrypted using TDE  
    SELECT d.name, dek.encryption_state   
    FROM sys.dm_database_encryption_keys AS dek  
    JOIN sys.databases AS d  
         ON dek.database_id = d.database_id;  
    ```  
  
    > [!NOTE]  
    >  いずれかのデータベースで TDE が有効になっている場合は常に、 `tempdb` データベースが自動的に暗号化されます。  
  
## <a name="encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a>Key Vault からの非対称キーを使用したバックアップの暗号化  
 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]以降では、バックアップの暗号化がサポートされています。 次の例では、資格情報コンテナー内の非対称キーで保護したデータ暗号化キーによって暗号化したバックアップを作成し、復元します。  
この資格情報は、データベースの読み込み時に、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] が Key Vault にアクセスする際に必要となります。 Key Vault に関して付与する権限を制限するために、パート I で、Azure Active Directory のクライアント ID とシークレットをデータベース エンジン用にもう 1 つ作成することをお勧めします。  
  
1.  **データベース エンジンがバックアップの暗号化に使用する SQL Server の資格情報を作成する**  
  
     [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを以下のように変更します。  
  
    -   `IDENTITY` 引数 (`ContosoDevKeyVault`) を編集し、Azure Key Vault を参照するようにします。
        - **グローバル Azure** を使用している場合は、`IDENTITY` 引数をパート II で使用した実際の Azure Key Vault の名前に置き換えます。
        - **プライベート Azure クラウド** ( Azure Government、Azure China 21Vianet、Azure Germany など) を使用している場合は、`IDENTITY` 引数をパート II の手順 3 で返された Vault URI に置き換えます。 Vault URI に "https://" は含めないでください。    
  
    -   `SECRET` 引数の最初の部分を、パート I で使用した Azure Active Directory の **クライアント ID** に置き換えます。この例の **クライアント ID** は `EF5C8E094D2A4A769998D93440D8115D`です。  
  
        > [!IMPORTANT]  
        >  **クライアント ID**のハイフンは削除してください。  
  
    -   `SECRET` 引数の 2 番目の部分を、パート I で使用した **クライアント シークレット** に置き換えます。この例のパート I で使用した **クライアント シークレット** は `Replace-With-AAD-Client-Secret`です。 完成した `SECRET` 引数は、 *ハイフンを含まない*アルファベットと数字とから成る長い文字列になります。   
  
        ```sql  
        USE master;  
  
        CREATE CREDENTIAL Azure_EKM_Backup_cred   
            WITH IDENTITY = 'ContosoDevKeyVault', -- for global Azure
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China 21Vianet
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
            SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;    
        ```  
  
2.  **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がバックアップの暗号化に使用する [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ログインを作成する**  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がバックアップの暗号化に使用する [!INCLUDE[ssDE](../../../includes/ssde-md.md)]ログインを作成し、手順 1. で作成した資格情報を追加します。 この例の [!INCLUDE[tsql](../../../includes/tsql-md.md)] では、既にインポートされているキーを使用しています。  
  
    > [!IMPORTANT]  
    >  TDE (上の例) または列レベルの暗号化 (次の例) で既に使用している非対称キーをバックアップの暗号化に使用することはできません。  
  
     この例では、Key Vault に格納されている `CONTOSO_KEY_BACKUP` 非対称キーを使用します。このキーは、マスター データベースに対してパート IV の手順 5. の説明に従って作成するか、あらかじめインポートしておくことができます。  
  
    ```sql  
    USE master;  
  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it is encrypting the backup.  
    CREATE LOGIN Backup_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY_BACKUP;  
    GO   
  
    -- Alter the Encrypted Backup Login to add the credential for use by   
    -- the Database Engine to access the key vault  
    ALTER LOGIN Backup_Login   
    ADD CREDENTIAL Azure_EKM_Backup_cred ;  
    GO  
    ```  
  
3.  **データベースのバックアップ**  
  
     Key Vault に保存されている非対称鍵で暗号化を指定し、データベースをバックアップします。
     
     下の例では、データベースが既に TDE で暗号化されていて、非対称キー `CONTOSO_KEY_BACKUP` が TDE の非対称キーとは異なる場合、バックアップは TDE 非対称キーと `CONTOSO_KEY_BACKUP` の両方で暗号化されることに注意してください。 バックアップの暗号化を解除するには、両方のキーがターゲットの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスで必要になります。
  
    ```sql  
    USE master;  
  
    BACKUP DATABASE [DATABASE_TO_BACKUP]  
    TO DISK = N'[PATH TO BACKUP FILE]'   
    WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
    ENCRYPTION(ALGORITHM = AES_256,   
    SERVER ASYMMETRIC KEY = [CONTOSO_KEY_BACKUP]);  
    GO  
    ```  
  
4.  **データベースの復元**  
    
    TDE で暗号化されたデータベースのバックアップを復元するには、ターゲットの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスはまず最初に、暗号化に使用された非対称の Key Vault キーのコピーが必要です。 次の方法でこれを実現します。  
    
    - TDE に使用された元の非対称キーが Key Vault にない場合は、Key Vault キーのバックアップを復元するか、またはローカルの HSM からキーを再インポートします。 **重要:** キーの拇印を、データベースのバックアップに記録された拇印と照合させるには、キーの名前が元の名前と**同じ Key Vault キー名**でなければいけません。
    
    - 手順 1 と 2 をターゲットの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに適用します。
    
    - ターゲットの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが、バックアップの暗号化に使用された非対称キーにアクセス可能になったら、サーバー上のデータベースを復元します。
    
     復元のサンプル コードは次のとおりです。  
  
    ```sql  
    RESTORE DATABASE [DATABASE_TO_BACKUP]  
    FROM DISK = N'[PATH TO BACKUP FILE]'   
        WITH FILE = 1, NOUNLOAD, REPLACE;  
    GO  
    ```  
  
     バックアップ オプションの詳細については、「 [BACKUP (Transact-SQL)](../../../t-sql/statements/backup-transact-sql.md)」を参照してください。  
  
## <a name="column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a>Key Vault からの非対称キーを使用した列レベルの暗号化  
 次の例では、資格情報コンテナー内の非対称キーによって保護された対称キーを作成します。 その後、その対称キーを使用してデータベース内のデータを暗号化します。  
  
> [!IMPORTANT]  
>  TDE またはバックアップの暗号化 (前の例) で既に使用している非対称キーをバックアップの暗号化に使用することはできません。  
  
 この例では、「 `CONTOSO_KEY_COLUMNS` Azure Key Vault を使用する拡張キー管理のセットアップ手順 [」の手順 3. (セクション 3) の説明に従って以前にインポートまたは作成した、資格情報コンテナーに格納されている](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)非対称キーを使用します。 この非対称キーを `ContosoDatabase` データベースで使用するには、 `CREATE ASYMMETRIC KEY` ステートメントをもう一度実行して、 `ContosoDatabase` データベースにキーへの参照を提供する必要があります。  
  
```sql  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY_COLUMNS   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoDevRSAKey2',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY  
    (  
    KEY_GUID('DATA_ENCRYPTION_KEY'),   
    CONVERT(VARBINARY,'Plain text data to encrypt')  
    );  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>参照  
 [Azure Key Vault を使用した拡張キー管理のセットアップ手順](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)   
 [Azure Key Vault を使用した拡張キー管理](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [EKM provider enabled サーバー構成オプション](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
