---
title: フォーマット ファイルを使用したデータ フィールドのスキップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f880dcacbd4571c188d0368a0378a89c45787af2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011723"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>フォーマット ファイルを使用したデータ フィールドのスキップ (SQL Server)
  データ ファイルには、テーブルの列数よりも多くのフィールドを格納できます。 このトピックでは、XML 以外のフォーマット ファイルと XML フォーマット ファイルの両方を変更し、データ ファイルに多くのフィールドを格納する方法について説明します。この操作は、テーブル列を対応するデータ フィールドにマップし、余分なフィールドを無視することによって行います。  
  
> [!NOTE]  
>  XML 以外のフォーマット ファイルまたは XML フォーマット ファイルを使用して、データ ファイルをテーブルに一括インポートできます。この操作は、**bcp** コマンド、BULK INSERT ステートメント、INSERT ... SELECT * FROM OPENROWSET(BULK...) ステートメントのいずれかを使用して実行します。 詳細については、「[データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)」を参照してください。  
  
## <a name="sample-data-file-and-table"></a>サンプル データ ファイルとサンプル テーブル  
 このトピックで例として変更するフォーマット ファイルは、次のテーブルとデータ ファイルに基づいています。  
  
### <a name="sample-table"></a>サンプル テーブル  
 以下の例を実行するには、`myTestSkipField` スキーマに基づいて、`dbo` という名前のテーブルを [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベース内に作成する必要があります。 このテーブルを作成するには、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターで次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipField   
   (  
   PersonID smallint,  
   FirstName nvarchar(50) ,  
   LastName nvarchar(50)   
   );  
GO  
```  
  
### <a name="sample-data-file"></a>サンプル データ ファイル  
 データ ファイル `myTestSkipField-c.dat` には、次のレコードが含まれています。  
  
```  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
```  
  
 `myTestSkipField-c.dat` から `myTestSkipField` テーブルにデータを一括インポートするには、フォーマット ファイルで次の操作を行う必要があります。  
  
-   最初のデータ フィールドを最初の列 `PersonID`にマップします。  
  
-   2 番目のデータ フィールドをスキップします。  
  
-   3 番目のデータ フィールドを 2 番目の列 `FirstName`にマップします。  
  
-   4 番目のデータ フィールドを 3 番目の列 `LastName` にマップします。  
  
## <a name="non-xml-format-file-for-more-data-fields"></a>より多くのデータ フィールドを格納するための XML 以外のフォーマット ファイル  
 次のフォーマット ファイル `myTestSkipField.fmt` は、`myTestSkipField-c.dat` のフィールドを `myTestSkipField` テーブルの列にマップします。 このフォーマット ファイルでは、文字データ形式が使用されます。 列マッピングをスキップするには、フォーマット ファイルの `ExtraField` 列に示すように、その列の順序の値を 0 に変更する必要があります。  
  
 `myTestSkipField.fmt` フォーマット ファイルには、次の情報が含まれています。  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     PersonID               ""  
2       SQLCHAR       0       100       ","    0     ExtraField             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   3     LastName               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  XML 以外のフォーマット ファイルの詳細については、「[XML以外のフォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」を参照してください。  
  
### <a name="examples"></a>使用例  
 次の例では、`INSERT ... SELECT * FROM OPENROWSET(BULK...)` フォーマット ファイルを使用して、`myTestSkipField.fmt` を使用します。 この例では、`myTestSkipField-c.dat` データ ファイルを `myTestSkipField` テーブルに一括インポートします。 サンプルのテーブルとデータ ファイルを作成するには、このトピックの「サンプル データ ファイルとサンプル テーブル」を参照してください。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
   SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.fmt'    
       ) AS t1;  
GO   
```  
  
## <a name="xml-format-file-for-more-data-fields"></a>より多くのデータ フィールドを格納するための XML フォーマット ファイル  
 この例で提供されるフォーマット ファイルは、別のフォーマット ファイルである `myTestSkipField.xml` に基づいています。このフォーマット ファイル全体では、文字データ形式が使用されます。また、フィールドの数と順序は `myTestSkipField` テーブルの列と完全に一致しています。 フォーマット ファイルの内容を確認するには、「[フォーマット ファイルの作成 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)」を参照してください。  
  
 次のフォーマット ファイル `myTestSkipField.xml` は、`myTestSkipField-c.dat` のフィールドを `myTestSkipField` テーブルの列にマップします。 このフォーマット ファイルでは、文字データ形式が使用されます。  
  
 `myTestSkipField.xml` フォーマット ファイルには、次の情報が含まれています。  
  
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
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
### <a name="examples"></a>使用例  
 次の例では、`INSERT ... SELECT * FROM OPENROWSET(BULK...)` フォーマット ファイルを使用して、`myTestSkipField.Xml` を使用します。 この例では、`myTestSkipField-c.dat` データ ファイルを `myTestSkipField` テーブルに一括インポートします。 サンプルのテーブルとデータ ファイルを作成するには、このトピックの「サンプル データ ファイルとサンプル テーブル」を参照してください。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
  SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.xml'    
       ) AS t1;  
GO  
  
```  
  
> [!NOTE]  
>  XML スキーマの構文と XML フォーマット ファイルのその他のサンプルの詳細については、「[XML フォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
