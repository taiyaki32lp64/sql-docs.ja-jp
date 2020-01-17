---
title: XML ドキュメントの一括インポートと一括エクスポート
ms.description: Examples of bulk importing and exporting of XML documents with SQL Server
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- field terminators [SQL Server]
- bulk importing [SQL Server], data formats
- row terminators [SQL Server]
- OPENROWSET function, XML bulk load
- terminators [SQL Server]
- bulk exporting [SQL Server], data formats
- XML bulk load [SQL Server]
ms.assetid: dff99404-a002-48ee-910e-f37f013d946d
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 9a665f51aa6fd6bc9b87ac354a26856049004d7e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401585"
---
# <a name="examples-of-bulk-import-and-export-of-xml-documents-sql-server"></a>XML ドキュメントの一括インポートと一括エクスポートの例 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

    
##  <a name="top"></a>
 XML ドキュメントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに一括インポートすることも、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースから一括エクスポートすることもできます。 このトピックではその両方の例を示します。  
  
 データ ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルまたはパーティション分割されていないビューにデータを一括インポートする場合、次の機能を使用できます。  
  
-   **bcp** ユーティリティ  
    **bcp** ユーティリティは、パーティション分割されたビューを含めて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースで SELECT ステートメントが機能する任意の場所からデータをエクスポートするためにも使用できます。  
  
-   BULK INSERT  
  
-   INSERT ...SELECT * FROM OPENROWSET(BULK...)  

詳細については、次の各トピックを参照してください。
- [bcp ユーティリティを使用した一括データのインポートとエクスポート (SQL Server)](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
- [BULK INSERT または OPENROWSET(BULK...) を使用した一括データのインポート (SQL Server)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) 
- [XML 一括ロード コンポーネントを使用して XML を SQL Server にインポートする方法](https://support.microsoft.com/kb/316005)
- [XML スキーマ コレクション (SQL Server)](../xml/xml-schema-collections-sql-server.md)
  
## <a name="examples"></a>例  
 次に例を示します。  
  
-  [A.バイナリ バイト ストリームとして XML データの一括インポートを行う](#binary_byte_stream)  
  
-  [B.既存の行に XML データの一括インポートを行う](#existing_row)  
  
-  [C.DTD を含むファイルから XML データの一括インポートを行う](#file_contains_dtd)  
  
- [D.フォーマット ファイルを使用してフィールド ターミネータを明示的に指定する](#field_terminator_in_format_file)  
  
-  [E.XML データの一括エクスポートを行う](#bulk_export_xml_data)  
  
## <a name="binary_byte_stream"></a>バイナリ バイト ストリームとして XML の一括インポートを行う  
 適用するエンコード宣言が含まれているファイルから XML データの一括インポートを行うときは、OPENROWSET(BULK...) 句で SINGLE_BLOB オプションを指定します。 SINGLE_BLOB オプションが指定されていると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の XML パーサーは必ず XML 宣言で指定されたエンコード体系に従ってデータをインポートします。  
  
#### <a name="sample-table"></a>サンプル テーブル  
 例 A をテストするには、サンプル テーブル `T`を作成します。  
  
```sql
USE tempdb  
CREATE TABLE T (IntCol int, XmlCol xml);  
GO  
```  
  
#### <a name="sample-data-file"></a>サンプル データ ファイル  
 例 A を実行する前に、次のサンプル インスタンスが指定する`C:\SampleFolder\SampleData3.txt`エンコード体系を含む、UTF-8 エンコードのファイル ( `UTF-8` ) を作成する必要があります。  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>  
<Root>  
          <ProductDescription ProductModelID="5">  
             <Summary>Some Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-a"></a>例 A  
 この例では、 `SINGLE_BLOB` オプションを `INSERT ... SELECT * FROM OPENROWSET(BULK...)` ステートメントで使用して、 `SampleData3.txt` という名前のファイルからデータをインポートし、XML インスタンスを 1 列のテーブル (サンプル テーブル `T`) に挿入します。  
  
```sql
INSERT INTO T(XmlCol)  
SELECT * FROM OPENROWSET(  
   BULK 'c:\SampleFolder\SampleData3.txt',  
   SINGLE_BLOB) AS x;  
```  
  
#### <a name="remarks"></a>解説  
 この場合に SINGLE_BLOB を使用すると、XML エンコード宣言で指定されている XML ドキュメントのエンコードと、サーバーによって暗黙的に示されている文字列のコード ページとの不一致を回避できます。  
  
 NCLOB または CLOB データ型を使用した際にコード ページまたはエンコードの競合が発生する場合は、次のいずれかの操作を行う必要があります。  
  
-   XML データ ファイルの内容を正常にインポートできるように、XML 宣言を削除します。  
  
-   XML 宣言で使用されているエンコード体系に一致するコード ページを、クエリの CODEPAGE オプションに指定します。  
  
-   データベースの照合順序の設定を Unicode 以外の XML エンコード体系に一致 (解決) させます。  
  
 [&#91;先頭に戻る&#93;](#top)  
  
##  <a name="existing_row"></a> 既存の行に XML データの一括インポートを行う  
 この例では `OPENROWSET` 一括行セット プロパイダを使用して、XML インスタンスを既存のサンプル テーブル `T`の 1 行または複数の行に追加します。  
  
> [!NOTE]  
>  この例を実行するには、まず例 A で提供されたテスト スクリプトを完了する必要があります。例 A では、 `tempdb.dbo.T` テーブルを作成し、 `SampleData3.txt`からデータを一括インポートをしています。  
  
#### <a name="sample-data-file"></a>サンプル データ ファイル  
 例 B では、例 A の `SampleData3.txt` サンプル データ ファイルを変更したバージョンを使用します。 例 B を実行するには、このファイルの内容を次のように修正します。  
  
```xml
<Root>  
          <ProductDescription ProductModelID="10">  
             <Summary>Some New Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-b"></a>例 B  
  
```sql  
-- Query before update shows initial state of XmlCol values.  
SELECT * FROM T  
UPDATE T  
SET XmlCol =(  
SELECT * FROM OPENROWSET(  
   BULK 'C:\SampleFolder\SampleData3.txt',  
           SINGLE_BLOB  
) AS x  
)  
WHERE IntCol = 1;  
GO  
```  
  
 [&#91;先頭に戻る&#93;](#top)  
  
## <a name="file_contains_dtd"></a> DTD を含むファイルから XML データの一括インポートを行う  
  
> [!IMPORTANT]  
>  作業中の XML 環境で DTD (文書型定義) が特に必要ではない場合は、DTD のサポートを無効にしておくことをお勧めします。 DTD のサポートを有効にすると、使用しているサーバーが外部からの攻撃を受けやすくなり、サービス拒否攻撃の危険にさらされる場合があります。 DTD のサポートを有効にする必要がある場合は、信頼できる XML ドキュメントのみを処理することにより、このセキュリティ上のリスクを軽減できます。  
  
 [bcp](../../tools/bcp-utility.md) コマンドを使用して、DTD を含むファイルから XML データのインポートを試みた場合に、次に示すようなエラーが表示されることがあります。  
  
 "SQLState = 42000, NativeError = 6359"  
  
 "エラー = [Microsoft][SQL Server Native Client][SQL Server]内部サブセット DTD を使用した XML の解析は許可されません。 スタイル オプション 2 を設定して CONVERT を使用し、制限付きの内部サブセット DTD のサポートを有効にしてください。"  
  
 "BCP コピー %s が失敗しました"  
  
 この問題を回避するには、XML データを DTD を含むデータ ファイルからインポートする際に `OPENROWSET(BULK...)` 関数を使用し、コマンドの `CONVERT` 句内で `SELECT` オプションを指定します。 コマンドの基本構文を次に示します。  
  
 `INSERT ... SELECT CONVERT(...) FROM OPENROWSET(BULK...)`  
  
#### <a name="sample-data-file"></a>サンプル データ ファイル  
 一括インポートの例をテストする前に、次のサンプル インスタンスを含むファイル (`C:\temp\Dtdfile.xml`) を作成します。  
  
```xml 
<!DOCTYPE DOC [<!ATTLIST elem1 attr1 CDATA "defVal1">]><elem1>January</elem1>  
```  
  
#### <a name="sample-table"></a>サンプル テーブル  
 例 C では、次の `T1` ステートメントで作成した `CREATE TABLE` サンプル テーブルを使用します。  
  
```sql  
USE tempdb;  
CREATE TABLE T1(XmlCol xml);  
GO  
```  
  
#### <a name="example-c"></a>例 C  
 この例では `OPENROWSET(BULK...)` を使用して、 `CONVERT` 句内で `SELECT` オプションを指定し、 `Dtdfile.xml` から XML データをサンプル テーブル `T1`にインポートします。  
  
```sql
INSERT T1  
  SELECT CONVERT(xml, BulkColumn, 2) FROM   
    OPENROWSET(Bulk 'c:\temp\Dtdfile.xml', SINGLE_BLOB) [rowsetresults];  
```  
  
 `INSERT` ステートメントの実行後、DTD が XML から分離され、テーブル `T1` に格納されます。  
  
 [&#91;先頭に戻る&#93;](#top)  
  
## <a name="field_terminator_in_format_file"></a> フォーマット ファイルを使用してフィールド ターミネータを明示的に指定する  
 次の例では、XML ドキュメント `Xmltable.dat`を一括インポートする方法を示します。  
  
#### <a name="sample-data-file"></a>サンプル データ ファイル  
 `Xmltable.dat` のドキュメントには 2 つの XML 値が、1 行に 1 つずつ含まれています。 最初の XML 値は UTF-16 でエンコードされており、2 番目の値は UTF-8 でエンコードされています。  
  
 このデータの内容を 16 進形式でダンプすると次のようになります。  
  
```  
FF FE 3C 00 3F 00 78 00-6D 00 6C 00 20 00 76 00  *..\<.?.x.m.l. .v.*  
65 00 72 00 73 00 69 00-6F 00 6E 00 3D 00 22 00  *e.r.s.i.o.n.=.".*  
31 00 2E 00 30 00 22 00-20 00 65 00 6E 00 63 00  *1...0.". .e.n.c.*  
6F 00 64 00 69 00 6E 00-67 00 3D 00 22 00 75 00  *o.d.i.n.g.=.".u.*  
74 00 66 00 2D 00 31 00-36 00 22 00 3F 00 3E 00  *t.f.-.1.6.".?.>.*  
3C 00 72 00 6F 00 6F 00-74 00 3E 00 A2 4F 9C 76  *\<.r.o.o.t.>..O.v*  
0C FA 77 E4 80 00 89 00-00 06 90 06 91 2E 9B 2E  *..w.............*  
99 34 A2 34 86 00 83 02-92 20 7F 02 4E C5 E4 A3  *.4.4..... ..N...*  
34 B2 B7 B3 B7 FE F8 FF-F8 00 3C 00 2F 00 72 00  *4.........\<./.r.*  
6F 00 6F 00 74 00 3E 00-00 00 00 00 7A EF BB BF  *o.o.t.>.....z...*  
3C 3F 78 6D 6C 20 76 65-72 73 69 6F 6E 3D 22 31  *\<?xml version="1*  
2E 30 22 20 65 6E 63 6F-64 69 6E 67 3D 22 75 74  *.0" encoding="ut*  
66 2D 38 22 3F 3E 3C 72-6F 6F 74 3E E4 BE A2 E7  *f-8"?><root>....*  
9A 9C EF A8 8C EE 91 B7-C2 80 C2 89 D8 80 DA 90  *................*  
E2 BA 91 E2 BA 9B E3 92-99 E3 92 A2 C2 86 CA 83  *................*  
E2 82 92 C9 BF EC 95 8E-EA 8F A4 EB 88 B4 EB 8E  *................*  
B7 EF BA B7 EF BF B8 C3-B8 3C 2F 72 6F 6F 74 3E  *.........</root>*  
00 00 00 00 7A                                   *....z*  
```  
  
#### <a name="sample-table"></a>サンプル テーブル  
 XML ドキュメントの一括インポートまたは一括エクスポートを行う際には、いずれのドキュメントにも記述されていない [フィールド ターミネータ](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md) を使用する必要があります。たとえば、一連の 4 つの Null (`\0`) の後に文字 `z`を付けた、 `\0\0\0\0z`などです。  
  
 この例では、サンプル テーブル `xTable` のフィールド ターミネータの使用方法を示します。 サンプル テーブルを作成するには、次の `CREATE TABLE` ステートメントを使用します。  
  
```sql
USE tempdb;  
CREATE TABLE xTable (xCol xml);  
GO  
```  
  
#### <a name="sample-format-file"></a>サンプル フォーマット ファイル  
 フィールド ターミネータは、フォーマット ファイルで指定する必要があります。 例 D では、次の内容を含む `Xmltable.fmt` という XML 以外のフォーマット ファイルを使用します。  
  
```  
9.0  
1  
1       SQLBINARY     0       0       "\0\0\0\0z"    1     xCol         ""  
```  
  
 このフォーマット ファイルを使用し、 `xTable` コマンドか、 `bcp` ステートメントまたは `BULK INSERT` ステートメントを使って、XML ドキュメントをテーブル `INSERT ... SELECT * FROM OPENROWSET(BULK...)` に一括インポートできます。  
  
#### <a name="example-d"></a>例 D  
 この例では、 `Xmltable.fmt` ステートメントで `BULK INSERT` フォーマット ファイルを使用して、 `Xmltable.dat`という XML データ ファイルの内容をインポートします。  
  
```sql
BULK INSERT xTable   
FROM 'C:\Xmltable.dat'  
WITH (FORMATFILE = 'C:\Xmltable.fmt');  
GO  
```  
  
 [&#91;先頭に戻る&#93;](#top)  
  
## <a name="bulk_export_xml_data"></a> XML データの一括エクスポートを行う  
 次の例では、[bcp](../../tools/bcp-utility.md) を使用し、同じ XML フォーマット ファイルを使用して、前の例で作成されたテーブルから XML データの一括エクスポートを行います。 次の `bcp` コマンドで、 `<server_name>` と `<instance_name>` はプレースホルダーであり、適切な値との差し替えが必要です。  
  
```cmd
bcp bulktest..xTable out a-wn.out -N -T -S<server_name>\<instance_name>  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML データがデータベース内に保存されるときに、 では XML エンコードが保存されません。 したがって、XML データをエクスポートするときは、XML フィールドの元のエンコードは使用できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は XML データをエクスポートする際に UTF-16 エンコードを使用します。  
  

## <a name="see-also"></a>参照  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [bcp ユーティリティ](../../tools/bcp-utility.md)   
 [データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)  
  
  
