---
title: UPPER (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e5a444d6dea225f37b8640fd642d91ae83618d5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297334"
---
# <a name="upper-ssis-expression"></a>UPPER (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  小文字が大文字に変換された状態の文字式を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 大文字に変換する対象となる文字式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 UPPER は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、UPPER による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
 引数が NULL の場合、UPPER は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、文字列リテラルを大文字に変換します。 返される結果は "HELLO" です。  
  
```  
UPPER("hello")  
```  
  
 この例では、 **FirstName** 列の最初の文字を大文字に変換します。 **FirstName** が anna の場合、返される結果は "A" です。 詳細については、「[SUBSTRING &#40;SSIS 式&#41;](../../integration-services/expressions/substring-ssis-expression.md)」を参照してください。  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 この例では、**PostalCode** 変数の値を大文字に変換します。 **PostalCode** が k4b1s2 の場合、返される結果は "K4B1S2" です。  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>参照  
 [LOWER &#40;SSIS 式&#41;](../../integration-services/expressions/lower-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
