---
title: PowerShell を使用した Always Encrypted の構成 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5c90ea22849dd1d0437cdf058f639bbe546ccab9
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594413"
---
# <a name="configure-always-encrypted-using-powershell"></a>Configure Always Encrypted using PowerShell
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

SqlServer PowerShell モジュールによって、[!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の両方で、[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) を構成するためのコマンドレットが提供されます。

## <a name="security-considerations-when-using-powershell-to-configure-always-encrypted"></a>PowerShell を使用して Always Encrypted を構成するときのセキュリティに関する考慮事項

Always Encrypted の主な目的は、データベース システムが侵害されても、暗号化された機密データが確実に保護されるようにすることにあるので、SQL Server コンピューター上でキーまたは機密データを処理する PowerShell スクリプトが実行されると、機能の効果が低下したり無効になったりするおそれがあります。 セキュリティ関連のその他の推奨事項については、 [Security Considerations for Key Management](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)(キー管理でのセキュリティに関する考慮事項) をご覧ください。

PowerShell を使うと、役割の分離を有効または無効にして、Always Encrypted キーを管理することができ、キー ストアの実際の暗号鍵にアクセスするユーザーと、データベースにアクセスできるユーザーを制御できます。

 追加の推奨事項については、 [Security Considerations for Key Management](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)(キー管理でのセキュリティに関する考慮事項) を参照してください。

## <a name="prerequisites"></a>Prerequisites

SQL Server インスタンスをホストしているコンピューターではない安全なコンピューターに [SqlServer モジュール](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/sqlserver) をインストールします。 モジュールは、PowerShell ギャラリーから直接インストールできます。  詳細については、[ダウンロード](../../../ssms/download-sql-server-ps-module.md)の手順を参照してください。


## <a name="importsqlservermodule"></a> SqlServer モジュールをインポートする 

SqlServer モジュールを読み込むには:

1.  適切なスクリプト実行ポリシーを設定するには、 **Set-ExecutionPolicy** コマンドレットを使用します。
2.  SqlServer モジュールをインポートするには、 **Import-Module** コマンドレットを使用します。

次に示すのは SqlServer モジュールを読み込む例です。

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connectingtodatabase"></a> データベースに接続する

一部の Always Encrypted コマンドレットはデータベースのデータまたはメタデータを操作するので、最初にデータベースに接続する必要があります。 SqlServer モジュールを使用して Always Encrypted を構成するときに推奨されるデータベース接続方法は次の 2 つです。 
1. **Get-SqlDatabase** コマンドレットを使用して接続します。
2. SQL Server PowerShell プロバイダーを使用して接続します。

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="using-get-sqldatabase"></a>Get-SqlDatabase の使用
**Get SqlDatabase** コマンドレットを使うと、SQL Server または Azure SQL Database 内のデータベースに接続できます。 それによって返されるデータベース オブジェクトを、データベースに接続するコマンドレットの **InputObject** パラメーター使って渡すことができます。 

### <a name="using-sql-server-powershell"></a>SQL Server PowerShell の使用

```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database
# Set the valid server name, database name and authentication keywords in the connection string
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$database = Get-SqlDatabase -ConnectionString $connStr

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```

代わりに、パイプを使用することもできます。


```
$database | Get-SqlColumnMasterKey
```

### <a name="using-sql-server-powershell-provider"></a>SQL Server PowerShell プロバイダーの使用
[SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)を使うと、ファイル システム パスと同様のパスで SQL Server オブジェクトの階層が公開されます。 SQL Server PowerShell では、ファイル システムのパスの操作に一般的に使用されているコマンドと同様の Windows PowerShell の別名を使用して、パスを操作できます。 ターゲットのインスタンスおよびデータベースに移動した後、後続のコマンドレットでは次の例で示すようにそのデータベースがターゲットにされます。 

> [!NOTE]
> このデータベース接続方法は、SQL Server に対してのみ動作します (Azure SQL Database ではサポートされていません)。

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
データベースに移動する代わりに、汎用の **Path** パラメーターを使用してデータベース パスを指定することもできます。


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
## <a name="always-encrypted-tasks-using-powershell"></a>PowerShell を使用した Always Encrypted のタスク

- [PowerShell を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-powershell.md)
- [PowerShell を使用した Always Encrypted キーの交換](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [PowerShell を使用して Always Encrypted で列を暗号化、再暗号化、復号化解除する](configure-column-encryption-using-powershell.md)


##  <a name="aecmdletreference"></a> Always Encrypted コマンドレット リファレンス

Always Encrypted では次の PowerShell コマンドレットを使用できます。

|コマンドレット |[説明]
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)**   |Azure への認証を実行し、認証トークンを取得します。
|**[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)**   |データベースの既存の列暗号化キー オブジェクトに新しく暗号化された値を追加します。
|**[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)**   |列マスター キーのローテーションを完了します。
|**[Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)** |データベースで定義されているすべての列暗号化キー オブジェクトを返すか、指定された名前の特定の列暗号化キー オブジェクトを返します。
|**[Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)** |データベースで定義されている列マスター キー オブジェクトを返すか、指定された名前の特定の列マスター キー オブジェクトを返します。
|**[Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)**   |列マスター キーのローテーションを開始します。
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)**   |Azure Key Vault に格納されている非対称キーを記述する SqlColumnMasterKeySettings オブジェクトを作成します。
|**[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)**   |Cryptography Next Generation (CNG) API をサポートするキー ストアに格納されている非対称キーを記述する SqlColumnMasterKeySettings オブジェクトを作成します。
|**[New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)** |データベースに列暗号化キー オブジェクトを作成します。
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)** |列暗号化キーの暗号化された値を生成します。
|**[New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)**   |1 つの列の暗号化に関する情報をカプセル化する SqlColumnEncryptionSettings オブジェクトを作成します。CEK と暗号化の種類を含みます。
|**[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)** |データベースに列マスター キー オブジェクトを作成します。
|**[New-SqlColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|指定されたプロバイダーとキーのパスを使用して、列マスター キーの SqlColumnMasterKeySettings オブジェクトを作成します。
|**[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)**   |Cryptography API (CAPI) をサポートする暗号化サービス プロバイダー (CSP) によってキー ストアに格納されている非対称キーを記述する SqlColumnMasterKeySettings オブジェクトを作成します。
|**[Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)**   |データベースから列暗号化キー オブジェクトを削除します。
|**[Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)** |データベースの既存の列暗号化キー オブジェクトから暗号化された値を削除します。
|**[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)**   |データベースから列マスター キー オブジェクトを削除します。
|**[Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)**   |データベースの指定された列を暗号化、復号化、または再暗号化します。



## <a name="see-also"></a>参照

- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [SQL Server Management Studio を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)