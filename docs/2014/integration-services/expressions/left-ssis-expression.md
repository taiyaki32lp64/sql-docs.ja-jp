---
title: LEFT (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e6deba09d2804903e8353d4648a2775d18c8c392
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62897690"
---
# <a name="left-ssis-expression"></a>LEFT (SSIS 式)
  指定された文字式の一番左の部分から指定された数の文字を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LEFT(character_expression,number)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 文字の抽出元となる文字式です。  
  
 *number*  
 返す文字の数を示す整数式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>コメント  
 *number* が *character_expression*より長い場合、関数は *character_expression*を返します。  
  
 *number* が 0 の場合、関数は長さが 0 の文字列を返します。  
  
 *number* が負の値の場合、関数はエラーを返します。  
  
 *number* 引数には、変数および列を使用できます。  
  
 LEFT は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、LEFT による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳細については、「[Integration Services のデータ型](../data-flow/integration-services-data-types.md)」 および「[Cast (SSIS 式)](cast-ssis-expression.md)」 を参照してください。  
  
 引数のいずれかが NULL の場合、LEFT は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、文字列リテラルを使用します。 返される結果は `"Mountain"`です。  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>関連項目  
 [RIGHT (SSIS 式)](right-ssis-expression.md)   
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
