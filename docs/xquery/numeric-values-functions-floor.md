---
title: floor 関数 (XQuery) |Microsoft Docs
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
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c27e432dc258b4d2b9d21bfe0ab28df8ee5b510
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946532"
---
# <a name="numeric-values-functions---floor"></a>数値関数 - floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  引数の値より大きくない小数部のないと最大数を返します。 引数が空のシーケンスの場合は、空のシーケンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 関数を適用する番号です。  
  
## <a name="remarks"></a>コメント  
 場合の種類 *$arg*は 3 つの数値基本データ型の 1 つ**xs:float**、 **xs:double**、または**xs:decimal**、戻り値の型は同じですが、 *$arg*型。 場合の種類 *$arg* 、数値型のいずれかから派生した型は、戻り値の型が基本の数値型。  
  
 Fn:floor、fn:ceiling、または fn:round 関数への入力が場合**xdt:untypedAtomic**、型指定されていないデータは、暗黙的にキャストされた**xs:double**します。 その他の型のデータが入力されると、静的エラーが生成されます。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列に、AdventureWorks サンプル データベース。  
  
 作業用サンプルを使用することができます、 [ceiling 関数 (XQuery)](../xquery/numeric-values-functions-ceiling.md)の**floor()** XQuery 関数。 置換を行う必要があるすべてが、 **ceiling()** 関数を使用したクエリで、 **floor()** 関数。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Floor()** 関数では、すべての整数値を xs:decimal にマップします。  
  
## <a name="see-also"></a>関連項目  
 [ceiling 関数&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 関数&#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
