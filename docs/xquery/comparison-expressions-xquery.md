---
title: 比較式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- node comparison operators [XQuery]
- comparison expressions [XQuery]
- node order comparison operators [XQuery]
- expressions [XQuery], comparison
- comparison operators [XQuery]
- value comparison operators
ms.assetid: dc671348-306f-48ef-9e6e-81fc3c7260a6
author: rothja
ms.author: jroth
ms.openlocfilehash: 7462e089f70b4da76edea25dcfe6e7e314ad7c46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039030"
---
# <a name="comparison-expressions-xquery"></a>比較式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery には、次の種類の比較演算子が用意されています。  
  
-   一般的な比較演算子  
  
-   値の比較演算子  
  
-   ノードの比較演算子  
  
-   ノード順の比較演算子  
  
## <a name="general-comparison-operators"></a>一般的な比較演算子  
 一般的な比較演算子を使用して、アトミック値、シーケンス、またはその 2 つの組み合わせを比較できます。  
  
 一般的な演算子を次の表に定義します。  
  
|演算子|説明|  
|--------------|-----------------|  
|=|等しい|  
|!=|等しくない|  
|\<|次の値未満|  
|>|より大きい|  
|\<=|以下|  
|>=|以上|  
  
 一般的な比較演算子を使用して 2 つのシーケンスを比較すると、最初のシーケンス内の値を比較する 2 番目のシーケンス値が存在する、全体的な結果は True です。 それ以外の場合、False になります。 たとえば、(1, 2, 3) = (3, 4) は両方のシーケンスに値 3 があるので True になります。  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3) = (3,4)')    
```  
  
 比較する 2 つの値の型は、比較できる型である必要があります。 具体的には、値の型は静的に確認されます。 数値の比較の場合、数値型の上位変換が発生する場合があります。 たとえば、10 進値の 10 が double 値 1e1 と比較される場合は、10 進数の値が二重に変更されます。 double 値の比較は正確には行えないので、不正確な結果になる場合があります。  
  
 値のいずれかが型指定された場合は、その他の値の型にキャストされます。 次の例では、値 7 が整数として扱われます。 比較する前に、型指定されていない値/a [1] は整数に変換します。 整数の比較は True を返します。  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < 7')  
```  
  
 逆に、型指定されていない値が文字列または別の型指定されていない値と比較される場合、xs:string にキャストされます。 次のクエリでは、文字列 6 が文字列「17」と比較されます。 このクエリは文字列の比較になるので、False が返されます。  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < "17"')  
```  
  
 次のクエリでは、AdventureWorks サンプル データベースで提供されている製品カタログから製品モデルの小さいサイズの写真を返します。 クエリによって返されるアトミック値のシーケンスを比較する`PD:ProductDescription/PD:Picture/PD:Size`単一のシーケンス"small"とします。 比較が True のかどうか、それを返します、< 画像\>要素。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('         
    for $P in /PD:ProductDescription/PD:Picture[PD:Size = "small"]         
    return $P') as Result         
FROM   Production.ProductModel         
WHERE  ProductModelID=19         
```  
  
 次のクエリで電話番号のシーケンスを比較する < 数\>文字列リテラル「112-111-1111」する要素。 クエリでは、特定の顧客の特定の電話番号が、ドキュメントに存在するかどうかを判断するのには、AdditionalContactInfo 列内の電話番号の要素のシーケンスを比較します。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.value('         
   /aci:AdditionalContactInfo//act:telephoneNumber/act:number = "112-111-1111"', 'nvarchar(10)') as Result         
FROM Person.Contact         
WHERE ContactID=1         
```  
  
 クエリから True が返されます。 これは、その数字がドキュメント内に存在することを示します。 次のクエリは、前のクエリの少し変更を加えたバージョンです。 このクエリでは、2 つの電話番号の値のシーケンスをドキュメントから取得された電話番号の値が比較されます。 比較が True の場合、< 数\>要素が返されます。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('         
  if (/aci:AdditionalContactInfo//act:telephoneNumber/act:number = ("222-222-2222","112-111-1111"))         
  then          
     /aci:AdditionalContactInfo//act:telephoneNumber/act:number         
  else         
    ()') as Result         
FROM Person.Contact         
WHERE ContactID=1  
  
```  
  
 結果を次に示します。  
  
```  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    112-111-1111  
\</act:number>   
```  
  
## <a name="value-comparison-operators"></a>値の比較演算子  
 値の比較演算子は、アトミック値を比較するために使用されます。 一般的な比較演算子、クエリで値の比較演算子ではなく使用できますに注意してください。  
  
 値の比較演算子は、次の表で定義されます。  
  
|演算子|説明|  
|--------------|-----------------|  
|eq|等しい|  
|ne|等しくない|  
|lt|次の値未満|  
|gt|より大きい|  
|le|以下|  
|ge|以上|  
  
 2 つの値では、選択演算子に従って同じ比較と、式は True を返します。 それ以外の場合、False を返します。 いずれかの値が空のシーケンスの場合、式の結果は False になります。  
  
 これらの演算子は、単一のアトミック値でのみ機能します。 つまり、オペランドの 1 つにシーケンスを指定することはできません。  
  
 たとえば、次のクエリを取得\<画像 > 要素、写真のサイズが製品モデルの"小さな。  
  
```  
SELECT CatalogDescription.query('         
              declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";         
              for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]         
              return         
                    $P         
             ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=19         
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `declare namespace` クエリで、後で使用される名前空間プレフィックスを定義します。  
  
-   \<サイズ > 要素の値が、指定したアトミック値"small"と比較されます。  
  
-   値の演算子がアトミック値でのみ動作するため、 **data()** 関数は、ノードの値を取得するが暗黙的に使用します。 つまり、`data($P/PD:Size) eq "small"` も同じ結果になります。  
  
 結果を次に示します。  
  
```  
\<PD:Picture   
  xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  \<PD:Angle>front\</PD:Angle>  
  \<PD:Size>small\</PD:Size>  
  \<PD:ProductPhotoID>31\</PD:ProductPhotoID>  
\</PD:Picture>  
```  
  
 値の比較でのデータ型の上位変換の規則は、一般的な比較でのデータ型の上位変換の規則と同じです。 また、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]一般的な比較の際に使用は、値の比較中に型指定されていない値に対して同じキャストの規則を使用します。 それに対して、XQuery 仕様の規則では、値の比較時に型指定されていない値は xs:string に常にキャストされます。  
  
## <a name="node-comparison-operator"></a>ノードの比較演算子  
 ノードの比較演算子、**は**ノードの種類にのみ適用されます。 結果を返しますでは、オペランドとして渡される 2 つのノードがソース ドキュメント内の同じノードを表すかどうかを示します。 この演算子は、2 つのオペランドが同じノードである場合に True を返します。 それ以外の場合、False を返します。  
  
 次のクエリは、ワーク センター拠点 10 が特定の製品モデルの製造プロセス内の最初であるかどうかをチェックします。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' AS AWMI)  
  
SELECT ProductModelID, Instructions.query('         
    if (  (//AWMI:root/AWMI:Location[@LocationID=10])[1]         
          is          
          (//AWMI:root/AWMI:Location[1])[1] )          
    then         
          <Result>equal</Result>         
    else         
          <Result>Not-equal</Result>         
         ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=7           
```  
  
 結果を次に示します。  
  
```  
ProductModelID       Result          
-------------- --------------------------  
7              <Result>equal</Result>      
```  
  
## <a name="node-order-comparison-operators"></a>ノード順の比較演算子  
 ノード順の比較演算子は、ドキュメント内の位置に基づいて、ノードの組み合わせを比較します。  
  
 ドキュメント順に基づいて、行われる比較を次に示します。  
  
-   `<<` :**オペランド 1**前**オペランド 2**ドキュメント順でします。  
  
-   `>>` :**オペランド 1**に従って**オペランド 2**ドキュメント順でします。  
  
 次のクエリは、製品カタログの説明がある場合に True を返します、\<保証 > 要素の前に、\<メンテナンス > 特定の製品ドキュメントの順序で要素。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM)  
  
SELECT CatalogDescription.value('  
     (/PD:ProductDescription/PD:Features/WM:Warranty)[1] <<   
           (/PD:ProductDescription/PD:Features/WM:Maintenance)[1]', 'nvarchar(10)') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **Value()** のメソッド、 **xml**データ型は、クエリで使用します。  
  
-   クエリのブール型の結果に変換されます**nvarchar (10)** 返されるとします。  
  
-   クエリから True が返されます。  
  
## <a name="see-also"></a>関連項目  
 [システム入力&#40;XQuery&#41;](../xquery/type-system-xquery.md)   
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
