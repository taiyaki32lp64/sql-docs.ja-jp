---
title: XML データのインスタンスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- type casting string instances [XML in SQL Server]
- XML [SQL Server], typed
- xml data type [SQL Server], generating instances
- casting string instances [XML in SQL Server]
- typed XML
- generating XML instances [SQL Server]
- XML [SQL Server], generating instances
- white space [XML in SQL Server]
ms.assetid: dbd6c06f-db6e-44a7-855a-6a55bf374907
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbdae019d2b4903bcebb0339df0ef243d6974766
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112922"
---
# <a name="create-instances-of-xml-data"></a>XML データのインスタンスの作成
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  このトピックでは、XML インスタンスを生成する方法について説明します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、次の方法で XML インスタンスを生成できます。  
  
-   文字列インスタンスの型をキャストする。  
  
-   FOR XML 句を指定した SELECT ステートメントを使用する。  
  
-   定数の代入を使用する。  
  
-   一括読み込みを使用する。  
  
## <a name="type-casting-string-and-binary-instances"></a>文字列インスタンスとバイナリ インスタンスの型キャスト  
 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] n **][** var **]** char **、** [n]text **、** varbinary **、** image **などの**の文字列データ型は、 **xml** データ型にキャスト (CAST) または変換 (CONVERT) することにより、 **xml** データ型に解析できます。 型指定されていない XML は、正しい形式かどうかが確認されます。 **xml** 型に関連付けられたスキーマがある場合は、検証も行われます。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
 XML ドキュメントは、UTF-8、UTF-16、windows-1252 など、さまざまなエンコードを使用してエンコードできます。 ここでは、文字列およびバイナリの元のデータ型と XML ドキュメントのエンコード間の相互作用における規則、およびパーサーの動作に関する規則を概説します。  
  
 **nvarchar** 型は UTF-16 や UCS-2 などの 2 バイト Unicode エンコードを想定しているので、XML パーサーは文字列値を 2 バイト Unicode でエンコードされた XML ドキュメントまたは XML フラグメントとして処理します。 つまり、XML ドキュメントには、元のデータ型との互換性だけでなく、2 バイト Unicode エンコードでのエンコードも必要であるということになります。 UTF-16 でエンコードされた XML ドキュメントでは、UTF-16 バイト順マーク (BOM) を指定できますが、指定する必要はありません。これは、変換元データ型のコンテキストにより、2 バイト Unicode でエンコードされたドキュメントに限定されることが明確であるためです。  
  
 **varchar** 文字列の内容は、XML パーサーによって、1 バイトでエンコードされた XML ドキュメントまたは XML フラグメントとして扱われます。 **varchar** の変換元文字列にはコード ページが関連付けられているので、明示的なエンコード方法が XML 自体に指定されていない場合、XML パーサーはそのコード ページを使用してエンコードを行います。XML インスタンスに BOM またはエンコード宣言がある場合、このコード ページとの一貫性が必要になります。そうでない場合、XML パーサーからエラーが報告されます。  
  
 **varbinary** の内容は、XML パーサーに直接渡されるコードポイント ストリームとして処理されます。 このため、XML ドキュメントまたは XML フラグメントに、BOM またはその他のエンコード情報をインラインで指定する必要があります。 XML パーサーは、ストリームからのみエンコード方法を判断します。 つまり、UTF-16 でエンコードされた XML には UTF-16 BOM を指定する必要があり、BOM やエンコード宣言のない XML インスタンスは UTF-8 として解釈されます。  
  
 XML ドキュメントのエンコードが事前にわからないために、XML にキャストする前に XML データではなく文字列データまたはバイナリ データとしてデータが渡される場合は、そのデータを **varbinary**として処理することをお勧めします。 たとえば、OpenRowset() を使用して XML ファイルからデータを読み取る場合、次のように、そのデータを **varbinary(max)** 値として読み取るように指定してください。  
  
```  
select CAST(x as XML)   
from OpenRowset(BULK 'filename.xml', SINGLE_BLOB) R(x)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部では、UTF-16 エンコードを使用した効率のよいバイナリ表記で XML が表現されます。 ユーザーが指定したエンコードは保持されませんが、解析処理時に考慮されます。  
  
### <a name="type-casting-clr-user-defined-types"></a>CLR ユーザー定義型の型キャスト  
 CLR ユーザー定義型で XML シリアル化を指定している場合は、その型のインスタンスを XML データ型に明示的にキャストすることができます。 CLR ユーザー定義型の XML シリアル化の詳細については、「 [XML Serialization from CLR Database Objects](https://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344)」を参照してください。  
  
### <a name="white-space-handling-in-typed-xml"></a>型指定された XML の空白文字の処理  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、要素の内容に含まれる空白文字は、開始タグや終了タグなどのマークアップで区切られた空白文字だけのシーケンス内に出現し、エンティティに変換されていない場合、重要でないと見なされます (CDATA セクションは無視されます)。この空白文字の処理は、W3C (World Wide Web Consortium) から公開されている XML 1.0 仕様の空白文字に関する記述とは異なります。 これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の XML パーサーが XML 1.0 の定義に従って、限定された数の DTD サブセットしか認識しないためです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされる限定された DTD サブセット数の詳細については、「[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。  
  
 XML パーサーは、既定では、文字列データを XML に変換するときに、次のいずれかの条件に当てはまる場合は、重要ではない空白文字を破棄します。  
  
-   `xml:space` 属性が、要素またはその先祖の要素で定義されていない。  
  
-   要素またはその先祖の要素の 1 つで有効になっている `xml:space` 属性に既定値が設定されている。  
  
 例:  
  
```  
declare @x xml  
set @x = '<root>      <child/>     </root>'  
select @x   
```  
  
 結果を次に示します。  
  
```  
<root><child/></root>  
```  
  
 ただし、この動作は変更できます。 xml DT インスタンスの空白文字を保持するには、CONVERT 演算子を使用し、省略可能な *style* パラメーターを値 1 に設定します。 例:  
  
```  
SELECT CONVERT(xml, N'<root>      <child/>     </root>', 1)  
```  
  
 *style* パラメーターが使用されていないか、この値が 0 に設定されていると、xml DT インスタンスの変換では重要でない空白文字は保持されません。 文字列データを xml DT インスタンスに変換するときの、CONVERT 演算子と *style* パラメーターの使用方法の詳細については、「[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>例: 型指定された xml に文字列値をキャストし、列に割り当てる  
 次の例では、XML フラグメントを格納した文字列変数を **xml** データ型にキャストし、 **xml** 型の列に格納します。  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 次の挿入操作では、文字列から **xml** 型に暗黙的に変換が行われます。  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 cast() を使用すると、文字列を **xml** 型に明示的にキャストできます。  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 または、次に示すように convert() を使用できます。  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>例: 型指定された xml に文字列を変換し、変数に割り当てる  
 次の例では、文字列を **xml** 型に変換し、 **xml** データ型の変数に割り当てます。  
  
```  
declare @x xml  
declare  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
set @x =convert (xml, @s)  
select @x  
```  
  
## <a name="using-the-select-statement-with-a-for-xml-clause"></a>FOR XML 句を指定した SELECT ステートメントの使用  
 SELECT ステートメントに FOR XML 句を使用すると、結果を XML として返すことができます。 例:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = (SELECT Column1, Column2  
               FROM   Table1, Table2  
               WHERE   Some condition  
               FOR XML AUTO)  
 ...  
```  
  
 SELECT ステートメントはテキスト形式の XML フラグメントを返します。これは、 **xml** データ型の変数への代入時に解析されます。  
  
 FOR XML 句で FOR XML 句の [TYPE ディレクティブ](../../relational-databases/xml/type-directive-in-for-xml-queries.md) を使用することもできます。その場合、FOR XML クエリの結果が直接 **xml** 型で返されます。  
  
```  
Declare @xmlDoc xml  
SET @xmlDoc = (SELECT ProductModelID, Name  
               FROM   Production.ProductModel  
               WHERE  ProductModelID=19  
               FOR XML AUTO, TYPE)  
SELECT @xmlDoc  
```  
  
 結果を次に示します。  
  
```  
<Production.ProductModel ProductModelID="19" Name="Mountain-100" />...  
```  
  
 次の例では、FOR XML クエリの型指定された **xml** の結果を、**xml** 型の列に挿入します。  
  
```  
CREATE TABLE T1 (c1 int, c2 xml)  
go  
INSERT T1(c1, c2)  
SELECT 1, (SELECT ProductModelID, Name  
           FROM Production.ProductModel  
           WHERE ProductModelID=19  
           FOR XML AUTO, TYPE)  
SELECT * FROM T1  
go  
```  
  
 FOR XML の詳細については、「[FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TYPE ディレクティブを使用する FOR XML クエリや、 **xml** データ型を使用して SQL 列、変数、および出力パラメーターから XML を返す FOR XML クエリなど、異なるサーバー構成の結果として、 **xml** データ型インスタンスをクライアントに返します。 クライアント アプリケーションのコードでは、ADO.NET プロバイダーがこの **xml** データ型情報をサーバーからバイナリ エンコード形式で送信するよう要求します。 ただし、TYPE ディレクティブを指定しないで FOR XML を使用した場合、XML データは文字列型のデータとして返されます。 どんな場合でも、クライアント プロバイダーは常にいずれかの形式の XML を処理できます。  
  
## <a name="using-constant-assignments"></a>定数の代入の使用  
 **xml** データ型のインスタンスが必要な場所に、文字列定数を使用できます。 これは、文字列から XML への暗黙の CAST と同じです。 例:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 上記の例では、文字列が **xml** データ型に暗黙的に変換され、 **xml** 型の変数に代入されます。  
  
 次の例では、 **xml** 型の列に定数文字列を挿入します。  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  型指定された XML では、指定したスキーマに対して XML が検証されます。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
## <a name="using-bulk-load"></a>一括読み込みの使用  
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md) 機能が強化され、データベースに XML ドキュメントを一括読み込みできるようになりました。 ファイルからデータベース内の **xml** 型の列に、XML インスタンスを一括読み込みできます。 作業用サンプルについては、「[XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)」を参照してください。 XML ドキュメントの読み込みの詳細については、「[XML データの読み込み](../../relational-databases/xml/load-xml-data.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[XML データの取得および XML データに対するクエリの実行](../../relational-databases/xml/retrieve-and-query-xml-data.md)|XML インスタンスをデータベースに格納するときに保持されない部分について説明します。|  
  
## <a name="see-also"></a>参照  
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [xml データ型のメソッド](../../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [XML Data &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
