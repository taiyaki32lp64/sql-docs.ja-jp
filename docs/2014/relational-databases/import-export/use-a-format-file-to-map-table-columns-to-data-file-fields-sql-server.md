---
title: フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd08aaa50f307d107a55c838395677e5692914ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011739"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング (SQL Server)
  データ ファイルに含めるフィールドは、対応するテーブル内の列とは異なる順序に並べ替えることができます。 このトピックでは、テーブル列とは異なる順序にフィールドを並べ替えたデータ ファイルを格納できるように変更した XML フォーマット ファイルと XML 以外のフォーマット ファイルについて説明します。 変更したフォーマット ファイルのデータ フィールドは、対応するテーブル列にマッピングされます。  
  
> [!NOTE]  
>  XML 以外のフォーマット ファイルまたは XML フォーマット ファイルを使用して、データ ファイルをテーブルに一括インポートできます。この操作は、**bcp** コマンド、BULK INSERT ステートメント、INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントのいずれかを使用して実行します。 詳細については、「[データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)」を参照してください。  
  
## <a name="sample-table-and-data-file"></a>サンプル テーブルとデータ ファイル  
 このトピックで例として変更するフォーマット ファイルは、次のテーブルとデータ ファイルに基づいています。  
  
### <a name="sample-table"></a>サンプル テーブル  
 このトピックの例を実行するには、`dbo` スキーマに基づいて、`myTestOrder` という名前のテーブルを [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベース内に作成する必要があります。 このテーブルを作成するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestOrder   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) ,  
   Col3 nvarchar(50) ,   
   Col4 nvarchar(50)   
   );  
GO  
  
```  
  
### <a name="data-file"></a>データ ファイル  
 データ ファイル `myTestOrder-c.txt` には、次のレコードが含まれています。  
  
```  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
  
```  
  
 `myTestSkipCol2-c.dat` から `myTestSkipCol` テーブルにデータを一括インポートするには、フォーマット ファイルで 1 番目のデータ フィールドを `Col3`、2 番目のデータ フィールドを `Col2`、3 番目のデータ フィールドを `Col1`、4 番目のデータ フィールドを `Col4` にそれぞれマップする必要があります。  
  
## <a name="using-a-non-xml-format-file"></a>XML 以外のフォーマット ファイルの使用  
 列の順序を表す値を、対応するデータ フィールドの位置を指すように変更することにより、列マッピングの順序を変更できます。  
  
 次の XML 以外のフォーマット ファイルのサンプルは、`myTestOrder.fmt` のフィールドを `myTestOrder-c.txt` テーブルの列にマップするフォーマット ファイル `myTestOrder` を示しています。 データ ファイルとテーブルの作成方法の詳細については、このトピックの「サンプル テーブルとデータ ファイル」を参照してください。 このフォーマット ファイルでは、文字データ形式が使用されます。  
  
 フォーマット ファイルには、次の情報が含まれています。  
  
```  
9.0  
4  
1       SQLCHAR       0       100     ","     3     Col3               SQL_Latin1_General_CP1_CI_AS  
2       SQLCHAR       0       100     ","     2     Col2               SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       7       ","     1     Col1               ""  
4       SQLCHAR       0       100     "\r\n"  4     Col4               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  XML 以外のフォーマット ファイルのレイアウトについての詳細は、「[XML 以外のフォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」を参照してください。  
  
### <a name="example"></a>例  
 次の例では `BULK INSERT` ステートメントを実行し、XML 以外のフォーマット ファイル `myTestOrder-c.txt` を使用して `myTestOrder` データ ファイルから `myTestOrder.fmt` サンプル テーブルにデータを一括インポートします。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターで、次のように実行します。  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestOrder  
FROM 'C:\myTestOrder-c.txt'   
WITH (formatfile='C:\myTestOrder.fmt');  
GO  
  
```  
  
## <a name="using-an-xml-format-file"></a>XML フォーマット ファイルの使用  
 次の XML 以外のフォーマット ファイルのサンプルは、`myTestOrder.xml` のフィールドを `myTestOrder-c.txt` テーブルの列にマップするフォーマット ファイル `myTestOrder` を示しています。データ ファイルとテーブルの作成方法の詳細については、このトピックの「サンプル テーブルとデータ ファイル」を参照してください。  
  
 `myTestOrder.xml` フォーマット ファイルには、次の情報が含まれています。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="3" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="1" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
  
```  
  
> [!NOTE]  
>  XML スキーマの構文と XML フォーマット ファイルのその他のサンプルに関する詳細については、「[XML フォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」を参照してください。  
  
### <a name="example"></a>例  
 次の例では `OPENROWSET` 一括行セット プロバイダーを実行し、XML フォーマット ファイル `myTestOrder-c.txt` を使用して `myTestOrder` データ ファイルから `myTestOrder.xml` サンプル テーブルにデータをインポートします。 `INSERT... SELECT` ステートメントの選択リストには、列リストを指定します。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestOrder   
  SELECT Col1, Col2, Col3, Col4  
      FROM  OPENROWSET(BULK  'C:\myTestOrder-c.txt',  
      FORMATFILE='C:\myTestOrder.Xml'    
       ) AS t1;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  
