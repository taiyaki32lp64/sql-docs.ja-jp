---
title: SUBSTRING (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SUBSTRING function
- part of expression returned [Integration Services]
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6bb017bdd22b98c255f5b40b680f9e7aa5ef31f5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71288265"
---
# <a name="substring-ssis-expression"></a>SUBSTRING (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>Remarks  
 SUBSTRING は 1 から始まるインデックスを使用します。 *position* が 1 の場合、部分文字列は *character_expression*の最初の文字から始まります。  
  
 SUBSTRING は DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、SUBSTRING による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
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
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
