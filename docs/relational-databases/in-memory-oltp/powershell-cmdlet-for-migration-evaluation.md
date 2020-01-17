---
title: 移行を評価するための PowerShell コマンドレット | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5272203fb1a1c0ac2f755a4da99c654b2595a7f0
ms.sourcegitcommit: 182ed49fa5a463147273b58ab99dc228413975b6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "68698305"
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>移行を評価するための PowerShell コマンドレット

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

`Save-SqlMigrationReport` コマンドレットは、SQL Server データベース内にある複数のオブジェクトの移行適合性を評価するツールです。

現時点では、このコマンドレットはインメモリ OLTP の移行適合性の評価に制限されています。 このコマンドレットは、管理者特権の Windows PowerShell 環境と sqlps の両方で実行できます。

この PowerShell コマンドレットを直接実行する代わりに、SQL Server Management Studio (SSMS) を使用してコマンドレットを暗黙的に実行することもできます。 SSMS **オブジェクトエクスプローラー**でテーブルを右クリックし、 **[メモリ最適化アドバイザー]** をクリックします。

## <a name="syntax"></a>構文

```
Save-SqlMigrationReport
    -FolderPath <output_path>
    [ -MigrationType <migration_scenario_type> ]
    [
        [ -Server <server_name> -Database <database_name>
            [ -Schema <schema_name> ] [ -Object <object_name> ]
        ]
       |
        [ -InputObject <smo_object> ]
    ]
;
```

## <a name="parameters"></a>パラメーター

次の表ではパラメーターについて説明します。

構文には、強調する必要がある側面があります。 パラメーター `-InputObject` を指定する場合は、次のパラメーターのいずれも指定できません。

- `-Server`
- `-Database`
- `-Schema`
- `-Object`

逆に、`-InputObject` を指定 _場合は、`-Server` および `-Database` を指定します。 `-Server` を指定する場合、`-Schema` または `-Object`、またはその両方を指定して範囲を狭めるオプションがあります。

| [パラメーター名] | [説明] |
| :------------- | :---------- |
| データベース | 対象の SQL Server データベースの名前。 `-Server` が必須の場合は必須です。<br/><br/> SQLPS では省略可能です。 |
| FolderPath | コマンドレットで、生成されたレポートを格納するフォルダー。<br/><br/> 必須。 |
| InputObject | コマンドレットが対象とする SMO オブジェクト。<br/><br/> `-Server` が指定されていない場合、Windows Powershell 環境では必須です。<br/><br/> SQLPS では省略可能です。 |
| MigrationType | コマンドレットが対象としている移行シナリオの種類。 現在、既定値の **'OLTP'** のみが既定値になります。<br/><br/> 省略可。 |
| Object | 報告するオブジェクトの名前。 テーブルまたはストアド プロシージャを指定できます。 |
| パスワード | `-Username` が必要な場合は必須。 |
| スキーマ | 報告されるオブジェクトを所有するスキーマの名前。<br/><br/> 省略可。 |
| [サーバー] | 対象の SQL Server インスタンスの名前。 `-InputObject` パラメーターが指定されていない場合、Windows Powershell 環境では必須です。<br/><br/> SQLPS では省略可能です。 |
| Username | Windows 認証ではなく SQL Server 認証を使用して接続する場合に必要です。 それ以外の場合は省略します。 |
| &nbsp; | &nbsp; |

## <a name="prerequisites"></a>Prerequisites

このコマンドレットを実行する前に、まず **SqlServer** という名前のモジュールをインストールする必要があります。

- `Install-Module -Name SqlServer`

> [!NOTE]
> 古い `SQLPS` モジュールは管理されなくなりました。 新しい `SqlServer` モジュールを使用してください。

詳細については、「[SQL Server PowerShell モジュールのダウンロード](../../powershell/download-sql-server-ps-module.md)」を参照してください。

## <a name="example-cmdlet-line"></a>コマンドレットの例

次は、この記事の後半で説明するレポートを生成するために、実行された実際のコマンドレット行を示します。

```powershell
Save-SqlMigrationReport `
  -FolderPath 'C:\Test\PowerShell-ps1\Save-SqlMigrationReport\' `
  -Server 'MyUserName123456.database.windows.net' `
  -Database 'MyDatabaseName_31' `
  -Schema 'dbo' `
  -Object 'Table2' `
  -Username 'MyUserName' `
  -Password 'MyPassword' `
  -MigrationType 'OLTP' `
;
```

## <a name="example-output-report"></a>出力レポートの例

`-FolderPath` パラメーターに指定されたフォルダーの下に、このコマンドレットを実行することにより、次の 2 つのフォルダーのパスが作成されます。 両方のパスは _server\_name_  値で始まります:

- MyDatabaseName_31\Tables\
- MyDatabaseName_31\Stored Procedures\

各オブジェクト レポート ファイルは、適切なフォルダーに格納されます。

レポート ファイル名の拡張子は **.html** です。 たとえば、実際に生成されたファイル名は **MigrationAdvisorChecklistReport_Table2_20190728.html** でした。

HTML は、主に次のヘッダーを持つ 2 列のテーブルです。

- [説明]
- 検証結果

1 つのテーブルの HTML レポートの実際の例を次に示します。

```html
<?xml version="1.0" encoding="utf-8"?>
<html>
  <head>
    <title>Memory optimization checklist for [MyDatabaseName_31].[Table2]</title>
  </head>
  <body>
    <p STYLE="font-family: Verdana, Arial, sans-serif; font-size: 14pt;">
      <b>Memory optimization checklist for [MyDatabaseName_31].[Table2]</b>
    </p>
    <p STYLE="font-family: Verdana, Arial, sans-serif; font-size: 10pt;">
      <b>Report Date/Time:</b>7/28/2019 2:25 PM<br /></p>
    <table border="1" cellpadding="5" cellspacing="0" STYLE="font-family: Verdana, Arial, sans-serif; font-size: 9pt;">
      <tr style="background-color:Silver">
        <th colspan="2" align="center">Description</th>
        <th align="center">Validation Result</th>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported data types are defined on this table. </td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No sparse columns are defined for this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No identity columns with unsupported seed and increment are defined for this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No foreign key relationships are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported constraints are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No unsupported indexes are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported triggers are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">Post migration row size does not exceed the row size limit of memory-optimized tables.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">Table is not partitioned or replicated.</td>
        <td>Succeeded</td>
      </tr>
    </table>
  </body>
</html>
```

また、テーブルがどのような外観かを次に示します。

| [説明] | 検証結果 |
| :---------- | :---------------- |
| このテーブルにはサポートされていないデータ型が定義されていません。 | 成功 |
| このテーブルにはスパース列が定義されていません。 | 成功 |
| このテーブルには、サポートされていないシードと増分を含む ID 列が定義されていません。 | 成功 |
| このテーブルには外部キー リレーションシップが定義されていません。 | 成功 |
| このテーブルにはサポートされていない制約が定義されていません。 | 成功 |
| このテーブルにはサポートされていないインデックスが定義されていません。 | 成功 |
| このテーブルにはサポートされていないトリガーが定義されていません。 | 成功 |
| 移行後の行のサイズは、メモリ最適化テーブルの行サイズの上限を超えていません。 | 成功 |
| テーブルはパーティション分割またはレプリケートされていません。 | 成功 |
| &nbsp; | &nbsp; |

## <a name="related-links"></a>関連リンク

- リファレンス ドキュメント:[Save-SqlMigrationReport](/powershell/module/sqlserver/save-sqlmigrationreport?view=sqlserver-ps)
