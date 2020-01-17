---
title: PowerShell を使用して Always Encrypted キーをローテーションする | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 5117b4fd-c8d3-48d5-87c9-756800769f31
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b5b5246dabbe205554b45cee91be93c4485a60f6
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594122"
---
# <a name="rotate-always-encrypted-keys-using-powershell"></a>PowerShell を使用して Always Encrypted キーをローテーションする
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、SqlServer PowerShell モジュールを使用し、Always Encrypted キーを交換する手順について説明します。 Always Encrypted に SqlServer PowerShell を使用する方法については、「 [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)」を参照してください。

Always Encrypted キーの交換は、既存のキーを新しいキーで置き換えるプロセスです。 キーの回転は、キーが侵害されている場合に、または必須の暗号化キーを定期的に回転することを求めた組織のポリシーまたはコンプライアンス規定に準拠するために、行うことが必要な場合があります。 

Always Encrypted は 2 種類のキーを使用するので、列マスター キーの交換と列暗号化キーの交換という 2 つの高レベルのキー交換ワークフローがあります。

* **列暗号化キーの交換** - 現在のキーで暗号化されたデータの復号化と、新しい列暗号化キーを使用した再暗号化が行われます。 列暗号化キーの交換には、キーとデータベースの両方にアクセスする必要があるので、列暗号化キーの交換は、役割を分離せずに行う必要があります。
* **列マスター キーの交換** では、現在の列マスター キーで保護された列暗号化キーを暗号化解除し、新しい列マスター キーを使用して列暗号化キーを再度暗号化し、両方の種類のキーについてメタデータを更新するという処理が必要です。 列マスター キーの交換は、(SqlServer PowerShell モジュールを使用する場合) 役割の分離の有無にかかわらず実行できます。

## <a name="column-master-key-rotation-without-role-separation"></a>役割の分離を行わない列マスター キーの交換

このセクションで説明されている列マスター キーを交換する方法では、セキュリティ管理者と DBA の間での役割の分離はサポートされていません。 以下の一部の手順では、物理キーの操作とキー メタデータの操作が組み合わされています。そのため、このワークフローは、DevOps を使用する組織、またはデータベースがクラウドでホストされ、主な目的が (オンプレミス DBA ではなく) クラウドの管理者が機密データにアクセスしないように制限することの場合に推奨されます。 潜在的な対立関係に DBA が含まれる場合、または DBA に機密データへのアクセスを許可するべきではない場合は、この方法は推奨されません。  


| タスク | [アーティクル] | プレーンテキストのキー/キーストアへのアクセス| データベースへのアクセス
|:---|:---|:---|:---
|手順 1. キー ストアで新しい列マスター キーを作成します。<br><br>**注:** SqlServer PowerShell モジュールでは、この手順はサポートされていません。 コマンドラインからこのタスクを実行するには、キー ストアに固有のツールを使用する必要があります。 | [Always Encrypted の列マスター キーを作成して保存する](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| はい | いいえ
|手順 2. PowerShell 環境を起動し、SqlServer モジュールをインポートします | [SqlServer モジュールのインポート](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | いいえ | いいえ
|手順 3. サーバーとデータベースに接続します。 | [データベースに接続する](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | いいえ | はい
|手順 4. 新しい列マスター キーの場所に関する情報を含む SqlColumnMasterKeySettings オブジェクトを作成します。 SqlColumnMasterKeySettings は、メモリ (PowerShell) に存在するオブジェクトです。 作成するには、キー ストアに固有のコマンドレットを使用する必要があります。 |[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)<br> | いいえ | いいえ
|手順 5. データベースの新しい列マスター キーに関するメタデータを作成します。 | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**注:** このコマンドレットは背後で [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを発行し、キー メタデータを作成します。 | いいえ | はい
|手順 6. 現在の列マスター キーまたは新しい列マスター キーが Azure Key Vault に格納されている場合は、Azure に対して認証する | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | はい | いいえ
|手順 7. 現在は古い列マスター キーで保護されている各列暗号化キーを、新しい列マスター キーを使用して暗号化することで交換を開始します。 この手順を実行すると、影響を受ける各列暗号化キー (古い列マスター キーと関連付けられ、交換対象であるキー) は、新旧両方の列マスター キーで暗号化され、データベース メタデータに 2 つの暗号化された値があります。| [Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation) | はい | はい
|手順 8. データベース内の暗号化された (そして古い列マスター キーで保護されている) 列をクエリするすべてのアプリケーションの管理者と調整して、アプリケーションから新しい列マスター キーにアクセスできるようにします。| [列マスター キーを作成して保存する (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | はい | いいえ
|手順 9. 交換を完了する<br><br>**注:** この手順を実行する前に、古い列マスター キーで保護されている暗号化された列をクエリするすべてのアプリケーションが、新しい列マスター キーを使用するように構成されていることを確認してください。 この手順を先に実行すると、一部のアプリケーションがデータを復号化できない可能性があります。 古い列マスター キーで作成された、暗号化された値をデータベースから削除して交換を完了します。 この操作で、古い列マスター キーと保護されている列マスター キーの関連付けが削除されます。 |[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)| いいえ | はい
|手順 10. 古い列マスター キーからメタデータを削除します。 |[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| いいえ | はい

> [!NOTE]
> 回転の後、古い列マスター キーは完全に削除しないを強くお勧めします。 そこで、古い列マスター キーを現在のキー ストアに保存するか、セキュリティで保護された別の場所にアーカイブします。 バックアップ ファイルからデータベースを復元して、新しい列マスター キーを構成する *前* の時点まで戻る場合は、古いキーでデータにアクセスする必要があります。

### <a name="rotating-a-column-master-key-without-role-separation-windows-certificate-example"></a>役割の分離なしで列マスター キーを交換する (Windows Certificate の例)

次のスクリプトは、既存の列マスター キー (CMK1) を新しい列マスター キー (CMK2) で置き換えるエンドツーエンドの例です。

```powershell
# Create a new column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Create metadata for your new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings

# Initiate the rotation from the current column master key to the new column master key.
$oldCmkName = "CMK1"
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName -TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```

## <a name="column-master-key-rotation-with-role-separation"></a>役割の分離ありの列マスター キーの交換

このセクションで説明する列マスター キー ワークフローでは、セキュリティ管理者と DBA 間を分離します。

> [!IMPORTANT]
> 以下の表で、 *プレーンテキストのキー/キーストアへのアクセス*=**はい** の手順 (プレーンテキスト キーまたはキー ストアにアクセスする手順) を実行する前に、データベースをホストするコンピューターとは異なるセキュリティで保護されたコンピューターで PowerShell 環境が実行されていることを確認します。 詳細については、「 [キー管理でのセキュリティに関する考慮事項](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)」を参照してください。

### <a name="part-1-dba"></a>パート 1: DBA

DBA は、交換する列マスター キーと、現在の列マスター キーと関連付けられている影響を受ける列暗号化キーに関するメタデータを取得します。 DBA は、セキュリティ管理者とすべての情報を共有します。


| タスク | [アーティクル] | プレーンテキストのキー/キーストアへのアクセス| データベースへのアクセス
|:---|:---|:---|:---
|手順 1. PowerShell 環境を起動し、Sql Server のモジュールをインポートします。 | [SqlServer モジュールのインポート](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | いいえ | なし
|手順 2. サーバーとデータベースに接続します。 | [データベースに接続する](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | いいえ | はい
|手順 3. 古い列マスター キーに関するメタデータを取得します。| [Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey) | いいえ | はい
|手順 4. 古い列マスター キーで保護されている列マスター キーに関するメタデータ (暗号化値など) を取得します。 | [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey) | いいえ | はい
|手順 5. 列マスター キーの場所 (プロバイダー名と列マスター キーのキー パス) と、前の列マスター キーで保護されている対応する列暗号化キーの暗号化値を共有します。| 後半の例を参照してください。 | いいえ | いいえ

### <a name="part-2-security-administrator"></a>パート 2: セキュリティ管理者

セキュリティ管理者は、新しい列マスター キーを生成し、影響を受ける列暗号化キーを新しい列マスター キーで再暗号化し、新しい列マスター キーに関する情報と、影響を受ける列暗号化キーの新しい暗号化値セットを、DBA と共有します。

| タスク | [アーティクル] | プレーンテキストのキー/キーストアへのアクセス| データベースへのアクセス
|:---|:---|:---|:---
|手順 1. 古い列マスター キーの場所と、古い列マスター キーで保護されている対応する列暗号化キーの暗号化値を、DBA から取得します。|なし<br>後半の例を参照してください。|いいえ| いいえ
|手順 2. キー ストアで新しい列マスター キーを作成します。<br><br>**注:** SqlServer モジュールでは、この手順はサポートされていません。 コマンドラインからこのタスクを実行するには、キー ストアの種類に固有のツールを使用する必要があります。|[Always Encrypted の列マスター キーを作成して保存する](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| はい | いいえ
|手順 3. PowerShell 環境を起動し、Sql Server のモジュールをインポートします。 | [SqlServer モジュールのインポート](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | いいえ | いいえ
|手順 4. **古い** 列マスター キーの場所に関する情報を含む SqlColumnMasterKeySettings オブジェクトを作成します。 SqlColumnMasterKeySettings は、メモリ (PowerShell) に存在するオブジェクトです。 |New-SqlColumnMasterKeySettings| いいえ | いいえ
|手順 5. **新しい** 列マスター キーの場所に関する情報を含む SqlColumnMasterKeySettings オブジェクトを作成します。 SqlColumnMasterKeySettings は、メモリ (PowerShell) に存在するオブジェクトです。 作成するには、キー ストアに固有のコマンドレットを使用する必要があります。 | [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)| いいえ | いいえ
|手順 6. 古い (現在の) 列マスター キーまたは新しい列マスター キーが Azure Key Vault に格納されている場合は、Azure に対して認証します。 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | はい | いいえ
|手順 7. 現在は古い列マスター キーで保護されている各列暗号化キー値を、新しい列マスター キーを使用して再暗号化します。 | [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)<br><br>**注:** このコマンドレットを呼び出すときは、SqlColumnMasterKeySettings オブジェクトと、列暗号化キー値を新旧両方の列マスター キーに渡して、再暗号化します。|はい|いいえ
|手順 8. 新しい列マスター キーの場所 (プロバイダー名と列マスター キーのキー パス) と、列暗号化キーの新しい暗号化値セットを DBA と共有します。| 後半の例を参照してください。 | いいえ | いいえ

> [!NOTE]
> 回転の後、古い列マスター キーは完全に削除しないを強くお勧めします。 そこで、古い列マスター キーを現在のキー ストアに保存するか、セキュリティで保護された別の場所にアーカイブします。 バックアップ ファイルからデータベースを復元して、新しい列マスター キーを構成する *前* の時点まで戻る場合は、古いキーでデータにアクセスする必要があります。

### <a name="part-3-dba"></a>パート 3: DBA

DBA は、新しい列マスター キーのメタデータを作成し、影響を受ける列暗号化キーのメタデータを更新して、新しい暗号化値セットを追加します。 この手順で、DBA は、アプリケーションから新しい列マスター キーにアクセスできるようにする、暗号化列をクエリするアプリケーションの管理者とも調整します。 新しいマスター キーを使用するようにすべてのアプリケーションがセットアップされたら、DBA は古い暗号化値セットと古い列マスター キー メタデータを削除します。

| タスク | [アーティクル] | プレーンテキストのキー/キーストアへのアクセス| データベースへのアクセス
|:---|:---|:---|:---
|手順 1. 新しい列マスター キーの場所と、古い列マスター キーで保護されている対応する列暗号化キーの新しい暗号化値セットを、セキュリティ管理者から取得します。| 後半の例を参照してください。 | いいえ | いいえ
|手順 2. PowerShell 環境を起動し、Sql Server のモジュールをインポートします。 | [SqlServer モジュールのインポート](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | いいえ | いいえ
|手順 3. サーバーとデータベースに接続します。 | [データベースに接続する](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | いいえ | はい
|手順 4. 新しい列マスター キーの場所に関する情報を含む SqlColumnMasterKeySettings オブジェクトを作成します。 SqlColumnMasterKeySettings は、メモリ (PowerShell) に存在するオブジェクトです。 |New-SqlColumnMasterKeySettings| いいえ| いいえ
|手順 5. データベースの新しい列マスター キーに関するメタデータを作成します。|[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**注:** このコマンドレットは背後で [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを発行し、キー メタデータを作成します。 | いいえ | はい
|手順 6. 古い列マスター キーで保護されている列マスター キーに関するメタデータを取得します。| [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)| いいえ | はい
|手順 7. 影響を受ける各列暗号化キーについて、新しい暗号化値 (新しい列マスター キーを使用して保護されている値) をメタデータに追加します。|[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)|いいえ|はい
|手順 8. データベース内の暗号化された (そして古い列マスター キーで保護されている) 列をクエリするすべてのアプリケーションの管理者と調整して、アプリケーションから新しい列マスター キーにアクセスできるようにします。|[列マスター キーの作成と保存 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| いいえ|いいえ
|手順 9. 古い列マスター キーと関連付けられた暗号化値をデータベースから削除して交換を完了します。<br><br>**注:** この手順を実行する前に、古い列マスター キーで保護されている暗号化された列のクエリを実行するすべてのアプリケーションが、新しい列マスター キーを使用するように構成されていることを確認してください。 この手順を先に実行すると、一部のアプリケーションがデータを復号化できない可能性があります。<br><br>この手順で、古い列マスター キーと保護されている列マスター キーの関連付けが削除されます。 | [Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)<br><br>また、 [Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)を使用することもできます | いいえ|はい
|手順 10. 古い列マスター キーをデータベースから削除する| [Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| いいえ|はい

### <a name="rotating-a-column-master-key-with-role-separation-windows-certificate-example"></a>役割の分離ありで列マスター キーを交換する (Windows Certificate の例)

次のスクリプトは、Windows 証明書ストアの証明書である新しい列マスター キーを生成し、既存の (現在の) 列マスター キーを交換し、新しい列マスター キーで置き換えるエンドツーエンドの例です。 このスクリプトでは、対象のデータベースに (交換対象の) CMK1 という列マスター キーが含まれている想定です。このキーで、一部の列暗号化キーが暗号化されます。

パート 1: DBA

```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Retrieve the data about the old column master key, which needs to be rotated.
$oldCmkName = "CMK1"
$oldCmk = Get-SqlColumnMasterKey -Name $oldCmkName -InputObject $database


# Share the location of the old column master key with a Security Administrator, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $oldCmkDataFile
$oldCmk.KeyStoreProviderName +", " + $oldCmk.KeyPath >> $oldCmkDataFile


# Find column encryption keys associated with the old column master key and provide the encrypted values of column encryption keys to the Security Administrator, via a CSV file on a share drive.
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
$oldCekValuesFile = "Z:\oldcekvalues.txt"
"CEKName, CEKEncryptedValue" > $oldCekValuesFile 
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {
        # This column encryption has 2 encrypted values - let's check, if it is associated with the old column master key.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {# This column encryption key has 1 encrypted value that was produced using the old column master key
        # Save the name and the encrypted value of the column encryption key in the file.
        $encryptedValue =  "0x" + -join ($ceks[$i].ColumnEncryptionKeyValues[0].EncryptedValue |  foreach {$_.ToString("X2") } )
        $ceks[$i].Name + "," + $encryptedValue >> $oldCekValuesFile
    }
} 
```


パート 2: セキュリティ管理者

```powershell
# Obtain the location of the old column master key and the encrypted values of the corresponding column encryption keys, from your DBA, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
$oldCmkData = Import-Csv $oldCmkDataFile
$oldCekValuesFile = "Z:\oldcekvalues.txt"
$oldCekValues = @(Import-Csv $oldCekValuesFile)

# Create a new column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:\" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your old column master key. 
$oldCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $oldCmkData.KeyStoreProviderName -KeyPath $oldCmkData.KeyPath

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation $storeLocation -Thumbprint $cert.Thumbprint


# Prepare a CSV file, you will use to share the encrypted values of column encryption keys, produced using the new column master key.
$newCekValuesFile = "Z:\newcekvalues.txt"
"CEKName, CEKEncryptedValue" > $newCekValuesFile

# Re-encrypt each value with the new column master key and save the new encrypted value in the file.
for($i=0; $i -lt $oldCekValues.Count; $i++){
    # Re-encrypt each value with the new CMK
    $newValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $newCmkSettings -ColumnMasterKeySettings $oldCmkSettings -EncryptedValue $oldCekValues[$i].CEKEncryptedValue
    $oldCekValues[$i].CEKName + ", " + $newValue >> $newCekValuesFile
}

# Share the new column master key data with your DBA, via a CSV file.
$newCmkDataFile = $home + "\newcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $newCmkDataFile
$newCmkSettings.KeyStoreProviderName +", " + $newCmkSettings.KeyPath >> $newCmkDataFile
```


パート 3: DBA

```powershell
# Obtain the location of the new column master key and the new encrypted values of the corresponding column encryption keys, from your Security Administrator, via a CSV file on a share drive.
$newCmkDataFile = "Z:\newcmkdata.txt"
$newCmkData = Import-Csv $newCmkDataFile
$newCekValuesFile = "Z:\newcekvalues.txt"
$newCekValues = @(Import-Csv $newCekValuesFile)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $newCmkData.KeyStoreProviderName -KeyPath $newCmkData.KeyPath
# Create metadata for the new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings


# Get all CEK objects
$oldCmkName = "CMK1"
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {# This column encryption key has 2 encrypted values. Let's check, if it is associated with the old CMK.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {
        # Find the corresponding new encrypted value, received from the Security Administrator.
        $newValueRow = ($newCekValues| Where-Object {$_.CEKName -eq $ceks[$i].Name }[0])
        # Update the column encryption key metadata object by adding the new encrypted value
        Add-SqlColumnEncryptionKeyValue -ColumnMasterKeyName $newCmkName -Name $ceks[$i].Name -EncryptedValue $newValueRow.CEKEncryptedValue -InputObject $database 
    }
}

# Complete the rotation of the current column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```

## <a name="rotating-a-column-encryption-key"></a>列暗号化キーの交換

列暗号化キーを交換するには、交換するキーで暗号化されたすべての列のデータを暗号化解除し、新しい列暗号化キーを使用してデータを再度暗号化する必要があります。 この交換ワークフローでは、キーとデータベースの両方にアクセスする必要があるので、役割の分離ありでは実行できません。 交換されるキーで暗号化される列が含まれるテーブルが大きい場合、列暗号化キーの交換に長い時間がかかることがあります。 したがって、組織で列暗号化キーを交換する場合は、慎重に計画を立てる必要があります。

オフラインまたはオンラインの手法で、列暗号化キーを回転できます。 前者の方法のほうが速いですが、お使いのアプリケーションでは、影響を受けるテーブルに書き込めません。 後者の手法は時間がかかりますが、時間間隔を設定できます。その間、アプリケーションでは影響を受けるテーブルを利用できません。 詳細については、「[PowerShell で Always Encrypted を使用した列暗号化を構成する](configure-column-encryption-using-powershell.md)」および「[Set-SqlColumnEncryption](/powershell/module/sqlserver/set-sqlcolumnencryption/)」を参照してください。

| タスク | [アーティクル] | プレーンテキストのキー/キーストアへのアクセス| データベースへのアクセス
|:---|:---|:---|:---
|手順 1. PowerShell 環境を起動し、Sql Server のモジュールをインポートします。 | [SqlServer モジュールのインポート](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | いいえ | いいえ
|手順 2. サーバーとデータベースに接続します。 | [データベースに接続する](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | いいえ | はい
|手順 3. (列暗号化キーを保護する、交換される) 列マスター キーが Azure Key Vault に格納されている場合は、Azure に対して認証します。 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | はい | いいえ
|手順 4. 新しい列暗号化キーを生成し、それを列マスター キーで暗号化し、データベースで列の暗号化キー メタデータを作成します。  | [New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**注:** 内部で列の暗号化キーを生成し、暗号化するコマンドレットのバリエーションを使用します。<br>このコマンドレットは背後で [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) ステートメントを発行し、キー メタデータを作成します。 | はい | はい
|手順 5. 古い列暗号化キーで暗号化されたすべての列を検索します。 | [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](../../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) | いいえ | はい
|手順 6. 影響を受ける各列について *SqlColumnEncryptionSettings* オブジェクトを作成します。  SqlColumnMasterKeySettings は、メモリ (PowerShell) に存在するオブジェクトです。 列のターゲット暗号化方式を指定します。 この場合、オブジェクトには、影響を受ける列を新しい列暗号化キーで暗号化することを指定します。 | [New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings) | いいえ | いいえ
|手順 7. 新しい暗号化キーを使用して、手順 5 で指定した列を再暗号化します。 | [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**注:** この手順の実行には時間がかかる場合があります。 アプリケーションでは、選択されたアプローチ (オンラインまたはオフライン) に応じて、操作全体または一部の操作でテーブルにアクセスできなくなります。 | はい | はい
|手順 8. 古い列暗号化キーのメタデータを削除します。 | [Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey) | いいえ | はい

### <a name="example---rotating-a-column-encryption-key"></a>例 - 列暗号化キーの交換

次のスクリプトは、列暗号化キーを交換する例です。  このスクリプトでは、対象データベースに、(交換対象の) CEK1 という列暗号化キーで暗号化されたいくつかの列が含まれていると仮定しています。このキーは、CMK1 という列マスター キーを使用して保護されています (列マスター キーは Azure Key Vault に格納されていません)。 


```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Generate a new column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cmkName = "CMK1"
$newCekName = "CEK2"
New-SqlColumnEncryptionKey -Name $newCekName -InputObject $database -ColumnMasterKey $cmkName 


# Find all columns encrypted with the old column encryption key, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$oldCekName = "CEK1"
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted -and $columns[$j].ColumnEncryptionKeyName -eq $oldCekName) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType $columns[$j].EncryptionType -EncryptionKey $newCekName
        }
     }
}

# Re-encrypt all columns, currently encrypted with the old column encryption key, using the new column encryption key.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -UseOnlineApproach -MaxDowntimeInSeconds 120 -LogFileDirectory .

# Remove the old column encryption key metadata.
Remove-SqlColumnEncryptionKey -Name $oldCekName -InputObject $database
```

## <a name="next-steps"></a>Next Steps
- [SQL Server Management Studio で Always Encrypted を使用した列のクエリを実行する](always-encrypted-query-columns-ssms.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)
  
## <a name="see-also"></a>参照
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md) 
- [PowerShell を使用した Always Encrypted の構成](configure-always-encrypted-using-powershell.md)
- [SQL Server Management Studio を使用して Always Encrypted キーを交換する](rotate-always-encrypted-keys-using-ssms.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)