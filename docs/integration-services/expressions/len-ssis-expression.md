---
title: LEN (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f84bb32435afe7cbe52cea6ed25f59940dbd42c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297527"
---
# <a name="len-ssis-expression"></a>LEN (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  文字式の文字数を返します。 文字列の先頭および末尾に空白が含まれる場合、この関数は、それらの空白をカウントに含めます。 1 バイト文字の文字列と 2 バイト文字の文字列が同一の場合、LEN 関数は同一の値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 評価の対象となる式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 *character_expression* 引数には、DT_WSTR、DT_TEXT、DT_NTEXT、または DT_IMAGE データ型を使用できます。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 *character_expression* が DT_STR データ型の文字列リテラルまたはデータ列である場合は、LEN による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳細については、「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
 DT_TEXT、DT_NTEXT、DT_IMAGE などのバイナリ ラージ オブジェクト (BLOB) データ型に引数が渡された場合、LEN 関数はバイト カウントを返します。  
  
 引数が NULL の場合、LEN は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例は、文字列リテラルの長さを返します。 返される結果は 12 です。  
  
```  
LEN("Ball Bearing")  
```  
  
 この例は、 **FirstName** と **LastName** 列の値の長さの差を返します。  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 システム変数 **MachineName**を使用して、コンピューター名の長さを返します。  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
