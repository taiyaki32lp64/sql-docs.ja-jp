---
title: RIGHT (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RIGHT function
ms.assetid: 83e70e75-4be5-4783-a8cf-032f82afe16e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1dcd15de93893b34a6842110767b2242fbc3a146
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297406"
---
# <a name="right-ssis-expression"></a>RIGHT (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  指定された文字式の一番右の部分から指定された数の文字を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RIGHT(character_expression,integer_expression)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 文字の抽出元となる文字式です。  
  
 *integer_expression*  
 返す文字の数を示す整数式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 *integer_expression* が *character_expression*より長い場合、関数は *character_expression*を返します。  
  
 *integer_expression* が 0 の場合、関数は長さが 0 の文字列を返します。  
  
 *integer_expression* が負の値の場合、関数はエラーを返します。  
  
 *integer_expression* 引数には、変数および列を使用できます。  
  
 RIGHT は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、RIGHT による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
 引数のいずれかが NULL の場合、RIGHT は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、文字列リテラルを使用します。 返される結果は `"Bike"`です。  
  
```  
RIGHT("Mountain Bike", 4)  
```  
  
 次の例では、 `Times` 列の右端からの文字が、 `Name` 変数で指定した文字数分返されます。 `Name` が `Touring Front Wheel` で `Times` が 5 の場合、返される結果は `"Wheel"`です。  
  
```  
RIGHT(Name, @Times)  
```  
  
 次の例でも、 `Times` 列の右端からの文字が、 `Name` 変数で指定した文字数分返されます。 `Times` の値は整数データ型でなく、式には DT_I2 データ型への明示的なキャストが含まれています。 `Name` が `Touring Front Wheel` で `Times` が `4.32`の場合、返される結果は `"heel"` です。これは、RIGHT 関数が値 4.32 を 4 に変換し、右端の 4 文字を返すためです。  
  
```  
RIGHT(Name, (DT_I2)@Times))  
```  
  
## <a name="see-also"></a>参照  
 [LEFT &#40;SSIS 式&#41;](../../integration-services/expressions/left-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
