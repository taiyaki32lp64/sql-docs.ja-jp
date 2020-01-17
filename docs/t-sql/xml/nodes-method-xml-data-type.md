---
title: nodes() メソッド (xml データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nodes() method
- nodes method
ms.assetid: 7267fe1b-2e34-4213-8bbf-1c953822446c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a0648ea24162f59562f6d7a68dd5007ca78be3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051272"
---
# <a name="nodes-method-xml-data-type"></a>nodes() メソッド (xml データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**Nodes()** メソッドは、細分化する場合に便利な **xml** データ型のインスタンスをリレーショナル データにします。 新しい行にマップされるノードを特定できます。  
  
すべての **xml** データ型のインスタンスには、コンテキスト ノードが暗黙に用意されています。 列や変数に格納された XML インスタンスの場合は、このノードがコンテキスト ノードになります。 このドキュメント ノードは、すべての **xml** データ型のインスタンスの最上位に位置する暗黙のノードです。  
  
**nodes()** メソッドの結果は、元の XML インスタンスの論理コピーを含む行セットです。 このような論理コピーでは、クエリ式で識別されるいずれかのノードが、すべての行インスタンスのコンテキスト ノードに設定されます。 このように、その後に実行されるクエリはこのようなコンテキスト ノードへ相対移動できます。  
  
行セットからは、複数の値を取得できます。 たとえば、**value()** メソッドを **nodes()** で返される行セットに適用し、元の XML インスタンスから複数の値を取得できます。 **value()** メソッドを XML インスタンスに適用すると、値は 1 つしか返されません。  
  
## <a name="syntax"></a>構文  
  
```sql
  
nodes (XQuery) as Table(Column)  
```  
  
## <a name="arguments"></a>引数  
*XQuery*  
XQuery 式の文字列リテラルです。 このクエリ式でノードが構築されると、構築されるノードが結果の行セットで公開されます。 クエリ式の結果が空のシーケンスの場合、行セットも空になります。 クエリ式で、ノードではなくアトミック値が含まれたシーケンスが静的に返される場合は、静的エラーが発生します。  
  
*テーブル*(*列*)  
結果の行セットのテーブル名と列名です。  
  
## <a name="remarks"></a>Remarks  
たとえば、次のテーブルがあるとします。  
  
```sql
T (ProductModelID int, Instructions xml)  
```  
  
次の製造手順ドキュメントがこのテーブルに格納されます。 記載しているのはドキュメントの一部のみです。 このドキュメントには 3 つの製造場所が含まれていることに注意してください。  
  
```sql
<root>  
  <Location LocationID="10"...>  
     <step>...</step>  
     <step>...</step>  
      ...  
  </Location>  
  <Location LocationID="20" ...>  
       ...  
  </Location>  
  <Location LocationID="30" ...>  
       ...  
  </Location>  
</root>  
```  
  
クエリ式 `/root/Location` を指定して `nodes()` メソッドを呼び出すと、次のように 3 つの行を持つ行セットが返されます。各行には元の XML ドキュメントの論理コピーが格納されており、いずれかの `<Location>` ノードがコンテキスト アイテムに設定されます。  
  
```sql
Product  
ModelID      Instructions  
----------------------------------  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
```  
  
この行セットには、**xml** データ型のメソッドを使用してクエリを実行できます。 次のクエリを実行すると、生成された行ごとにコンテキスト アイテムのサブツリーが抽出されます。  
  
```sql
SELECT T2.Loc.query('.')  
FROM   T  
CROSS APPLY Instructions.nodes('/root/Location') as T2(Loc)   
```  
  
以下に結果を示します。  
  
```sql
ProductModelID  Instructions  
----------------------------------  
1        <Location LocationID="10" ... />  
1        <Location LocationID="20" ... />  
1        <Location LocationID="30" .../>  
```  
  
返された行セットでは型情報が保持されます。 **nodes()** メソッドの結果には、**query()** 、**value()** 、**exist()** 、**nodes()** など、**xml** データ型のメソッドを適用できます。 ただし、**modify()** メソッドを適用して XML インスタンスを変更することはできません。  
  
また、行セットのコンテキスト ノードは具体化できません。 つまり、このコンテキスト ノードは SELECT ステートメントでは使用できません。 ただし、IS NULL と COUNT(*) では使用できます。  
  
**nodes()** メソッドを使用するシナリオは、XML の行セット ビューを提供する [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md) を使用する場合と同じです。 ただし、XML ドキュメントの複数の行が含まれるテーブルに **nodes()** メソッドを使用するときは、カーソルを使用する必要はありません。  
  
**nodes()** メソッドで返される行セットには名前が付きません。 したがって、別名を使用してこれらの行セットに明示的に名前を付ける必要があります。  
  
**nodes()** 関数をユーザー定義関数の結果に直接適用することはできません。 **nodes()** 関数と共にスカラー ユーザー定義関数を使用するには、次のいずれかを行います。
 
- ユーザー定義関数の結果を変数に割り当てる
- 派生テーブルを使用して列エイリアスをユーザー定義関数の戻り値に割り当て、`CROSS APPLY` を使用してエイリアスから選択する  
  
次の例では、`CROSS APPLY` を使用し、ユーザー定義関数の結果から選択する方法を示します。  
  
```sql
USE AdventureWorks;  
GO  
  
CREATE FUNCTION XTest()  
RETURNS xml  
AS  
BEGIN  
RETURN '<document/>';  
END;  
GO  
  
SELECT A2.B.query('.')  
FROM  
(SELECT dbo.XTest()) AS A1(X)   
CROSS APPLY X.nodes('.') A2(B);  
GO  
  
DROP FUNCTION XTest;  
GO  
```  
  
## <a name="examples"></a>使用例  
  
### <a name="using-nodes-method-against-a-variable-of-xml-type"></a>xml 型の変数に対する nodes() メソッドの使用  
次の例では、<`Root`> 最上位要素と 3 つの <`row`> 子要素が含まれる XML ドキュメントを使用します。 このクエリでは、`nodes()` メソッドを使用して、各 <`row`> 要素に 1 つずつ別のコンテキスト ノードを設定します。 `nodes()` メソッドにより、3 つの行を持つ行セットが返されます。 各行には元の XML の論理コピーが含まれ、それぞれのコンテキスト ノードで元のドキュメントの異なる <`row`> 要素が識別されます。  
  
その後、次のクエリを実行すると、各行のコンテキスト ノードが返されます。  
  
```sql
DECLARE @x xml   
SET @x='<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>'  
SELECT T.c.query('.') AS result  
FROM   @x.nodes('/Root/row') T(c)  
GO  
```  
  
次の例の結果では、クエリのメソッドでコンテキスト アイテムとそのコンテンツが返されます。  
  
```sql
<row id="1"><name>Larry</name><oflw>some text</oflw></row>  
<row id="2"><name>moe</name></row>  
<row id="3"/>  
```  
  
次のように、親アクセサーをコンテキスト ノードに適用すると、3 つのノードすべての <`Root`> 要素が返されます。  
  
```sql
SELECT T.c.query('..') AS result  
FROM   @x.nodes('/Root/row') T(c)  
go  
```  
  
以下に結果を示します。  
  
```sql
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
```  
  
### <a name="specifying-the-nodes-method-against-a-column-of-xml-type"></a>xml 型の列に対する nodes() メソッドの指定  
この例では、**ProductModel** テーブルの **xml** 型の Instructions 列に格納されている、自転車の製造手順を使用します。  
  
次の例では、`ProductModel` テーブルの **xml** 型の `Instructions` 列に対して `nodes()` メソッドを指定します。  
  
`/MI:root/MI:Location` パスを指定することで、`nodes()` メソッドでは <`Location`> 要素がコンテキスト ノードに設定されます。 結果の行セットには、ドキュメントの各 <`Location`> ノードに 1 つずつ元のドキュメントの論理コピーが含まれます。また、その <`Location`> 要素がコンテキスト ノードに設定されます。 結果として、`nodes()` 関数から返されるのは、<`Location`> コンテキスト ノードのセットです。  
  
この行セットに対する `query()` メソッドでは `self::node` が要求されるため、各行の `<Location>` 要素が返されます。  
  
この例のクエリでは、各 <`Location`> 要素が、特定の製品モデルの製造手順ドキュメントのコンテキスト ノードとして設定されます。 これらのコンテキスト ノードを使用して、次のような値を取得できます。  
  
- 各 <`Location`> の場所 ID  
  
- 各 <`Location`> の製造手順 (<`step`> 子要素)  
  
このクエリでは、`'.'` メソッドで `self::node()` に対する省略構文 `query()` を指定して、コンテキスト アイテムを返しています。  
  
次のことを考慮してください。
  
- `nodes()` メソッドは Instructions 列に適用され、行セット `T (C)` を返します。 この行セットには、`/root/Location` をコンテキスト アイテムとして、元の製造手順ドキュメントの論理コピーが格納されています。  
  
- CROSS APPLY により、`Instructions` テーブルの各行に `nodes()` が適用され、結果セットを生成する行のみが返されます。  
  
    ```sql  
    SELECT C.query('.') as result  
    FROM Production.ProductModel  
    CROSS APPLY Instructions.nodes('  
    declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /MI:root/MI:Location') as T(C)  
    WHERE ProductModelID=7  
    ```  
  
  次に結果の一部を示します。  
  
    ```sql
    <MI:Location LocationID="10"  ...>  
       <MI:step ... />  
          ...  
    </MI:Location>  
    <MI:Location LocationID="20"  ... >  
        <MI:step ... />  
          ...  
    </MI:Location>  
    ...  
    ```  
  
### <a name="applying-nodes-to-the-rowset-returned-by-another-nodes-method"></a>別の nodes() メソッドにより返された行セットに対する nodes() の適用  
次のコードでは、XML ドキュメントに対し、`Instructions` テーブルの `ProductModel` 列に格納されている製造手順をクエリしています。 このクエリでは、製品モデル ID、製造場所、および製造手順が含まれた行セットが返されます。  
  
次のことを考慮してください。  
  
- `nodes()` メソッドは `Instructions` 列に適用され、`T1 (Locations)` 行セットを返します。 この行セットには、`/root/Location` 要素をコンテキスト アイテムとして、元の製造手順ドキュメントの論理コピーが格納されています。  
  
- `nodes()` は `T1 (Locations)` 行セットに適用され、`T2 (steps)` 行セットを返します。 この行セットには、`/root/Location/step` 要素をコンテキスト アイテムとして、元の製造手順ドキュメントの論理コピーが格納されています。  
  
```sql
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO         
```  
  
以下に結果を示します。  
  
```sql
ProductModelID LocID Step         
----------------------------         
7      10   <step ... />         
7      10   <step ... />         
...         
7      20   <step ... />         
7      20   <step ... />         
7      20   <step ... />         
...         
```  
  
このクエリでは、`MI` プレフィックスを 2 回宣言しています。 代わりに `WITH XMLNAMESPACES` を使用し、このプレフィックスを 1 回宣言してクエリで使用することもできます。  
  
```sql
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions'  AS MI)  
  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO    
```  
  
## <a name="see-also"></a>参照  
[WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
[XML データのインスタンスの作成](../../relational-databases/xml/create-instances-of-xml-data.md)   
[xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)  
  
  
