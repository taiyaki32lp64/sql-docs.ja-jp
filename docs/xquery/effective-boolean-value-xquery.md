---
title: 有効なブール値 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 4eb94e51896e08f60389edde0c2a6cd0461e8538
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929958"
---
# <a name="effective-boolean-value-xquery"></a>有効なブール値 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  有効なブール値を次に示します。  
  
-   オペランドが空のシーケンスまたはブール値 false の場合は false。  
  
-   それ以外の場合、値は true です。  
  
 単一のブール値、ノード シーケンス、または空のシーケンスを返す式では、有効なブール値を計算できます。 ブール値が次の種類の式が処理されるときに暗黙的に計算されることに注意してください。  
  
-   論理式  
  
-   [機能しません。](../xquery/functions-on-boolean-values-not-function.md)  
  
-   FLWOR 式の WHERE 句  
  
-   [条件式](../xquery/conditional-expressions-xquery.md)  
  
-   [QuantifiedeExpressions](../xquery/quantified-expressions-xquery.md)  
  
 次に、有効なブール値の例を示します。 ときに、**場合**式が処理される場合、条件の有効なブール値が決定されます。 `/a[1]`が空のシーケンスを返す有効なブール値は false。 結果は、1 つのテキスト ノード (false) を XML として返されます。  
  
```  
value is false  
DECLARE @x XML  
SET @x = '<b/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 次の例では、式が空ではないシーケンスを返すので、有効なブール値は true になります。  
  
```  
DECLARE @x XML  
SET @x = '<a/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 ときに型指定されたクエリを実行する**xml**列または変数、ブール型のノードを持つことができます。 **Data()** ここではブール値を返します。 クエリ式がブール値 true を返す場合、次の例で示すように、有効なブール値は true になります。 この例では、次のことも示しています。  
  
-   XML スキーマ コレクションが作成されます。 要素\<b > コレクションでのブール型です。  
  
-   型指定された**xml**変数が作成され、クエリを実行します。  
  
-   式`data(/b[1])`ブール値 true を返します。 そのため、有効なブール値でこの場合は true です。  
  
-   式`data(/b[2])`ブール値 false を返します。 したがって、この場合の有効なブール値は false になります。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="s" type="string"/>  
      <element name="b" type="boolean"/>  
</schema>'  
go  
DECLARE @x XML(SC)  
SET @x = '<b>true</b><b>false</b>'  
SELECT @x.query('if (data(/b[1])) then "true" else "false"')  
SELECT @x.query('if (data(/b[2])) then "true" else "false"')  
go  
```  
  
## <a name="see-also"></a>関連項目  
 [XQuery の基礎](../xquery/xquery-basics.md)   
 [FLWOR ステートメントおよびイテレーション&#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
