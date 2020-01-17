---
title: OPENXML (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs:
- TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9dacd09604661f9880533fcdcafd2fb7ab9ab12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914591"
---
# <a name="openxml-transact-sql"></a>OPENXML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  OPENXML は XML ドキュメントに対して行セット ビューを提供します。 OPENXML は行セット プロバイダーなので、テーブル、ビュー、または OPENROWSET 関数など、行セット プロバイダーを指定できる [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの中で使用できます。  
  
 ![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>引数  
 *idoc*  
 XML ドキュメントの内部表現のドキュメント ハンドルを指定します。 XML ドキュメントの内部表現は、**sp_xml_preparedocument** を呼び出すことによって作成されます。  
  
 *rowpattern*  
 渡されるノードを行として識別するのに使用される XPath パターンです。 ノードの取得元は XML ドキュメントで、そのハンドルは *idoc* パラメーターで渡されます。
  
 *flags*  
 XML データとリレーショナル行セットとの間で使用するマッピング、およびオーバーフローした列の処理方法を指定します。 *flags* は省略可能な入力パラメーターで、次のいずれかの値を指定できます。  
  
|バイト値|[説明]|  
|----------------|-----------------|  
|**0**|既定では、**属性中心**のマッピングが使用されます。|  
|**1**|**属性中心**のマッピングを使用します。 XML_ELEMENTS と組み合わせることができます。 この場合、最初に**属性中心**のマッピングが適用されます。 次に、**要素中心**のマッピングが残りの列に適用されます。|  
|**2**|**要素中心**のマッピングを使用します。 XML_ATTRIBUTES と組み合わせることができます。 この場合、最初に**属性中心**のマッピングが適用されます。 次に、**要素中心**のマッピングが残りの列に適用されます。|  
|**8**|XML_ATTRIBUTES または XML_ELEMENTS と組み合わせる (論理和) ことができます。 取得のコンテキストにおいて、このフラグは、使用したデータをオーバーフロー プロパティ **\@mp:xmltext** にコピーしないことを示します。|  
  
 _SchemaDeclaration_  
 スキーマ定義を次の形式で指定します。_ColName_*ColType* [_ColPattern_ | _MetaProperty_] [ **,** _ColNameColType_ [_ColPattern_ | _MetaProperty_]...]  
  
 _ColName_  
 行セット内の列名を指定します。  
  
 *ColType*  
 行セット内の列の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を指定します。 列のデータ型が、基になる属性の **xml** データ型とは異なる場合、強制型変換が行われます。  
  
 *ColPattern*  
 XML ノードを列へマップする方法を表す標準 XPath パターンを指定します (省略可能)。 *ColPattern* を指定しない場合、既定のマッピング (*flags* で指定した**属性中心**または**要素中心**のマッピング) が適用されます。  
  
 *ColPattern* として指定した XPath パターンは、**属性中心**および**要素中心**のマッピングの場合に、*flags* で指定される既定のマッピングを上書きまたは拡張する、特殊なマッピング特性を指定するときに使用されます。  
  
 *ColPattern* で指定する標準 XPath パターンでは、メタプロパティもサポートされます。  
  
 *MetaProperty*  
 OPENXML で提供されるメタプロパティの 1 つを指定します。 *MetaProperty* を指定すると、メタプロパティで提供される情報が列に格納されます。 メタプロパティによって、XML ノードの情報 (相対的な位置や名前空間の情報など) を抽出できます。 これらのメタプロパティにより、テキストとして表示されている情報よりも多くの情報が表示されます。  
  
 *TableName*  
 目的のスキーマを備えたテーブルが既に存在し、列パターンが必要ない場合は、*SchemaDeclaration* の代わりにテーブル名を指定できます。  
  
## <a name="remarks"></a>Remarks  
 WITH 句を、*SchemaDeclaration*、または既存の *TableName* と共に使用すると、行セットの形式、および必要に応じて追加のマッピング情報を指定できます。 WITH 句の指定を省略すると、結果は**エッジ** テーブル形式で返されます。 エッジ テーブルでは、1 つのテーブル内での詳細な XML ドキュメントの構造 (要素/属性名、ドキュメント階層、名前空間、PI など) が表されます。  
  
 次の表で、**エッジ** テーブルの構造について説明します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|ドキュメント ノードの一意の ID。<br /><br /> ルート要素の ID 値は 0 です。 負の ID 値は予約済みです。|  
|**parentid**|**bigint**|ノードの親の識別子。 この ID によって識別される親は、必ずしも親要素ではなく、ノードの NodeType に依存します。その親は、この ID によって識別されます。 たとえば、ノードがテキスト ノードである場合、その親は属性ノードである場合もあります。<br /><br /> ノードが XML ドキュメントの最上位にある場合、その **ParentID** は NULL になります。|  
|**nodetype**|**int**|ノードの型を識別します。 XML DOM ノードの型番号に対応する整数です。<br /><br /> ノードの型は次のとおりです。<br /><br /> 1 = 要素ノード<br /><br /> 2 = 属性ノード<br /><br /> 3 = テキスト ノード|  
|**localname**|**nvarchar**|要素または属性のローカル名。 DOM オブジェクトに名前がない場合は NULL になります。|  
|**prefix**|**nvarchar**|ノード名の名前空間のプレフィックス。|  
|**namespaceuri**|**nvarchar**|ノードの名前空間 URI。 値が NULL の場合、名前空間はありません。|  
|**datatype**|**nvarchar**|要素または属性行の実際のデータ型。それ以外の行は NULL になります。 データ型は、インライン DTD またはインライン スキーマから推定されます。|  
|**prev**|**bigint**|前の兄弟要素の XML ID。 前に直接の兄弟がない場合は NULL になります。|  
|**text**|**ntext**|テキスト形式の属性値または要素の内容を含みます (または、**エッジ** テーブル エントリに値が必要ない場合は NULL になります)。|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. OPENXML と共に単純な SELECT ステートメントを使用する  
 次の例では、`sp_xml_preparedocument` を使用して XML イメージの内部表現を作成します。 次に、XML ドキュメントの内部表現に対して、`SELECT` 行セット プロバイダーを使用して `OPENXML` ステートメントを実行します。  
  
 *flag* の値は、`1` に設定されています。 この値は**属性中心**のマッピングを示します。 したがって、XML 属性は行セット内の列にマップされます。 *rowpattern* は `/ROOT/Customer` として指定します。これは `<Customers>` ノードを処理することを示します。  
  
 列名が XML 属性名と一致しているので、省略可能な *ColPattern* (列パターン) パラメーターは指定しません。  
  
 `OPENXML` 行セット プロバイダーでは、2 列の行セット (`CustomerID` および `ContactName`) が作成されます。`SELECT` ステートメントでは、これらの行セットから必要な列 (この場合はすべての列) を取得します。  
  
```  
DECLARE @idoc int, @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;  
-- Execute a SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customer',1)  
            WITH (CustomerID  varchar(10),  
                  ContactName varchar(20));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 *flags* を `2` に設定して (**要素中心**のマッピングを示します) 同じ `SELECT` ステートメントを実行すると、XML ドキュメント内の両方の顧客に対する `CustomerID` および `ContactName` の値が NULL として返されます。これは、`CustomerID` または `ContactName` という名前の要素が XML ドキュメント内に存在しないためです。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. 列と XML 属性の間のマッピングに ColPattern を指定する  
 次のクエリでは、XML ドキュメントから顧客 ID、注文日、製品 ID、および数量の属性を返します。 *rowpattern* によって、`<OrderDetails>` 要素が識別されます。 `ProductID` および `Quantity` は、`<OrderDetails>` 要素の属性です。 ただし、`OrderID`、`CustomerID`、および `OrderDate` は、親要素 (`<Orders>`) の属性です。  
  
 次のマッピングでは、省略可能な *ColPattern* を指定します。  
  
-   行セット内の `OrderID`、`CustomerID`、および `OrderDate` 列は、XML ドキュメント内の *rowpattern* によって識別されるノードの親の属性にマップされます。  
  
-   行セット内の `ProdID` 列は `ProductID` 属性にマップされます。行セット内の `Qty` 列は *rowpattern* によって識別されるノードの `Quantity` 属性にマップされます。  
  
 *flags* パラメーターでは**要素中心**のマッピングを指定しますが、これは *ColPattern* で指定するマッピングで上書きされます。  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">v  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';   
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT stmt using OPENXML rowset provider  
SELECT *  
FROM   OPENXML (@idoc, '/ROOT/Customer/Order/OrderDetail',2)   
         WITH (OrderID       int         '../@OrderID',   
               CustomerID  varchar(10) '../@CustomerID',   
               OrderDate   datetime    '../@OrderDate',   
               ProdID      int         '@ProductID',   
               Qty         int         '@Quantity');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
OrderID CustomerID           OrderDate                 ProdID    Qty  
------------------------------------------------------------------------  
10248      VINET       1996-07-04 00:00:00.000   11      12  
10248      VINET       1996-07-04 00:00:00.000   42      10  
10283      LILAS       1996-08-16 00:00:00.000   72      3  
```  
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>C. エッジ テーブル形式で結果を取得する  
 次の例の XML ドキュメントは、`<Customers>`、`<Orders>`、および `<Order_0020_Details>` 要素で構成されています。 まず、**sp_xml_preparedocument** を呼び出してドキュメント ハンドルを取得します。 このドキュメント ハンドルは `OPENXML` に引き渡されます。  
  
 `OPENXML` ステートメントの *rowpattern* (`/ROOT/Customers`) によって、処理する `<Customers>` ノードが識別されます。 WITH 句を指定しないため、`OPENXML` では行セットが**エッジ** テーブル形式で返されます。  
  
 最後に、`SELECT` ステートメントで、**エッジ** テーブルに含まれるすべての列を取得します。  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customers CustomerID="VINET" ContactName="Paul Henriot">  
   <Orders CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <Order_x0020_Details OrderID="10248" ProductID="11" Quantity="12"/>  
      <Order_x0020_Details OrderID="10248" ProductID="42" Quantity="10"/>  
   </Orders>  
</Customers>  
<Customers CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Orders CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <Order_x0020_Details OrderID="10283" ProductID="72" Quantity="3"/>  
   </Orders>  
</Customers>  
</ROOT>';  
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customers')   
EXEC sp_xml_removedocument @idoc;  
  
```  
  
## <a name="see-also"></a>参照  
 [例:OPENXML の使用](../../relational-databases/xml/examples-using-openxml.md)  
  
