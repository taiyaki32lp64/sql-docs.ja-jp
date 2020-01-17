---
title: SUBSTRING (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SUBSTRING function
- part of expression returned [Integration Services]
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2b749a88a0783e6981cf9fd643412f0ca614e6a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768735"
---
# <a name="substring-ssis-expression"></a>SUBSTRING (SSIS 式)
  指定された位置で始まり、かつ指定された長さを持つ文字式の一部を返します。 *position* パラメーターと *length* パラメーターは整数に評価される必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
SUBSTRING(character_expression, position, length)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 文字の抽出元となる文字式です。  
  
 *position*  
 部分文字列が始まる位置を指定する整数です。  
  
 *length*  
 部分文字列の長さを文字数として指定する整数です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>コメント  
 SUBSTRING は 1 から始まるインデックスを使用します。 *position* が 1 の場合、部分文字列は *character_expression*の最初の文字から始まります。  
  
 SUBSTRING は DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、SUBSTRING による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](cast-ssis-expression.md)」をご覧ください。  
  
 引数が NULL の場合、SUBSTRING は NULL を返します。  
  
 式のすべての引数で、変数および列を使用できます。  
  
 *length* 引数が文字列の長さを超える場合、 この関数は残りの文字列を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、文字列リテラルの 4 文字目から始まる 2 文字が返されます。 返される結果は "ph" です。  
  
```  
SUBSTRING("elephant",4,2)  
```  
  
 この例では、4 文字目から始まる文字列リテラルの残りの部分が返されます。 返される結果は "phant" です。 *length* 引数が文字列の長さを超えても、エラーにはなりません。  
  
```  
SUBSTRING ("elephant",4,50)  
```  
  
 この例では、 **MiddleName** 列の最初の文字が返されます。  
  
```  
SUBSTRING(MiddleName,1,1)  
```  
  
 この例では、 *position* 引数と *length* 引数に変数を使用します。 **Start** が 1 で **Length** が 5 の場合、関数は **Name** 列の最初の 5 文字を返します。  
  
```  
SUBSTRING(Name,@Start,@Length)  
```  
  
 この例では、 **PostalCode** 変数の 6 文字目から始まる、最後の 4 文字が返されます。  
  
```  
SUBSTRING (@PostalCode,6,4)  
```  
  
 この例では、文字列リテラルから長さ 0 の文字列が返されます。  
  
```  
SUBSTRING ("Redmond",4,0)  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
