---
title: max 関数 (XQuery) |Microsoft Docs
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
author: rothja
ms.author: jroth
ms.openlocfilehash: e47539a350a2918ef24c47e3c1eca270d4aeb72e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985955"
---
# <a name="aggregate-functions---max"></a>集計関数 - max
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  アトミック値のシーケンスを返します *$arg*、1 つの項目の値がその他のすべての値より大きい。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 最大値が返されるアトミック値のシーケンス。  
  
## <a name="remarks"></a>コメント  
 すべての種類に渡されるアトミック値の**max()** 同じ基本型のサブタイプにする必要があります。 受け付けられるベースの型をサポートする型では、 **gt**操作。 これらの型には、次の 3 つの組み込み数値基本データ型、日付/時刻の基本型、xs:string、xs:boolean、および xdt:untypedAtomic が含まれます。 Xdt:untypedAtomic 型の値は、xs:double にキャストされます。 これらの型の混在がある場合、またはその他の種類の他の値が渡された場合は、静的エラーが発生します。  
  
 結果**max()** xdt:untypedAtomic の場合は xs:double など、渡された型の基本型を受け取ります。 入力が静的に空の場合、結果が暗黙的し、静的エラーが発生します。  
  
 **Max()** 関数は、入力シーケンス内の他のよりも大きいシーケンスの 1 つの値を返します。 Xs:string 値の場合は、既定の Unicode コード ポイント照合順序が使用されています。 Xdt:untypedAtomic 値は、xs:double にキャストできない場合で、入力シーケンスの値が無視されます。 *$arg*します。 入力が動的に計算された空のシーケンスの場合は、空のシーケンスが返されます。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**内の列を入力、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]データベース。  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. Max() XQuery 関数を使用して、ほとんどの労働時間が製造プロセス内でのワーク センターの場所を検索するには  
 指定したクエリ[min 関数 (XQuery)](../xquery/aggregate-functions-min.md)を使用して書き換えることができます、 **max()** 関数。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Max (** ) 関数では、すべての整数値を xs:decimal にマップします。  
  
-   **Max()** xs:duration 型の値に対して関数がサポートされていません。  
  
-   基本データ型の境界を超えて複数の型が混在するシーケンスはサポートされません。  
  
-   照合順序を指定する構文オプションはサポートされていません。  
  
## <a name="see-also"></a>関連項目  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
