---
title: アトミック化 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
author: rothja
ms.author: jroth
ms.openlocfilehash: e034e6464e395c1516eed874ed1c0cff2c32238f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985707"
---
# <a name="atomization-xquery"></a>アトミック化 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アトミック化とは、アイテムの型指定された値を抽出するプロセスです。 このプロセスが特定の状況で暗黙的に指定します。 算術演算子や比較演算子などの一部の XQuery 演算子は、このプロセスに依存します。 たとえば、ノードに直接算術演算子を適用すると、ノードの型指定された値が最初に取得暗黙的に呼び出すことによって、[データ関数](../xquery/data-accessor-functions-data-xquery.md)します。 算術演算子、オペランドとして、アトミック値を渡します。  
  
 たとえば、次のクエリは LaborHours 属性の合計を返します。 この場合、 **data()** が属性ノードに暗黙的に適用します。  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 明示的に指定できますが、必須ではありません、 **data()** 関数。  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 暗黙のアトミック化の別の例では、算術演算子を使用する場合です。 **+** 演算子はアトミック値を必要と**data()** LaborHours 属性のアトミック値を取得するが暗黙的に適用します。 クエリがの Instructions 列に対して指定された、 **xml** ProductModel テーブルの型。 次のクエリでは、3 回 LaborHours 属性を返します。 クエリでは、次に注意してください。  
  
-   OrignialLaborHours 属性の構築では、(`$WC/@LaborHours`) によって返される単一シーケンスにアトミック化が暗黙的に適用されます。 LaborHours 属性の型指定された値が、OrignialLaborHours に代入されます。  
  
-   UpdatedLaborHoursV1 属性の構築では、算術演算子がアトミック値を必要とします。 そのため、 **data()** によって返される LaborHours 属性に暗黙的に適用されます (`$WC/@LaborHours`)。 アトミック値 1 は、これには追加されます。 UpdatedLaborHoursV2 属性の構築の明示的な適用を示しています。 **data()** 、がは必要ありません。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 結果を次に示します。  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 単純型、空のセット、または静的な型エラーのインスタンスで、アトミック化が発生します。  
  
 アトミック化は、関数、関数によって返される値に渡される比較式のパラメーターにも発生**cast()** 式、および by 句の順序で渡される順序式。  
  
## <a name="see-also"></a>関連項目  
 [XQuery の基礎](../xquery/xquery-basics.md)   
 [比較式&#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)   
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
