---
title: ネイティブ形式を使用したデータのインポートまたはエクスポート
ms.date: 09/30/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: f6e1eaa9670a5cea38bbf617675d42737b13f796
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055916"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>ネイティブ形式を使用したデータのインポートまたはエクスポート (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
ネイティブ形式は、拡張文字や 2 バイト文字セット (DBCS) の文字を含まないデータ ファイルを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送する場合に推奨します。  

> [!NOTE]
>  拡張文字や DBCS 文字を含んだデータ ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンス間でデータを一括転送するには、Unicode ネイティブ形式を使用する必要があります。 詳細については、「 [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)」をご覧ください。

ネイティブ形式ではデータベースのネイティブ データ型が維持されます。 ネイティブ形式は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル間でデータを高速に転送できるようにデザインされています。 フォーマット ファイルを使用する場合は、転送元と転送先のテーブルは同じである必要はありません。 データ転送は、次の 2 つの手順で行われます。  
  
1.  転送元テーブルからデータ ファイルへのデータの一括エクスポート  
  
2.  データ ファイルから転送先テーブルへのデータの一括インポート  

同一のテーブル間でネイティブ形式を使用すると、文字形式との間でデータ型の不必要な変換を防ぐことができ、時間と領域を節約できます。 ただし、最適な転送速度を実現するために、データの形式設定に関するチェックはほとんど行われません。 読み込まれたデータに関する問題を回避するには、次の制限事項の一覧を参照してください。  

|このトピックの内容|
|---|
|[制限](#restrictions)|
|[bcp によるネイティブ形式でのデータ処理のしくみ](#considerations)|
|[ネイティブ形式用のコマンド オプション](#command_options)|
|[テスト条件の例](#etc)<br /><br />&emsp;&#9679;&emsp;[サンプル テーブル](#sample_table)<br />&emsp;&#9679;&emsp;[XML 形式以外のフォーマット ファイルのサンプル](#nonxml_format_file)|
|[使用例](#examples)<br />&emsp;&#9679;&emsp;[bcp とネイティブ形式を使用したデータのエクスポート](#bcp_native_export)<br />&emsp;&#9679;&emsp;[フォーマット ファイルなしで bcp とネイティブ形式を使用してデータをインポートする方法](#bcp_native_import)<br />&emsp;&#9679;&emsp;[XML 形式以外のフォーマット ファイルで bcp とネイティブ形式を使用してデータをインポートする方法](#bcp_native_import_fmt)<br />&emsp;&#9679;&emsp;[フォーマット ファイルなしで BULK INSERT とネイティブ形式を使用する方法](#bulk_native)<br />&emsp;&#9679;&emsp;[XML 以外のフォーマット ファイルで BULK INSERT とネイティブ形式を使用する方法](#bulk_native_fmt)<br />&emsp;&#9679;&emsp;[XML 形式以外のフォーマット ファイルで OPENROWSET とネイティブ形式を使用する方法](#openrowset_native_fmt)|
|[関連タスク](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|

## 制限<a name="restrictions"></a>  
データをネイティブ形式で正常にインポートするには、次の条件を満たすようにします。  
  
-   データ ファイルがネイティブ形式です。  
  
-   インポート先のテーブルは、(正しい列数、データ型、長さ、NULL 状態などが含まれた) データ ファイルと互換性を持つ必要があります。または、フォーマット ファイルを使用して、各フィールドを対応する各列にマップする必要があります。  
  
    > [!NOTE]
    >  インポート先のテーブルと一致しないファイルからデータをインポートすると、インポート操作が成功する場合もありますが、多くの場合、インポート先のテーブルに挿入されるデータ値が不適切な値になります。 これは、インポート元のファイルのデータが、インポート先のテーブルの形式を使用して解釈されるためです。 そのため、インポート先のテーブルと一致しない場合には、不適切な値が挿入されることになります。 ただし、このような不一致が原因で、データベース内で論理的または物理的に不一致が発生することはありません。  
  
     フォーマット ファイルの使用方法については、「[データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。  
  
 インポートが正常な場合、インポート先のテーブルは破損しません。  
  
## bcp によるネイティブ形式でのデータ処理のしくみ<a name="considerations"></a>
 ここでは、 **bcp** ユーティリティによるネイティブ形式でのデータのエクスポートとインポートのしくみについて、特別な考慮事項を説明します。  
  
-   非文字データ  
  
     [bcp ユーティリティ](../../tools/bcp-utility.md) では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部バイナリ データ形式を使用して、非文字データをテーブルからデータ ファイルに書き込みます。  
  
-   [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) または [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) データ  
  
     [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) または [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) の各フィールドの先頭に、 [bcp](../../tools/bcp-utility.md) ユーティリティによってプレフィックス長が追加されます。  
  
    > [!IMPORTANT]
    >  ネイティブ モードを使用すると、既定では、 [bcp ユーティリティ](../../tools/bcp-utility.md) は、文字をデータ ファイルにコピーする前に、それらの文字を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文字から OEM 文字に変換します。 [bcp ユーティリティ](../../tools/bcp-utility.md) では、データ ファイルの文字を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに一括インポートする前に、それらの文字を ANSI 文字に変換します。 このような変換が行われている間、拡張文字のデータが失われる場合があります。 拡張文字については、Unicode ネイティブ形式を使用するか、コード ページを指定します。
  
-   [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) データ型  
  
     [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) データが SQLVARIANT としてネイティブ形式のデータ ファイルに格納されている場合、そのデータのすべての特性が保持されます。 各データ値のデータ型を記録するメタデータが、そのデータ値と一緒に格納されます。 このメタデータを使用して、インポート先の [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 列に同じデータ型でデータ値を再作成します。  
  
     インポート先の列のデータ型が [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)でない場合、各データ値は、暗黙的なデータ変換の通常の規則に従ってインポート先の列のデータ型に変換されます。 データ変換中にエラーが発生すると、現在のバッチがロールバックされます。 [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) 列間で転送される [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) 値と [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) 値で、コード ページの変換問題が生じている可能性があります。  
  
     詳細については、「[データ型の変換 &#40;データベース エンジン&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)」を参照してください。  
  
## ネイティブ形式用のコマンド オプション<a name="command_options"></a>  
ネイティブ形式のデータは、[bcp](../../tools/bcp-utility.md)、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)、または [INSERT ...SELECT * FROM OPENROWSET(BULK...) を使用してテーブルにインポートできます](../../t-sql/functions/openrowset-transact-sql.md)。[bcp](../../tools/bcp-utility.md) コマンドまたは [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ステートメントの場合は、ステートメントでデータ形式を指定できます。  [INSERT ...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) ステートメントの場合は、フォーマット ファイルでデータ形式を指定する必要があります。  

ネイティブ形式は、次のコマンド オプションでサポートされています。  

|コマンド|オプション|[説明]|  
|-------------|------------|-----------------|  
|bcp|**-n**|bcp ユーティリティで、ネイティブ データ型のデータが使用されます。*|  
|BULK INSERT|DATAFILETYPE **='native'**|ネイティブ データ型またはワイド ネイティブ データ型のデータが使用されます。 フォーマット ファイルでデータ型を指定している場合、DATAFILETYPE は必要ありません。|  
|OPENROWSET|なし|フォーマット ファイルを使用する必要があります|

  
 \* ネイティブ ( **-n**) データを、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントと互換性のある形式のテーブルに読み込むには、 **-V** スイッチを使用します。 詳細については、「 [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)」をご覧ください。  
  
> [!NOTE]
>  また、フォーマット ファイルでフィールドごとに形式を指定することもできます。 詳細については、「 [データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)」を参照してください。
  

## テスト条件の例<a name="etc"></a>  
このトピックの例は、以下に定義されたテーブルとフォーマット ファイルに基づいています。

### **サンプル テーブル**<a name="sample_table"></a>
次のスクリプトは、 `myNative` という名前のテーブルのテスト データベースを作成し、テーブルにいくつかの初期値を設定します。  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNative ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myNative
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myNative;
```

### **XML 形式以外のフォーマット ファイルのサンプル**<a name="nonxml_format_file"></a>
SQL Server は、非 XML 形式と XML 形式の 2 種類のフォーマット ファイルをサポートしています。  XML 以外のフォーマットとは、以前のバージョンの SQL Server でサポートされる従来のフォーマットです。  詳細については、「 [XML 以外のフォーマット ファイル (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) 」を参照してください。  次のコマンドでは、 [bcp ユーティリティ](../../tools/bcp-utility.md) を使用し、 `myNative.fmt`のスキーマに基づいて XML 以外のフォーマット ファイル `myNative`を生成します。  [bcp](../../tools/bcp-utility.md) コマンドを使用してフォーマット ファイルを作成するには、 **format** 引数を指定し、データ ファイルのパスの代わりに **nul** を使用します。  format オプションには、次に示す **-f** オプションが必要です。  さらに、この例では、修飾子 **c** を使用して文字データを指定し、 **T** を使用して統合セキュリティによる信頼関係接続を指定します。  コマンド プロンプトで、次のコマンドを入力します。

```cmd
bcp TestDatabase.dbo.myNative format nul -f D:\BCP\myNative.fmt -T -n 

REM Review file
Notepad D:\BCP\myNative.fmt
```

> [!IMPORTANT]
> XML 以外のフォーマット ファイルは、キャリッジ リターン\ライン フィードで終わるようにします。  そうしないと、次のエラー メッセージが発生する可能性があります。
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## 使用例<a name="examples"></a>
次の例では、上記で作成したデータベースとフォーマット ファイルを使用します。

### **bcp とネイティブ形式を使用したデータのエクスポート**<a name="bcp_native_export"></a>
**-n** スイッチと **OUT** コマンドです。  注: この例で作成するデータ ファイルをその後のすべての例で使用します。  コマンド プロンプトで、次のコマンドを入力します。

```cmd
bcp TestDatabase.dbo.myNative OUT D:\BCP\myNative.bcp -T -n

REM Review results
NOTEPAD D:\BCP\myNative.bcp
```

### **フォーマット ファイルなしで bcp とネイティブ形式を使用してデータをインポートする方法**<a name="bcp_native_import"></a>
**-n** スイッチと **IN** コマンドです。  コマンド プロンプトで、次のコマンドを入力します。

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -T -n

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **XML 形式以外のフォーマット ファイルで bcp とネイティブ形式を使用してデータをインポートする方法**<a name="bcp_native_import_fmt"></a>
**-n** および **-f** スイッチと **IN** コマンドです。  コマンド プロンプトで、次のコマンドを入力します。

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -f D:\BCP\myNative.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **フォーマット ファイルなしで BULK INSERT とネイティブ形式を使用する方法**<a name="bulk_native"></a>
**DATAFILETYPE** 引数です。  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
    FROM 'D:\BCP\myNative.bcp'
    WITH (
        DATAFILETYPE = 'native'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **XML 以外のフォーマット ファイルで BULK INSERT とネイティブ形式を使用する方法**<a name="bulk_native_fmt"></a>
**FORMATFILE** 引数。  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
   FROM 'D:\BCP\myNative.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNative.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **XML 形式以外のフォーマット ファイルで OPENROWSET とネイティブ形式を使用する方法**<a name="openrowset_native_fmt"></a>
**FORMATFILE** 引数。  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) で次の Transact-SQL を実行します。

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative;  -- for testing
INSERT INTO TestDatabase.dbo.myNative
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNative.bcp', 
        FORMATFILE = 'D:\BCP\myNative.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```
  
## 関連タスク<a name="RelatedTasks"></a>
一括インポートまたは一括エクスポートのデータ形式を使用するには 
  
-   [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
