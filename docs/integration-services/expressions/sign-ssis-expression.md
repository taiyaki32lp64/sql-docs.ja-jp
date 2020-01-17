---
title: SIGN (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d98782b0c007f584c5d013c49dafe47a01106a38
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71288632"
---
# <a name="sign-ssis-expression"></a>SIGN (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  数値式の符号として正 (+1)、負 (-1)、0 のいずれかを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 有効な符号付き数値式です。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 引数が NULL の場合、SIGN は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルの符号を返します。 返される結果は -1 です。  
  
```  
SIGN(-123.45)  
```  
  
 この例では、 **StandardCost** 列を **DealerPrice** 列から減算した結果の符号を返します。  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
