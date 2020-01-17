---
title: round 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
author: rothja
ms.author: jroth
ms.openlocfilehash: 1927d6e483683699196cfc7e87928f27bf23446a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946545"
---
# <a name="numeric-values-functions---round"></a>数値関数 - round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  引数に最も近く、小数部分を持たない数値を返します。 そのような複数の番号がある、正の無限大に最も近いものが返されます。 以下に例を示します。  
  
 引数が 2.5 の場合**round()** 3 が返されます。  
  
 引数がある場合、2.4999 場合**round()** 2 を返します。  
  
 場合は、引数が-2.5、 **round()** -2 を返します。  
  
 引数が空のシーケンスの場合**round()** 空のシーケンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 関数を適用する番号です。  
  
## <a name="remarks"></a>コメント  
 場合の種類 *$arg*は 3 つの数値基本データ型の 1 つ**xs:float**、 **xs:double**、または**xs:decimal**、戻り値の型は同じですが、 *$arg*型。 場合の種類 *$arg* 、数値型のいずれかから派生した型は、戻り値の型が基本の数値型。  
  
 場合への入力、 **fn:floor**、 **fn:ceiling**、または**fn:round**関数は**xdt:untypedAtomic**、型指定されていないデータは、暗黙的にキャストされます**xs:double**します。  
  
 その他の型のデータが入力されると、静的エラーが生成されます。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
 作業用サンプルを使用することができます、 [ceiling 関数 (XQuery)](../xquery/numeric-values-functions-ceiling.md)の**round()** XQuery 関数。 置換を行う必要があるすべてが、 **ceiling()** 関数を使用したクエリで、 **round()** 関数。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Round()** 関数では、整数値を xs:decimal にマップします。  
  
-   **Round()** 0.5e0 と 0e0 間 xs:double および xs:float 値の関数ではなく - 0e0 0e0 にマップされます。  
  
## <a name="see-also"></a>関連項目  
 [floor 関数&#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [ceiling 関数&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
