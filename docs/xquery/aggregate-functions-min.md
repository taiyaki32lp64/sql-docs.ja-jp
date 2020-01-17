---
title: min 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
author: rothja
ms.author: jroth
ms.openlocfilehash: 29e5718debadb4725bc9d9ebcd499c261ed23d54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985752"
---
# <a name="aggregate-functions---min"></a>集計関数 - min
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  アトミック値のシーケンスを返します *$arg*値が小さいよりも、他のすべての項目を 1 つ。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 最小値を取得する項目のシーケンス。  
  
## <a name="remarks"></a>コメント  
 すべての種類に渡されるアトミック値の**min()** 同じ基本型のサブタイプにする必要があります。 受け付けられるベースの型をサポートする型では、 **gt**操作。 これらの型には、次の 3 つの組み込み数値基本データ型、日付/時刻の基本型、xs:string、xs:boolean、および xdt:untypedAtomic が含まれます。 Xdt:untypedAtomic 型の値は、xs:double にキャストされます。 これらの型の混在がある場合、またはその他の種類の他の値が渡された場合は、静的エラーが発生します。  
  
 結果**min()** xdt:untypedAtomic の場合は xs:double など、渡された型の基本型を受け取ります。 入力が静的に空の場合、結果が暗黙的し、静的エラーが返されます。  
  
 **Min()** 関数は、入力シーケンス内の他のよりも小さいをシーケンスの 1 つの値を返します。 Xs:string 値の場合は、既定の Unicode コード ポイント照合順序が使用されています。 Xdt:untypedAtomic 値は、xs:double にキャストできない場合で、入力シーケンスの値が無視されます。 *$arg*します。 入力が動的に計算された空のシーケンスの場合は、空のシーケンスが返されます。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. min() XQuery 関数を使用した、労働時間が最も短いワーク センター拠点の検索  
 次のクエリは、製品モデルの製造プロセス内のすべての作業・ センターの場所を取得 (ProductModelID = 7) 最小限の労働時間があります。 通常、次に示すように 1 つの拠点が返されます。 複数の場所の最小の労働時間数が等しい場合は、それらがすべて返されます。  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **名前空間**XQuery プロローグ内のキーワード名前空間プレフィックスを定義します。 このプレフィックスは、XQuery の本文で使用されます。  
  
 XQuery の本文を持つ XML の構築、\<場所 > WCID を持つ要素と**LaborHrs**属性。  
  
-   クエリではまた、ProductModelID を取得し、名前の値。  
  
 結果を次に示します。  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Min()** 関数では、すべての整数値を xs:decimal にマップします。  
  
-   **Min()** xs:duration 型の値に対して関数がサポートされていません。  
  
-   基本データ型の境界を超えて複数の型が混在するシーケンスはサポートされません。  
  
-   照合順序を指定する構文オプションはサポートされていません。  
  
## <a name="see-also"></a>関連項目  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
