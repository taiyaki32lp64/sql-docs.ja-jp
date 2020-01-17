---
title: PowerShell での Always Encrypted を使用した列暗号化の構成 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 074c012b-cf14-4230-bf0d-55e23d24f9c8
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cc6f86a091f96f3d38bc4db7a5d5d2fde5462dce
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594384"
---
# <a name="configure-column-encryption-using-always-encrypted-with-powershell"></a>PowerShell での Always Encrypted を使用した列暗号化の構成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、( [SqlServer](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption) PowerShell モジュールで) *Set-SqlColumnEncryption* コマンドレットを使用して、データベース列にターゲット Always Encrypted 構成を設定する手順を説明します。 **Set-SqlColumnEncryption** コマンドレットは、ターゲット データベースと選択した列に格納されたデータの両方のスキーマを変更します。 列に格納されたデータは、その列に指定されたターゲットの暗号化設定と現在の暗号化の構成に応じて、暗号化、再暗号化、または復号化できます。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] を使用していて、お使いの SQL Server インスタンスがセキュリティで保護されたエンクレーブで構成されている場合は、データベースからデータを移動せずに、暗号化操作をインプレースで実行できます。 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」を参照してください。 PowerShell では、インプレース暗号化がサポートされていないことに注意してください。

::: moniker-end
SqlServer PowerShell モジュールでの Always Encrypted のサポートの詳細については、「[PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)」を参照してください。

## <a name="prerequisites"></a>Prerequisites

ターゲットの暗号化構成を設定するには、次のことを確認する必要があります。
- 列暗号化キーがデータベースで構成されていること (列を暗号化または再暗号化する場合)。 詳しくは、「[PowerShell を使用して Always Encrypted キーを構成する](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)」を参照してください。
- PowerShell コマンドレットを実行しているコンピューターから、暗号化、再暗号化、また復号化する各列の列マスター キーにアクセスできること。 

## <a name="performance-and-availability-considerations"></a>パフォーマンスと可用性に関する考慮事項

データベースに指定されたターゲットの暗号化設定を適用するには、 **Set-SqlColumnEncryption** コマンドレットを使用して、ターゲット テーブルを含む列からデータをすべて透過的にダウンロードし、一時テーブル セットにデータをアップロードして戻し (ターゲットの暗号化された設定を使用)、最終的には元のテーブルを新しいバージョンのテーブルに置き換えます。 基になる .NET Framework Data Provider for SQL Server は、ターゲット列の現在の暗号化構成とターゲット列に指定されたターゲットの暗号化設定に応じて、ダウンロードまたはアップロード時にデータを暗号化または暗号化解除します。 影響を受けるテーブル内のデータのサイズとネットワーク帯域幅に応じて、データの移動操作に時間がかかる場合があります。

**Set-SqlColumnEncryption** コマンドレットでは、ターゲット暗号化構成をセットアップする際にオンラインとオフラインの 2 つのアプローチがサポートされます。

オフライン アプローチの場合、ターゲット テーブル (およびターゲット テーブルに関連するすべてのテーブル。たとえば、ターゲット テーブルと外部キー リレーションシップがあるテーブルなど) は、操作中にトランザクションを書き込むことはできません。 外部キー制約のセマンティクス (**CHECK** または **NOCHECK**) は、オフライン アプローチの場合は常に保持されます。

オンライン アプローチ (SqlServer PowerShell モジュール バージョン 21.x 以降が必要) では、データのコピーと暗号化、暗号化の解除、再暗号化の操作がインクリメンタルに実行されます。 アプリケーションでは、データの移動操作中にターゲット テーブルに対してデータの読み取りと書き込みを実行できます。ただし、最後の繰り返しを除きます。期間は **MaxDownTimeInSeconds** パラメーターで制限されます (ユーザーが定義可能)。 データのコピー中にアプリケーションで実行できる変更を検出して処理するため、コマンドレットによってターゲット データベースでの [Change Tracking](../../track-changes/enable-and-disable-change-tracking-sql-server.md) が有効にされます。 そのため、オフライン アプローチの場合よりサーバー側で使用するリソース量が多くなる可能性があります。 また、オンライン アプローチの場合、操作にかなり時間がかかることがあります。特に、データベースに対して負荷の高い書き込みが実行される場合です。 オンライン アプローチを使用できるのは一度に 1 つのテーブルを暗号化する場合です。テーブルには主キーになります。 既定では、外部キー制約は **NOCHECK** オプションで再作成され、アプリケーションへの影響を最小限に抑えます。 **KeepCheckForeignKeyConstraints** オプションを指定して、外部キー制約のセマンティックを強制的に保持できます。 

ここでは、オフラインとオンラインのいずれかのアプローチを選択する場合のガイドラインを示します。

次のような場合はオフライン アプローチを使用します。
- 操作期間を最小限に抑える。 
- 複数のテーブルの列を同時に暗号化/暗号化解除/再暗号化する。
- ターゲット テーブルに主キーがない。

次のような場合はオンライン アプローチを使用します。
- アプリケーションに対するデータベースのダウンタイム/使用不可の状態を最小限にする。

## <a name="security-considerations"></a>セキュリティに関する考慮事項

データベース列の暗号化を構成するために使用される **Set-SqlColumnEncryption** コマンドレットは、Always Encrypted キーとデータベース列に格納されているデータの両方を処理します。 したがって、セキュリティで保護されたコンピューターでコマンドレットを実行することが重要です。 データベースが SQL Server にある場合は、SQL Server インスタンスをホストするコンピューターとは異なるコンピューターからコマンドレットを実行します。 Always Encrypted の主な目的は、データベース システムが侵害されても、暗号化された機密データが確実に保護されるようにすることにあるので、SQL Server コンピューター上でキーや機密データを処理する PowerShell スクリプトが実行されると、機能の効果が低下したり無効になったりするおそれがあります。

タスク  |[アーティクル]  |プレーンテキストのキー/キー ストアへのアクセス  |データベースへのアクセス   
---|---|---|---
手順 1. PowerShell 環境を起動し、Sql Server のモジュールをインポートします。 | [SqlServer モジュールのインポート](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | いいえ | いいえ
手順 2. サーバーとデータベースに接続します。 | [データベースに接続する](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | いいえ | はい
手順 3. (列暗号化キーを保護する、交換される) 列マスター キーが Azure Key Vault に格納されている場合は、Azure に対して認証します。 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | はい | いいえ
手順 4. 暗号化、再暗号化または復号化するデータベースの各列に 1 つずつ SqlColumnEncryptionSettings オブジェクトの配列を構築します。 SqlColumnMasterKeySettings は、メモリ (PowerShell) に存在するオブジェクトです。 列のターゲット暗号化方式を指定します。 | [New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings) | いいえ | いいえ
手順 5. 前の手順で作成した SqlColumnMasterKeySettings オブジェクトの配列で指定された、目的の暗号化構成を設定します。 指定したターゲットの設定と列の現在の暗号化の構成に応じて、列が暗号化、再暗号化、または復号化されます。| [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**注:** この手順の実行には時間がかかる場合があります。 アプリケーションでは、選択されたアプローチ (オンラインまたはオフライン) に応じて、操作全体または一部の操作でテーブルにアクセスできなくなります。 | はい | はい

## <a name="encrypt-columns-using-offline-approach---example"></a>オフライン アプローチを使用した列の暗号化 - 例

次の例では、いくつかの列にターゲット暗号化構成を設定しているところを示しています。 まだ暗号化されていない列があれば、暗号化されます。 別のキーや異なる暗号化の種類を使用して既に暗号化されている列がある場合は、復号化した後に、指定したターゲット キー/種類で再暗号化されます。


```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -LogFileDirectory .
```
 
## <a name="encrypt-columns-using-online-approach---example"></a>オンライン アプローチを使用した列の暗号化 - 例

次の例では、オンライン アプローチを使用して、いくつかの列にターゲット暗号化構成を設定します。 まだ暗号化されていない列があれば、暗号化されます。 別のキーや異なる暗号化の種類を使用して既に暗号化されている列がある場合は、復号化した後に、指定したターゲット キー/種類で再暗号化されます。

```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -UseOnlineApproach -MaxDowntimeInSeconds 180 -LogFileDirectory .
```
## <a name="decrypt-columns---example"></a>列の復号化 - 例

次の例では、データベースで現在暗号化されているすべての列を復号化する方法を示しています。


```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Find all encrypted columns, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType "Plaintext" 
        }
    }
}

# Decrypt all columns.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -LogFileDirectory .
```
 
## <a name="next-steps"></a>Next Steps
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)

## <a name="see-also"></a>参照  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md) 
 - [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
 - [Always Encrypted ウィザードを使用して列暗号化を構成する](always-encrypted-wizard.md)
 - [DAC パッケージでの Always Encrypted を使用した列暗号化の構成](configure-always-encrypted-using-dacpac.md)


