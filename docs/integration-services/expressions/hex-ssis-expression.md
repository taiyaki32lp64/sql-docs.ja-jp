---
title: HEX (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- hexadecimal data
- HEX function
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c28f8dbaa649e0755c6f18f7cc0f1485f022e4a6
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71289558"
---
# <a name="hex-ssis-expression"></a>HEX (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  整数の 16 進値を表す文字列を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HEX(integer_expression)  
```  
  
## <a name="arguments"></a>引数  
 *integer_expression*  
 符号付き整数または符号なし整数です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 *integer_expression* が null の場合、HEX は null を返します。  
  
 *integer_expression* 引数は整数に評価される必要があります。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 返される結果には、0x プレフィックスなどの修飾子は含まれません。 プレフィックスを含めるには、+ (連結) 演算子を使用します。 詳細については、「[+ &#40;連結&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)」を参照してください。  
  
 HEX 表記法で使用される A から F の文字は、大文字で表示されます。  
  
 整数データ型の結果の文字列の長さは、次のようになります。  
  
-   DT_I1 および DT_UI1 データ型は、最大長 2 の文字列を返します。  
  
-   DT_I2 および DT_UI2 データ型は、最大長 4 の文字列を返します。  
  
-   DT_I4 および DT_UI4 データ型は、最大長 8 の文字列を返します。  
  
-   DT_I8 および DT_UI8 データ型は、最大長 16 の文字列を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルを使用しています。 この関数は、値 190 を返します。  
  
```  
HEX(400)   
```  
  
 この例では、 **ReorderPoint** 列を使用します。 列のデータ型は **smallint**です。 **ReorderPoint** が 750 の場合、関数は 2EE を返します。  
  
```  
HEX(ReorderPoint)   
```  
  
 この例では、システム変数 **LocaleID**を使用しています。 **LocaleID** が 1033 の場合、関数は 409 を返します。  
  
```  
HEX(@LocaleID)  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
