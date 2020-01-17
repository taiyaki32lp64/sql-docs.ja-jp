---
title: データの一括インポートでのフォーマット ファイルの使用 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 772dbb86188bf164a2e135f7bb9b71a1cc030745
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011766"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>データの一括インポートでのフォーマット ファイルの使用 (SQL Server)
  このトピックでは、一括インポート操作でのフォーマット ファイルの使用方法について説明します。 フォーマット ファイルでは、データ ファイルのフィールドがテーブルの列にマップされます。  XML 以外のフォーマット ファイルまたは XML フォーマット ファイルを使用して、データを一括インポートできます。この操作には、**bcp** コマンド、または[!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドの BULK INSERT か INSERT ... SELECT * FROM OPENROWSET(BULK...) を使用します。  
  
> [!IMPORTANT]  
>  Unicode 文字データ ファイルを操作するフォーマット ファイルの場合、すべての入力フィールドが Unicode テキスト文字列 (つまり、固定サイズの Unicode 文字列または終端文字が指定された Unicode 文字列) でなければなりません。  
  
> [!NOTE]  
>  フォーマット ファイルに慣れていない場合は、次を参照してください。 [XML 以外のフォーマット ファイル&#40;SQL Server&#41; ](xml-format-files-sql-server.md)と[XML フォーマット ファイル&#40;SQL Server&#41;](xml-format-files-sql-server.md)します。  
  
## <a name="format-file-options-for-bulk-import-commands"></a>一括インポート コマンドのフォーマット ファイル オプション  
 次の表は、各一括インポート コマンドのフォーマット ファイル オプションを示しています。  
  
|一括読み込みコマンド|フォーマット ファイル オプションの使用方法|  
|------------------------|-----------------------------------|  
|BULK INSERT|FORMATFILE = '*format_file_path*'|  
|INSERT ...SELECT * FROM OPENROWSET(BULK...)|FORMATFILE = '*format_file_path*'|  
|**bcp** .**で**|**-f** *format_file*|  
  
 詳細については、「[bcp ユーティリティ](../../tools/bcp-utility.md)」、「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」、または「[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  SQLXML データを一括エクスポートまたは一括インポートするには、フォーマット ファイルで次のいずれかのデータ型を使用します。SQLCHAR または SQLVARYCHAR (データはクライアント コード ページまたは照合順序で暗黙的に指定されるコード ページで送られます)、SQLNCHAR または SQLNVARCHAR (データは Unicode として送られます)、SQLBINARY または SQLVARYBIN (データは変換なしで送られます)。  
  
## <a name="examples"></a>使用例  
 このセクションの例では、**bcp** コマンド、BULK INSERT ステートメント、および INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントを使用してデータを一括インポートする場合のフォーマット ファイルの使用方法を示します。 一括インポートの例を実行する前に、サンプル テーブル、データ ファイル、およびフォーマット ファイルを作成する必要があります。  
  
### <a name="sample-table"></a>サンプル テーブル  
 次の例では、 **dbo** スキーマ内の [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] myTestFormatFiles **という名前のテーブルを** サンプル データベースに作成する必要があります。 このテーブルを作成するには、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestFormatFiles (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50),  
   Col4 nvarchar(50)  
   );  
GO  
```  
  
### <a name="sample-data-file"></a>サンプル データ ファイル  
 この例では、次のレコードが含まれているサンプル データ ファイル `myTestFormatFiles-c.Dat`を使用します。 このデータ ファイルを作成するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のコマンド プロンプトで次のように入力します。  
  
```  
10,Field2,Field3,Field4  
15,Field2,Field3,Field4  
46,Field2,Field3,Field4  
58,Field2,Field3,Field4  
```  
  
### <a name="sample-format-files"></a>サンプル フォーマット ファイル  
 このセクションの例では、XML フォーマット ファイル `myTestFormatFiles-f-x-c.Xml` を使用する場合と、XML 形式以外のフォーマット ファイルを使用する場合があります。 どちらのフォーマット ファイルでも、文字データの形式と既定外のフィールド ターミネータ (,) を使用します。  
  
#### <a name="the-sample-non-xml-format-file"></a>XML 形式以外のフォーマット ファイルのサンプル  
 次の例では、 **bcp** を使用して、 `myTestFormatFiles` テーブルから XML フォーマット ファイルを生成します。 `myTestFormatFiles.Fmt` ファイルには、次の情報が格納されます。  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     ","      2     Col2         SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      3     Col3         SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   4     Col4         SQL_Latin1_General_CP1_CI_AS  
```  
  
 **format** オプションと共に **bcp** を使用して、このフォーマット ファイルを作成するには、Windows のコマンド プロンプトで次のように入力します。  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -f myTestFormatFiles.Fmt -T  
  
```  
  
 フォーマット ファイルの作成方法の詳細については、「[フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)」を参照してください。  
  
#### <a name="the-sample-xml-format-file"></a>XML 形式のフォーマット ファイルのサンプル  
 次の例では、 **bcp** を使用して、 `myTestFormatFiles` テーブルから XML フォーマット ファイルを生成します。 `myTestFormatFiles.Xml` ファイルには、次の情報が格納されます。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 **format** オプションと共に **bcp** を使用して、このフォーマット ファイルを作成するには、Windows のコマンド プロンプトで次のように入力します。  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -x -f myTestFormatFiles.Xml -T  
```  
  
### <a name="using-bcp"></a>bcp の使用  
 次の例では、 **bcp** を使用して、 `myTestFormatFiles-c.Dat` データ ファイルのデータをサンプル データベース内の `HumanResources.myTestFormatFiles` テーブルに一括インポートします。 この例では、XML 形式のフォーマット ファイル `MyTestFormatFiles.Xml`を使用します。 既存のテーブル行は、データ ファイルのインポート前に削除されます。  
  
 Windows のコマンド プロンプトで、次のように入力します。  
  
```  
bcp AdventureWorks2012..myTestFormatFiles in C:\myTestFormatFiles-c.Dat -f C:\myTestFormatFiles.Xml -T  
```  
  
> [!NOTE]  
>  このコマンドの詳細については、「[bcp ユーティリティ](../../tools/bcp-utility.md)」を参照してください。  
  
### <a name="using-bulk-insert"></a>BULK INSERT の使用  
 次の例では、BULK INSERT を使用して、`myTestFormatFiles-c.Dat` データ ファイルから [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] サンプル データベース内の `HumanResources.myTestFormatFiles` テーブルにデータを一括インポートします。 この例では、XML 形式以外のフォーマット ファイル `MyTestFormatFiles.Fmt` を使用します。 既存のテーブル行は、データ ファイルのインポート前に削除されます。  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
DELETE myTestFormatFiles;  
GO  
BULK INSERT myTestFormatFiles   
   FROM 'C:\myTestFormatFiles-c.Dat'   
   WITH (FORMATFILE = 'C:\myTestFormatFiles.Fmt');  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
> [!NOTE]  
>  この句の詳細については、「[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)」を参照してください。  
  
### <a name="using-the-openrowset-bulk-rowset-provider"></a>OPENROWSET 一括行セット プロバイダーの使用  
 次の例では、 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` を使用して、 `myTestFormatFiles-c.Dat` データ ファイルのデータを `HumanResources.myTestFormatFiles` サンプル データベース内の `AdventureWorks` テーブルに一括インポートします。 この例では、XML 形式のフォーマット ファイル `MyTestFormatFiles.Xml`を使用します。 既存のテーブル行は、データ ファイルのインポート前に削除されます。  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
DELETE myTestFormatFiles;  
GO  
INSERT INTO myTestFormatFiles  
    SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestFormatFiles-c.Dat',  
      FORMATFILE='C:\myTestFormatFiles.Xml'       
      ) as t1 ;  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
 サンプル テーブルを使用し終わったら、次のステートメントを使用してテーブルを削除できます。  
  
```  
DROP TABLE myTestFormatFiles  
```  
  
> [!NOTE]  
>  OPENROWSET BULK 句の詳細については、「 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)を使用) を示すことができます。  
  
## <a name="additional-examples"></a>その他の例  
 [フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
 [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
 [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [XML 以外のフォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [XML フォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)  
  
  
