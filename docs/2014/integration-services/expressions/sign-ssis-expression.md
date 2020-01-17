---
title: SIGN (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b77aaffe4e6f0f0163978ba346abdd31cdc61ce8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62897308"
---
# <a name="sign-ssis-expression"></a>SIGN (SSIS 式)
  数値式の符号として正 (+1)、負 (-1)、0 のいずれかを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 有効な符号付き数値式です。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>コメント  
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
  
## <a name="see-also"></a>関連項目  
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
