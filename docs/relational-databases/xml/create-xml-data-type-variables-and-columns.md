---
title: XML データ型の変数と列の作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- xml data type [SQL Server], columns
ms.assetid: 8994ab6e-5519-4ba2-97a1-fac8af6f72db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16cb419ef7cc893575e91c695158e9d7b66ce2c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984868"
---
# <a name="create-xml-data-type-variables-and-columns"></a>XML データ型の変数と列の作成
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **xml** データ型は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での組み込みデータ型の 1 つであり、 **int** 、 **varchar**などの他の組み込みデータ型といくつかの点で似ている部分があります。 他の組み込みの型と同じく、 **xml** データ型はテーブルを作成するときに列の型として変数の型、パラメーターの型、および関数の戻り値の型と同様に使用したり、 [CAST および CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)で使用できます。  
  
## <a name="creating-columns-and-variables"></a>列と変数の作成  
 テーブルの一部として `xml` 型の列を作成するには、 `CREATE TABLE` ステートメントを使用します。次に例を示します。  
  
```  
CREATE TABLE T1(Col1 int primary key, Col2 xml)   
```  
  
 `DECLARE statement` を使用して `xml` 型の変数を作成できます。次に例を示します。  
  
```  
DECLARE @x xml   
```  
  
 XML スキーマ コレクションを指定して、型指定された `xml` 変数を作成します。次に例を示します。  
  
```  
DECLARE @x xml (Sales.StoreSurveySchemaCollection)  
```  
  
 `xml` 型のパラメーターをストアド プロシージャに渡すには、 `CREATE PROCEDURE` ステートメントを使用します。次に例を示します。  
  
```  
CREATE PROCEDURE SampleProc(@XmlDoc xml) AS ...   
```  
  
 XQuery を使用して、列、パラメーター、または変数に格納されている XML インスタンスにクエリを実行できます。 また、XML DML (データ操作言語) を使用して、XML インスタンスに更新を適用することもできます。 開発時点では XQuery 標準に XQuery DML が定められていなかったので、XQuery については [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML DML (XML データ変更言語) [拡張機能が](../../t-sql/xml/xml-data-modification-language-xml-dml.md) に実装されています。 この拡張機能を使用して、挿入、更新、および削除を実行できます。  
  
## <a name="assigning-defaults"></a>既定の XML の割り当て  
 テーブル内で、 **xml** 型の列に、既定の XML インスタンスを割り当てることができます。 既定の XML を割り当てるには、XML 定数を使用する方法と、 **xml** 型への明示的なキャストを使用する方法の 2 つがあります。  
  
 既定の XML を XML 定数として割り当てるには、次の例の構文を使用します。 文字列は暗黙的に **xml** 型にキャストされることに注意してください。  
  
```  
CREATE TABLE T (XmlColumn xml default N'<element1/><element2/>')  
```  
  
 既定の XML を `CAST` への明示的な `xml`として割り当てるには、次の例の構文を使用します。  
  
```  
CREATE TABLE T (XmlColumn xml   
                  default CAST(N'<element1/><element2/>' AS xml))  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** 型の列に対する NULL 制約および NOT NULL 制約もサポートされます。 例:  
  
```  
CREATE TABLE T (XmlColumn xml NOT NULL)  
```  
  
## <a name="specifying-constraints"></a>制約の指定  
 **xml** 型の列を作成するときには、列レベルまたはテーブル レベルの制約を定義できます。 制約は、次のような場合に使用してください。  
  
-   ビジネス ルールが XML スキーマでは表現できない場合。 たとえば、花屋の配達可能地域が店舗から 80 km 以内に限られている場合などです。 このルールは XML 列の制約として記述できます。 この制約には、 **xml** データ型のメソッドが必要になる場合があります。  
  
-   制約が、テーブル内の他の XML 列または XML 以外の列に関係している場合。 たとえば、XML インスタンスに現れる Customer の ID (`/Customer/@CustId`) が、CustomerID リレーショナル列の値と一致する必要がある場合などです。  
  
 制約は、型指定された **xml** データ型の列にも、型指定されていない xml データ型の列にも指定できます。 ただし、制約を指定するとき、[XML データ型のメソッド](../../t-sql/xml/xml-data-type-methods.md) は使用できません。 また、 **xml** データ型では次の列およびテーブルの制約はサポートされません。  
  
-   PRIMARY KEY/ FOREIGN KEY  
  
-   UNIQUE  
  
-   COLLATE  
  
     XML では、独自のエンコードが使用されます。 照合順序は、文字列型にのみ適用されます。 **xml** データ型は文字列型ではありません。 ただし、文字列で表記され、文字列データ型との相互のキャストが可能です。  
  
-   RULE  
  
 制約を使用する代わりに、次の例に示すように、 **xml** データ型のメソッドをラップするためのラッパーと呼ばれるユーザー定義関数を作成し、ユーザー定義関数を CHECK 制約を適用して指定します。  
  
 次の例では、 `Col2` 列に対して、保存する各 XML インスタンスには `<ProductDescription>` 属性を持つ `ProductID` 要素が必要であるという制約を指定します。 この制約は、次のユーザー定義関数によって適用されます。  
  
```  
CREATE FUNCTION my_udf(@var xml) returns bit  
AS BEGIN   
RETURN @var.exist('/ProductDescription/@ProductID')  
END  
GO  
```  
  
 インスタンスの `exist()` 要素に `xml` 属性が含まれる場合、 `1` データ型の `<ProductDescription>` メソッドは `ProductID` を返します。 それ以外の場合は `0`を返します。  
  
 ここで、次のようにして列レベルの制約を定義したテーブルを作成できます。  
  
```  
CREATE TABLE T (  
    Col1 int primary key,   
    Col2 xml check(dbo.my_udf(Col2)=1))  
GO  
```  
  
 次の挿入操作は成功します。  
  
```  
INSERT INTO T values(1,'<ProductDescription ProductID="1" />')  
```  
  
 次の挿入操作は制約に違反するため失敗します。  
  
```  
INSERT INTO T values(1,'<Product />')  
```  
  
## <a name="same-or-different-table"></a>同じテーブルと別のテーブル  
 **xml** データ型の列は、他にリレーショナル列が存在するテーブルにも作成できます。また、メインのテーブルと外部キー リレーションシップがある別のテーブルにも作成できます。  
  
 次の条件のいずれかに該当する場合は、同一のテーブルに **xml** データ型の列を作成してください。  
  
-   XML 列のデータを取得するが、その列に XML インデックスは不要な場合。  
  
-   **xml** データ型の列に XML インデックスを作成するときに、メイン テーブルの主キーがクラスター化キーと同一である場合。 詳細については、「[XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)」をご覧ください。  
  
 次の条件に該当する場合は、別のテーブルに **xml** データ型の列を作成してください。  
  
-   **xml** データ型の列に XML インデックスを作成するときに、メイン テーブルの主キーがクラスター化キーと異なる場合、メイン テーブルに主キーがない場合、またはメイン テーブルがヒープである (クラスター化キーがない) 場合。 メイン テーブルが既に存在する場合、これに該当している可能性があります。  
  
-   テーブルに XML 列が存在することでテーブル スキャンが遅くなるのを避ける場合。 テーブル スキャンは、XML が行内に保存されていても行外に保存されていても領域を消費します。  
  
  
