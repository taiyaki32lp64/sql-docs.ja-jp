---
title: フォーマット ファイルを使用したテーブル列のスキップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 80c5c5b2f4e6d4f691b7c3977ae2f715f5424e7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011688"
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>フォーマット ファイルを使用したテーブル列のスキップ (SQL Server)
  このトピックでは、フォーマット ファイルについて説明します。 フォーマット ファイルを使用すると、データ ファイルにフィールドが存在しない場合にテーブル列のインポートをスキップできます。 スキップされる列に NULL 値が許容されているか、既定値があるか、またはその両方の場合のみ、テーブルの列の数より少ないフィールドをデータ ファイルに含めることができます。  
  
## <a name="sample-table-and-data-file"></a>サンプル テーブルとデータ ファイル  
 次の例では、 `myTestSkipCol` サンプル データベースで [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] というテーブルを **dbo** スキーマを使用して作成する必要があります。 このテーブルは次のように作成します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
 次の例では、 `myTestSkipCol2.dat`というサンプル データ ファイルを使用します。対応するテーブルには列が 3 つありますが、このファイルにはフィールドが 2 つしかありません。  
  
```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
  
```  
  
 `myTestSkipCol2.dat` から `myTestSkipCol` テーブルにデータを一括インポートするには、フォーマット ファイルで最初のデータ フィールドを `Col1`にマップし、 `Col3`をスキップして 2 番目のフィールドを `Col2`にマップする必要があります。  
  
## <a name="using-a-non-xml-format-file"></a>XML 以外のフォーマット ファイルの使用  
 XML 以外のフォーマット ファイルを変更して、テーブル列をスキップすることができます。 通常、この作業は、 **bcp** ユーティリティを使用して XML 以外の既定のフォーマット ファイルを作成して、その既定のファイルをテキスト エディターで変更する必要があります。 変更後のフォーマット ファイルでは、既存の各フィールドを対応するテーブル列にマップし、スキップする列を指定する必要があります。 XML 以外の既定のデータ ファイルを変更するには、2 つの方法があります。 どちらの方法も、データ ファイルにデータ フィールドが存在しないこと、および対応するテーブル列にデータが挿入されないことを示します。  
  
### <a name="creating-a-default-non-xml-format-file"></a>XML 以外の既定のフォーマット ファイルの作成  
 ここでは、以下の `myTestSkipCol` bcp **コマンドで** サンプル テーブル用に作成した、XML 以外の既定のフォーマット ファイルを使用します。  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  
  
 上記のコマンドでは、 `myTestSkipCol_Default.fmt`という XML 以外のフォーマット ファイルを作成します。 このフォーマット ファイルは *bcp* で作成した形式なので、 **既定のフォーマット ファイル**といいます。 既定のフォーマット ファイルには通常、データ ファイル フィールドとテーブル列の一対一の対応が記述されます。  
  
> [!IMPORTANT]  
>  場合によっては、接続先サーバー インスタンスの名前を指定する必要があります。 また、ユーザー名とパスワードの指定が必要な場合もあります。 詳細については、「 [bcp Utility](../../tools/bcp-utility.md)」を参照してください。  
  
 次の図に、この既定のフォーマット ファイルのサンプルで使用されている値を示します。 図には、各フォーマット ファイル フィールドの名前も示しています。  
  
 ![myTestSkipCol 用の既定の XML 以外のフォーマット ファイル](../../database-engine/media/mytestskipcol-f-c-default-fmt.gif "myTestSkipCol 用の既定の XML 以外のフォーマット ファイル")  
  
> [!NOTE]  
>  フォーマット ファイル フィールドの詳細については、「[XML 以外のフォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」をご覧ください。  
  
### <a name="methods-for-modifying-a-non-xml-format-file"></a>XML 以外のフォーマット ファイルを変更する方法  
 テーブル列をスキップするには、既定の XML 以外のフォーマット ファイルを編集し、そのファイルを以下のいずれかの方法で変更します。  
  
-   推奨されている方法には、3 つの基本的な手順が含まれています。 まず、データ ファイルに存在しないフィールドを記述しているフォーマット ファイルの行をすべて削除します。 次に、削除したフォーマット ファイルの行に続く各行の "ホスト ファイル フィールドの順序" の値を減らします。 "ホスト ファイル フィールドの順序" の値が、データ ファイル内での各データ フィールドの実際の場所を反映した 1 ～ *n*の通し番号になるようにします。 最後に、データ ファイル内の実際のフィールド数が反映されるように、"列の数" フィールドの値を減らします。  
  
     次の例は、このトピックの「XML 以外の既定のフォーマット ファイルの作成」で既に作成した `myTestSkipCol` テーブルの既定のフォーマット ファイルを基にしています。 変更後のフォーマット ファイルは、最初のデータ フィールドを `Col1`にマップし、 `Col2`をスキップして、2 番目のデータ フィールドを `Col3`にマップしています。 `Col2` に相当する行は削除されています。 他の変更点は太字で示してあります。  
  
    ```  
    9.0  
    2  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
-   スキップするテーブル列に対応するフォーマット ファイルの行の定義を変更することもできます。 変更するフォーマット ファイルの行は、"プレフィックス長"、"ホスト ファイルのデータ長"、および "サーバーの列の順序" の値を 0 に設定する必要があります。 さらに、"ターミネータ" および "列の照合順序" のフィールド値を "" (NULL) に設定する必要があります。  
  
     "サーバーの列名" の値は、実際の列名が不要な場合でも、空でない文字列を指定する必要があります。 残りのフォーマット フィールドは既定値のままにしておく必要があります。  
  
     次の例も、 `myTestSkipCol` テーブルの既定のフォーマット ファイルから作成しました。 0 または NULL にする必要がある値を太字で示してあります。  
  
    ```  
    9.0  
    3  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       00""0     Col2         ""  
    3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
### <a name="examples"></a>使用例  
 以下の例は、このトピックの「サンプル テーブルとデータ ファイル」で既に作成した `myTestSkipCol` サンプル テーブルおよび `myTestSkipCol2.dat` サンプル データ ファイルを基にしています。  
  
#### <a name="using-bulk-insert"></a>BULK INSERT の使用  
 次の例を動作させるには、このトピックの「XML 以外のフォーマット ファイルを変更する方法」で既に作成した、変更後の XML 以外のフォーマット ファイルの 1 つを使用します。 この例では、変更後のフォーマット ファイルの名前を `C:\myTestSkipCol2.fmt`とします。 `BULK INSERT` を使用して `myTestSkipCol2.dat` データ ファイルを一括インポートするには、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] のクエリ エディターで次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="using-an-xml-format-file"></a>XML フォーマット ファイルの使用  
 XML フォーマット ファイルでは、 **bcp** コマンドまたは BULK INSERT ステートメントを使用して直接テーブルにインポートする場合は、列をスキップできません。 ただし、テーブルの最後の列を除くすべての列にインポートできます。 最後の列を除く特定の列をスキップする必要がある場合、データ ファイルに含まれている列のみを含んでいる対象テーブルのビューを作成する必要があります。 その後、データ ファイルからビューにデータを一括インポートできます。  
  
 OPENROWSET(BULK...) を使用してテーブル列をスキップするために XML フォーマット ファイルを使用するには、次のように選択リストおよび対象テーブルの列リストを明示的に指定する必要があります。  
  
 INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)  
  
### <a name="creating-a-default-xml-format-file"></a>既定の XML フォーマット ファイルの作成  
 変換後のフォーマット ファイルの例は、このトピックの「サンプル テーブルとデータ ファイル」で既に作成した `myTestSkipCol` サンプル テーブルおよびデータ ファイルを基にしています。 次の **bcp** コマンドを実行すると、 `myTestSkipCol` テーブルの既定の XML フォーマット ファイルが作成されます。  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
 作成される既定の XML フォーマット ファイルには、次に示すように、データ ファイル フィールドとテーブル列の一対一の対応が記述されます。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  XML フォーマット ファイルの構造については、「[XML フォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」をご覧ください。  
  
### <a name="examples"></a>使用例  
 ここに記載している例は、このトピックの「サンプル テーブルとデータ ファイル」で既に作成した `myTestSkipCol` サンプル テーブルおよび `myTestSkipCol2.dat` サンプル データ ファイルを使用します。 `myTestSkipCol2.dat` から `myTestSkipCol` テーブルにデータをインポートするため、変更した XML フォーマット ファイル `myTestSkipCol2-x.xml`を使用します。 このファイルは、このトピックの「既定の XML フォーマット ファイルの作成」で既に作成したフォーマット ファイルを基にしています。  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
#### <a name="using-openrowsetbulk"></a>OPENROWSET(BULK...) の使用  
 次の例では、 `OPENROWSET` 一括行セット プロバイダーと `myTestSkipCol2.xml` フォーマット ファイルを使用します。 この例では、 `myTestSkipCol2.dat` データ ファイルを `myTestSkipCol` テーブルに一括インポートします。 必要に応じて、ステートメントでは、選択リストおよびターゲット テーブルの列の一覧を明示的に指定します。  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] のクエリ エディターで、次のコードを実行します。  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```  
  
#### <a name="using-bulk-import-on-a-view"></a>ビューに対する BULK IMPORT の使用  
 次の例では、 `v_myTestSkipCol` テーブルに `myTestSkipCol` ビューを作成します。 このビューでは 2 番目のテーブル列である `Col2`がスキップされます。 その後、 `BULK INSERT` を使用して `myTestSkipCol2.dat` データ ファイルをこのビューにインポートします。  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] のクエリ エディターで、次のコードを実行します。  
  
```  
CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
USE AdventureWorks2012;  
GO  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
