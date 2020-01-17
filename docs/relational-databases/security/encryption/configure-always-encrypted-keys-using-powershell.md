---
title: PowerShell を使用して Always Encrypted キーをプロビジョニングする | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 3bdf8629-738c-489f-959b-2f5afdaf7d61
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2748ffa055927670b840a17590dc4e29436deb30
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594462"
---
# <a name="provision-always-encrypted-keys-using-powershell"></a>PowerShell を使用して Always Encrypted キーをプロビジョニングする
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

    
この記事では、 [SqlServer PowerShell モジュール](../../../relational-databases/scripting/sql-server-powershell-provider.md)を使用し、Always Encrypted のキーを与える手順について説明します。 PowerShell を使用し、Always Encrypted キーを与えることができますが、そのとき、 [役割の分離を指定することも、指定しないこともできます](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#KeyManagementRoles)。キー ストアの実際の暗号鍵にアクセスするユーザーとデータベースにアクセスするユーザーを制御できます。 

推奨されるベスト プラクティスを含む (上位)、Always Encrypted のキー管理の概要については、「[Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」を参照してください。
Always Encrypted に SqlServer PowerShell を使用する方法については、「 [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)」を参照してください。


## <a name="KeyProvisionWithoutRoles"></a> 役割の分離を指定せずにキーを与える

このセクションで説明するキーのプロビジョニング方法では、セキュリティ管理者と DBA の間での役割の分離はサポートされていません。 以下の手順の一部では、物理キーの操作とキー メタデータの操作が組み合わされています。 そのため、この方法によるキーのプロビジョニングは、DevOps モデルを使用している組織の場合、またはデータベースがクラウドでホストされていて、(オンプレミスの DBA ではなく) クラウドの管理者の機密データへのアクセスを制限することが主な目的の場合に、お勧めします。 潜在的な対立関係に DBA が含まれる場合、または DBA に機密データへのアクセスを許可するべきではない場合は、この方法は推奨されません。

プレーンテキストまたはキー ストアへのアクセス (下の表の **[プレーンテキストのキー/キー ストアへのアクセス]** 列で確認) を含む手順を実行する前に、データベースをホストしているコンピューターとは別の安全なコンピューターで PowerShell 環境が実行されていることを確認してください。 詳細については、「 [キー管理でのセキュリティに関する考慮事項](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)」を参照してください。


タスク  |[アーティクル]  |プレーンテキストのキー/キー ストアへのアクセス  |データベースへのアクセス   
---------|---------|---------|---------
手順 1. キー ストアで列マスター キーを作成します。<br><br>**注:** SqlServer PowerShell モジュールでは、この手順はサポートされていません。 コマンドラインからこのタスクを実行するには、選択したキー ストアに固有のツールを使用します。 |[Always Encrypted の列マスター キーを作成して保存する](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | はい | いいえ     
手順 2.  PowerShell 環境を起動し、SqlServer の PowerShell モジュールをインポートします。  |   [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   |    いいえ    | いいえ         
手順 3.  サーバーとデータベースに接続します。     |     [データベースに接続する](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase)    |    いいえ     | はい         
手順 4.  列マスター キーの場所に関する情報を含む *SqlColumnMasterKeySettings* オブジェクトを作成します。 SqlColumnMasterKeySettings は、メモリ (PowerShell) に存在するオブジェクトです。 キー ストアに固有のコマンドレットを使用します。   |     [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)        |   いいえ      | いいえ         
手順 5.  データベースの列マスター キーに関するメタデータを作成します。      |    [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**注:** このコマンドレットは背後で [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを発行し、キー メタデータを作成します。|    いいえ     |    はい
手順 6.  列マスター キーが Azure Key Vault に保存されている場合、Azure に対して認証します。 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |  はい   | いいえ         
手順 7.  新しい列暗号化キーを生成し、それを列マスター キーで暗号化し、データベースで列の暗号化キー メタデータを作成します。     |    [New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**注:** 内部で列の暗号化キーを生成し、暗号化するコマンドレットのバリエーションを使用します。<br><br>**注:** このコマンドレットは背後で [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) ステートメントを発行し、キー メタデータを作成します。  | はい | はい
  

## <a name="windows-certificate-store-without-role-separation-example"></a>Windows 証明書ストアの例 (役割の分離なし)

このスクリプトは、Windows 証明書ストアの証明書である列マスター キーを生成し、列の暗号化キーを生成して暗号化し、SQL Server データベースでキー メタデータを作成する方法を端から端まで例示しています。 


```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings


# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="azure-key-vault-without-role-separation-example"></a>Azure Key Vault 例 (役割の分離なし)

このスクリプトは、Azure Key Vault をプロビジョニングして構成し、Azure Key Vault で列マスター キーを生成し、列の暗号化キーを生成して暗号化し、Azure SQL データベースでキー メタデータを作成する方法を端から端まで例示しています。


```powershell
# Create a column master key in Azure Key Vault.
Import-Module Az
Connect-AzAccount
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"
$azureCtx = Set-AzConteXt -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if your desired group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"

# Connect to your database (Azure SQL database).
Import-Module "SqlServer"
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Authenticate to Azure
Add-SqlAzureAuthenticationContext -Interactive

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="cngksp-without-role-separation-example"></a>CNG/KSP 例 (役割の分離なし)

下のスクリプトは、Cryptography Next Generation API (CNG) を実装するキー ストアで列マスター キーを生成し、列の暗号化キーを生成して暗号化し、SQL Server データベースでキー メタデータを作成する方法を端から端まで例示しています。

この例では、Microsoft ソフトウェア キー記憶域プロバイダーを使用するキー ストアを活用しています。 この例を変更し、ハードウェア セキュリティ モジュールなど、別のストアを使用できます。 そのためには、デバイスに CNG を実装するキー ストア プロバイダー (KSP) がコンピューターに適切にインストールされていることを確認する必要があります。 `Microsoft Software Key Storage Provider` をデバイスの KSP 名に置き換える必要があります。


```powershell
# Create a column master key in a key store that has a CNG provider, a.k.a key store provider (KSP).
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCngColumnMasterKeySettings -CngProviderName $cngProviderName -KeyName $cngKeyName

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="KeyProvisionWithRoles"></a> 役割の分離を指定してキーを与える

このセクションでは、セキュリティ管理者がデータベースにアクセスせず、データベース管理者にキー ストアまたはプレーンテキスト キーへのアクセス許可を与えない暗号化を構成するための手順について説明します。


### <a name="security-administrator"></a>セキュリティ管理者

プレーンテキスト キーまたはキー ストアへのアクセスを含む (下の表の **[プレーンテキストのキー/キー ストアへのアクセス]** 列で確認) 手順を実行する前に、次を確認してください。
1.  データベースをホストしているコンピューターとは別の安全なコンピューターで PowerShell 環境が実行されています。
2.  組織の DBA に、コンピューターにアクセスする許可が与えられていません (アクセスできると、役割の分離の目的が達成されません)。

詳細については、「 [キー管理でのセキュリティに関する考慮事項](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)」を参照してください。


タスク  |[アーティクル]  |プレーンテキストのキー/キー ストアへのアクセス  |データベースへのアクセス  
---------|---------|---------|---------
手順 1. キー ストアで列マスター キーを作成します。<br><br>**注:** SqlServer モジュールでは、この手順はサポートされていません。 コマンドラインからこのタスクを実行するには、キー ストアの種類に固有のツールを使用する必要があります。     | [Always Encrypted の列マスター キーを作成して保存する](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)  |    はい    | いいえ 
手順 2.  PowerShell セッションを起動し、SqlServer のモジュールをインポートします。      |     [SqlServer モジュールのインポート](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule)     | いいえ | いいえ         
手順 3.  列マスター キーの場所に関する情報を含む *SqlColumnMasterKeySettings* オブジェクトを作成します。 *SqlColumnMasterKeySettings* は、メモリ (PowerShell) に存在するオブジェクトです。 キー ストアに固有のコマンドレットを使用します。 |      [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)   | いいえ         | いいえ         
手順 4.  列マスター キーが Azure Key Vault に保存されている場合、Azure に対して認証します。 |    [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |はい|いいえ         
手順 5.  列暗号化キーを生成し、それを列マスター キーで暗号化して列の暗号化キーの値を暗号化します。     |   [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)     |    はい    | いいえ        
手順 6.  列マスター キーの場所 (プロバイダー名と列マスター キーのキー パス) と列暗号化キーの暗号化値を DBA に提供します。  | 後半の例を参照してください。        |   いいえ      | いいえ         

### <a name="dba"></a>DBA 

DBA は、セキュリティ管理者から受け取った (上記の手順 6) 情報を利用し、データベースの Always Encrypted キー メタデータを作成し、管理します。

タスク  |[アーティクル]  |プレーンテキストのキーへのアクセス  |データベースへのアクセス   
---------|---------|---------|---------
手順 1.  列の暗号化キーの場所と列の暗号化キーの暗号化された値をセキュリティ管理者から取得します。 |後半の例を参照してください。 | いいえ | いいえ
手順 2.  PowerShell 環境を起動し、Sql Server のモジュールをインポートします。  | [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)  | いいえ | いいえ
手順 3.  サーバーとデータベースに接続します。 | [データベースに接続する](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | いいえ | はい
手順 4.  列マスター キーの場所に関する情報を含む SqlColumnMasterKeySettings オブジェクトを作成します。 SqlColumnMasterKeySettings は、メモリに存在するオブジェクトです。 | New-SqlColumnMasterKeySettings | いいえ | いいえ
手順 5. データベースの列マスター キーに関するメタデータを作成します。 | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br>**注:** このコマンドレットは背後で [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを発行し、列マスター キー メタデータを作成します。 | いいえ | はい
手順 6. データベースで列の暗号化キー メタデータを作成します。 | New-SqlColumnEncryptionKey<br>**注:** DBA は、列の暗号化キー メタデータのみを作成するコマンドレットのバリエーションを使用します。<br>このコマンドレットは背後で [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) ステートメントを発行し、列の暗号化キー メタデータを作成します。 | いいえ | はい
  
## <a name="windows-certificate-store-with-role-separation-example"></a>Windows 証明書ストアの例 (役割の分離あり)

### <a name="security-administrator"></a>セキュリティ管理者


```powershell
# Create a column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Generate a column encryption key, encrypt it with the column master key to produce an encrypted value of the column encryption key.
$encryptedValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $cmkSettings

# Share the location of the column master key and an encrypted value of the column encryption key with a DBA, via a CSV file on a share drive
$keyDataFile = "Z:\keydata.txt"
"KeyStoreProviderName, KeyPath, EncryptedValue" > $keyDataFile
$cmkSettings.KeyStoreProviderName + ", " + $cmkSettings.KeyPath + ", " + $encryptedValue >> $keyDataFile

# Read the key data back to verify
$keyData = Import-Csv $keyDataFile
$keyData.KeyStoreProviderName
$keyData.KeyPath
$keyData.EncryptedValue 
```

### <a name="dba"></a>DBA

```powershell
# Obtain the location of the column master key and the encrypted value of the column encryption key from your Security Administrator, via a CSV file on a share drive.
$keyDataFile = "Z:\keydata.txt"
$keyData = Import-Csv $keyDataFile

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $keyData.KeyStoreProviderName -KeyPath $keyData.KeyPath

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a  column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName -EncryptedValue $keyData.EncryptedValue
```  
 
## <a name="next-steps"></a>Next Steps    
- [PowerShell での Always Encrypted を使用した列暗号化の構成](configure-column-encryption-using-powershell.md)  
- [PowerShell を使用して Always Encrypted キーをローテーションする](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)

## <a name="see-also"></a>参照    
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)    
- [Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted の列マスター キーを作成して保存する](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
