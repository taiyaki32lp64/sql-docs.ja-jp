---
title: データの一括インポートでのフォーマット ファイルの使用
ms.date: 09/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: e81bf59912499310fc95afd29758d5be5f691118
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056365"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>データの一括インポートでのフォーマット ファイルの使用 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

このトピックでは、一括インポート操作でのフォーマット ファイルの使用方法について説明します。  フォーマット ファイルでは、データ ファイルのフィールドがテーブルの列にマップされます。  詳細については、「 [フォーマット ファイルの作成 (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) 」を参照してください。

|[外枠]|
|---|
|[はじめに](#begin)<br />[テスト条件の例](#etc)<br />&emsp;&#9679;&emsp;[サンプル テーブル](#sample_table)<br />&emsp;&#9679;&emsp;[サンプル データ ファイル](#sample_data_file)<br />[フォーマット ファイルの作成](#create_format_file)<br />&emsp;&#9679;&emsp;[XML 以外のフォーマット ファイルの作成](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[XML フォーマット ファイルの作成](#xml_format_file)<br />[フォーマット ファイルを使用してデータを一括インポート](#import_data)<br />&emsp;&#9679;&emsp;[bcp と XML 以外のフォーマット ファイルの使用](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[bcp と XML フォーマット ファイルの使用](#bcp_xml)<br />&emsp;&#9679;&emsp;[BULK INSERT と XML 以外のフォーマット ファイルの使用](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[BULK INSERT と XML フォーマット ファイルの使用](#bulk_xml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) と XML 以外のフォーマット ファイルの使用](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[OPENROWSET(BULK...) と XML フォーマット ファイルの使用](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
## はじめに<a name="begin"></a>
* Unicode 文字データ ファイルを操作するフォーマット ファイルの場合、すべての入力フィールドが Unicode テキスト文字列 (つまり、固定サイズの Unicode 文字列または終端文字が指定された Unicode 文字列) でなければなりません。
* [SQLXML](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md) データを一括エクスポートまたは一括インポートする場合、フォーマット ファイルのデータ型には次のいずれかを使用します。
  * SQLCHAR または SQLVARYCHAR (データは、クライアント コード ページまたは照合順序で暗黙的に指定されるコード ページで送られます)
  * SQLNCHAR または SQLNVARCHAR (データは Unicode として送信されます)
  * SQLBINARY または SQLVARYBIN (データは変換なしで送られます)
* Azure SQL Database と Azure SQL Data Warehouse は、 [bcp](../../tools/bcp-utility.md)のみをサポートします。  その他の詳細については、以下を参照してください。
  * [Azure SQL Data Warehouse にデータを読み込む](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-load/)
  * [SQL Server から Azure SQL Data Warehouse にデータを読み込む (フラット ファイル)](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-from-sql-server-with-bcp/)
  * [データを移行する](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-migrate-data/)

## テスト条件の例<a name="etc"></a>  
このトピックのフォーマット ファイルの例は、以下に定義されたテーブルとデータ ファイルに基づいています。

### **サンプル テーブル**<a name="sample_table"></a>
以下のスクリプトでは、テスト データベースと `myFirstImport`という名前のテーブルが作成されます。  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.MyFirstImport (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   BirthDate Date
   );
```

### **サンプル データ ファイル**<a name="sample_data_file"></a>
メモ帳を使用して、空のファイル `D:\BCP\myFirstImport.bcp` を作成し、次のデータを挿入します。
```
1,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
3,Stella,Rosenhain,1992-03-02
```

また、次の PowerShell スクリプトを実行して、データ ファイルを作成および設定することもできます。
```powershell
Clear-Host
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = Join-Path -Path $dir -ChildPath 'MyFirstImport.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Notepad.exe $bcpfile;
```

## フォーマット ファイルの作成<a name="create_format_file"></a>
SQL Server は、非 XML 形式と XML 形式の 2 種類のフォーマット ファイルをサポートしています。  XML 以外のフォーマットとは、以前のバージョンの SQL Server でサポートされる従来のフォーマットです。

### **XML 以外のフォーマット ファイルの作成**<a name="nonxml_format_file"></a>
詳細については、「 [XML 以外のフォーマット ファイル (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 」を参照してください。  次のコマンドでは、 [bcp ユーティリティ](../../tools/bcp-utility.md) を使用し、 `myFirstImport.fmt`のスキーマに基づいて XML 以外のフォーマット ファイル `myFirstImport`を生成します。  bcp コマンドを使用してフォーマット ファイルを作成するには、 **format** 引数を指定し、データ ファイルのパスの代わりに **nul** を使用します。  format オプションには、次に示す **-f** オプションが必要です。  さらに、この例では、修飾子 **c** を使用して文字データを指定し、 **t** を使用して [フィールド ターミネータ](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)としてコンマを指定し、 **T** を使用して統合セキュリティによる信頼された接続を指定します。  コマンド プロンプトで、次のコマンドを入力します。

```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -f D:\BCP\myFirstImport.fmt -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.fmt
```

非 XML フォーマット ファイルの `D:\BCP\myFirstImport.fmt` は次のようになります。
```
13.0
4
1       SQLCHAR             0       7       ","      1     PersonID               ""
2       SQLCHAR             0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR             0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR             0       11      "\r\n"   4     BirthDate              ""
```

> [!IMPORTANT]
> XML 以外のフォーマット ファイルは、キャリッジ リターン\ライン フィードで終わるようにします。  そうしないと、次のエラー メッセージが発生する可能性があります。
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

### **XML フォーマット ファイルの作成**<a name="xml_format_file"></a>  
詳細については、「 [XML フォーマット ファイル (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) 」を参照してください。  次のコマンドでは、 [bcp ユーティリティ](../../tools/bcp-utility.md) を使用し、 `myFirstImport.xml`のスキーマに基づいて XML のフォーマット ファイル `myFirstImport`を生成します。 bcp コマンドを使用してフォーマット ファイルを作成するには、 **format** 引数を指定し、データ ファイルのパスの代わりに **nul** を使用します。  format オプションには常に **-f** オプションが必要です。XML フォーマット ファイルを作成するには、 **-x** オプションも指定する必要があります。  さらに、この例では、修飾子 **c** を使用して文字データを指定し、 **t** を使用して [フィールド ターミネータ](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)としてコンマを指定し、 **T** を使用して統合セキュリティによる信頼された接続を指定します。  コマンド プロンプトで、次のコマンドを入力します。
```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -x -f D:\BCP\myFirstImport.xml -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.xml
```

XML フォーマット ファイルの `D:\BCP\myFirstImport.xml` は次のようになります。
```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="11"/>
 </RECORD>
 <ROW>
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="4" NAME="BirthDate" xsi:type="SQLDATE"/>
 </ROW>
</BCPFORMAT>
```

## フォーマット ファイルを使用してデータを一括インポート<a name="import_data"></a>
次の例では、データベース、データ ファイル、および上記で作成したフォーマット ファイルを使用します。

### **[bcp](../../tools/bcp-utility.md) と [XML 以外のフォーマット ファイル](../../relational-databases/import-export/non-xml-format-files-sql-server.md)の使用**<a name="bcp_nonxml"></a>
コマンド プロンプトで、次のコマンドを入力します。
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport"
```


### **[bcp](../../tools/bcp-utility.md) と [XML フォーマット ファイル](../../relational-databases/import-export/xml-format-files-sql-server.md)の使用**<a name="bcp_xml"></a>
コマンド プロンプトで、次のコマンドを入力します。
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.xml -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport;"
```


### **[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) と [XML 以外のフォーマット ファイル](../../relational-databases/import-export/non-xml-format-files-sql-server.md)の使用**<a name="bulk_nonxml"></a>
Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) と [XML フォーマット ファイル](../../relational-databases/import-export/xml-format-files-sql-server.md)の使用**<a name="bulk_xml"></a>
Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **[OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) と [XML 以外のフォーマット ファイル](../../relational-databases/import-export/non-xml-format-files-sql-server.md)の使用**<a name="openrowset_nonxml"></a>    
Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **[OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) と [XML フォーマット ファイル](../../relational-databases/import-export/xml-format-files-sql-server.md)の使用**<a name="openrowset_xml"></a>
Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```
  
## <a name="more-examples"></a>その他の例  
 [フォーマット ファイルの作成 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
 [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
 [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
 [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [bcp ユーティリティ](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [XML 以外のフォーマット ファイル &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML フォーマット ファイル &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  [データのインポートまたはエクスポート用のフォーマット ファイル (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
  
