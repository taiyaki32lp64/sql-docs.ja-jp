---
title: エンクレーブ対応キーをプロビジョニングする | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6b87620704416df94cf21cda05d1a64a8159eb32
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595587"
---
# <a name="provision-enclave-enabled-keys"></a>エンクレーブ対応キーをプロビジョニングする
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

この記事では、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) に使用されるサーバー側のセキュリティで保護されたエンクレーブ内での計算をサポートするエンクレーブ対応キーをプロビジョニングする方法について説明します。 

[Always Encrypted キーの管理](overview-of-key-management-for-always-encrypted.md)に関する一般的なガイドラインとプロセスが、エンクレーブ対応キーをプロビジョニングするときも適用されます。 この記事では、セキュリティで保護されたエンクレーブが設定された Always Encrypted に固有の詳細について説明します。

SQL Server Management Studio または PowerShell を使用してエンクレーブ対応列マスター キーをプロビジョニングするには、新しいキーでエンクレーブ計算がサポートされていることを確認します。 これにより、ツール (SSMS または PowerShell) によって、データベースで列マスター キーのメタデータに `ENCLAVE_COMPUTATIONS` を設定する `CREATE COLUMN MASTER KEY` ステートメントが生成されます。 詳細については、「[CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)」を参照してください。 

また、ツールでは、列マスター キーを使用して列マスター プロパティがデジタル署名され、データベース メタデータに署名が格納されます。 署名により、`ENCLAVE_COMPUTATIONS` の設定での悪意のある改ざんが防止されます。 SQL クライアント ドライバーは、エンクレーブの使用を許可する前に署名を検証します。 これにより、セキュリティ管理者は、エンクレーブ内でどの列データを計算できるかを制御できます。

`ENCLAVE_COMPUTATIONS` は変更できません。つまり、メタデータで列マスター キーを定義した後に変更することはできません。 特定の列マスター キーによって暗号化が行われる、列暗号化キーを使用したエンクレーブ計算を有効にするには、列マスター キーをローテーションし、エンクレーブ対応の列マスター キーに置き換える必要があります。 「[エンクレーブ対応キーをローテーションする](always-encrypted-enclaves-rotate-keys.md)」をご覧ください。

> [!NOTE]
> 現時点では、SSMS と PowerShell の両方で、Azure Key Vault または Windows 証明書ストアに格納されたエンクレーブ対応の列マスター キーがサポートされています。 (CNG または CAPI を使用した) ハードウェア セキュリティ モジュールはサポートされていません。

エンクレーブ対応の列暗号化キーを作成するには、エンクレーブ対応の列マスター キーを選択して新しいキーを暗号化する必要があります。 

次のセクションでは、SSMS と PowerShell を使用してエンクレーブ対応キーをプロビジョニングする方法の詳細について説明します。

## <a name="provision-enclave-enabled-keys-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してエンクレーブ対応キーをプロビジョニングする
SQL Server Management Studio 18.3 以降では、以下のプロビジョニングができます。
- **[新しい列マスター キー]** ダイアログを使用した、エンクレーブ対応の列マスター キーのプロビジョニング。
- **[新しい列の暗号化キー]** ダイアログを使用した、エンクレーブ対応の列暗号化キーのプロビジョニング。

> [!NOTE]
> 現在、[Always Encrypted ウィザード](always-encrypted-wizard.md)では、エンクレーブ対応キーの生成はサポートされていません。 ただし、最初に上記のダイアログを使用してエンクレーブ対応キーを作成した後、ウィザードを実行するときに、暗号化する列に対して既存のエンクレーブ対応の列暗号化を選択することができます。

### <a name="provision-enclave-enabled-column-master-keys-with-the-new-column-master-key-dialog"></a>[新しい列マスター キー] ダイアログを使用してエンクレーブ対応の列マスター キーをプロビジョニングする
エンクレーブ対応の列マスター キーをプロビジョニングするには、「[[新しい列マスター キー] ダイアログを使用して列マスター キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)」の手順に従います。 必ず、 **[エンクレーブ計算を許可する]** を選択します。 次のスクリーンショットをご覧ください。

![エンクレーブ計算を許可する](./media/always-encrypted-enclaves/allow-enclave-computations.png)

> [!NOTE]
> **[エンクレーブ計算を許可する]** チェック ボックスは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに正しく初期化されたセキュリティで保護されたエンクレーブが含まれている場合にのみ表示されます。 詳しくは、[Always Encrypted のエンクレーブの種類の構成](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)に関する記事をご覧ください。

> [!TIP]
> 列マスター キーがエンクレーブ対応かどうかを確認するには、オブジェクト エクスプローラーでキーを右クリックし、 **[プロパティ]** を選択します。 キーがエンクレーブ対応の場合は、 **[エンクレーブ計算: 許可]** と、キーのプロパティを示すウィンドウに表示されます。 または、[sys.column_master_keys (Transact-SQL)](../../system-catalog-views/sys-column-master-keys-transact-sql.md) ビューを使用することもできます。

### <a name="provision-enclave-enabled-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>[新しい列の暗号化キー] ダイアログを使用してエンクレーブ対応の列暗号化キーをプロビジョニングする
エンクレーブ対応の列暗号化キーをプロビジョニングするには、「[[新しい列の暗号化キー] ダイアログを使用して列の暗号化キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)」の手順に従います。 列マスター キーを選択するときは、エンクレーブ対応であることを確認します。

> [!TIP]
> 列暗号化キーがエンクレーブ対応かどうかを確認するには、オブジェクト エクスプローラーでキーを右クリックし、 **[プロパティ]** を選択します。 キーがエンクレーブ対応の場合は、 **[エンクレーブ計算: 許可]** と、キーのプロパティを示すウィンドウに表示されます。

## <a name="provision-enclave-enabled-keys-using-powershell"></a>PowerShell を使用してエンクレーブ対応キーをプロビジョニングする
PowerShell を使用してエンクレーブ対応キーをプロビジョニングするには、SqlServer PowerShell モジュール バージョン 21.1.18179 以降が必要です。

一般に、「[PowerShell を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-powershell.md)」で説明されている、Always Encrypted に対する PowerShell でのキー プロビジョニング ワークフロー (役割の分離の有無に関係なく) が、エンクレーブ対応キーにも適用されます。 このセクションでは、エンクレーブ対応キーに固有の詳細について説明します。

SqlServer PowerShell モジュールは、[**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) および [**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings) コマンドレットが `-AllowEnclaveComputations` パラメーターで拡張され、プロビジョニング処理中にエンクレーブ対応の列マスター キーを指定できるようになっています。 どちらのコマンドレットでも、(Azure Key Vault または Windows 証明書ストアに格納されている) 列マスター キーのプロパティを含むローカル オブジェクトが作成されます。 `-AllowEnclaveComputations` プロパティを指定すると、キーがローカル オブジェクトでエンクレーブ対応としてマークされます。 また、コマンドレットでは、参照されている列マスター キー (Azure Key Vault または Windows 証明書ストア内) にアクセスして、キーのプロパティへのデジタル署名が行われます。 新しいエンクレーブ対応列マスター キーの設定オブジェクトを作成すると、以降の [**SqlColumnMasterKey**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcolumnmasterkey) コマンドレットの呼び出しでそれを使用して、新しいキーを記述するメタデータ オブジェクトをデータベースに作成できます。

エンクレーブ対応の列暗号化キーのプロビジョニングは、エンクレーブ対応ではない列暗号化キーのプロビジョニングと同じです。 新しい列暗号化キーの暗号化に使用される列マスター キーがエンクレーブ対応であることを確認する必要があるだけです。

> [!NOTE]
> 現在、SqlServer PowerShell モジュールでは、(CNG または CAPI を使用する) ハードウェア セキュリティ モジュールに格納されているエンクレーブ対応キーのプロビジョニングはサポートされていません。

### <a name="example---provision-enclave-enabled-keys-using-windows-certificate-store"></a>例 - Windows 証明書ストアを使用してエンクレーブ対応キーをプロビジョニングする
次のエンドツーエンドの例では、Windows 証明書ストアに格納されている列マスター キーを格納して、エンクレーブ対応キーをプロビジョニングする方法を示します。 スクリプトは、「[Windows 証明書ストアの例 (役割の分離なし)](configure-always-encrypted-keys-using-powershell.md#windows-certificate-store-without-role-separation-example)」の例が基になっています。 重要な点は、[**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) コマンドレットでは `-AllowEnclaveComputations` パラメーターを使用することです。これが、2 つの例のワークフローの唯一の違いです。

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

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

### <a name="example---provision-enclave-enabled-keys-using-azure-key-vault"></a>例 - Azure Key Vault を使用してエンクレーブ対応キーをプロビジョニングする
次のエンドツーエンドの例では、Azure Key Vault に列マスター キーを格納して、エンクレーブ対応キーをプロビジョニングする方法を示します。 スクリプトは、「[Azure Key Vault 例 (役割の分離なし)](configure-always-encrypted-keys-using-powershell.md#azure-key-vault-without-role-separation-example)」の例が基になっています。 エンクレーブ対応のキーとエンクレーブ対応ではないキーのワークフローでの 2 つの違いに注意することが重要です。 
- 次のスクリプトの [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) では、`-AllowEnclaveComputations` パラメーターを使用して、新しい列マスター キーがエンクレーブ対応にされています。 
- 次のスクリプトでは、[**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings) コマンドレットを呼び出す前に、[**Add-SqlAzureAuthenticationContext**](https://docs.microsoft.com/powershell/module/sqlserver/add-sqlazureauthenticationcontext) コマンドレットを呼び出して、Azure にサインインします。 `-AllowEnclaveComputations` パラメーターを指定すると、**New-SqlAzureKeyVaultColumnMasterKeySettings** によって Azure Key Vault が呼び出され、列マスター キーのプロパティへの署名が行われるため、最初に Azure にサインインする必要があります。

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

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure - it is required before calling the next cmdlet.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="next-steps"></a>Next Steps
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを実行する](always-encrypted-enclaves-query-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)
- [既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>参照  
- [チュートリアル: SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](always-encrypted-enclaves-manage-keys.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 