---
title: SQRT (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a13d07fe353c4d10345cce609f4b82cd7019db6c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297394"
---
# <a name="sqrt-ssis-expression"></a>SQRT (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  数値式の平方根を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 任意の数値データ型の数値式です。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 引数が NULL の場合、SQRT 関数は NULL を返します。  
  
 引数が負の値の場合、SQRT 関数の処理は失敗します。  
  
 平方根演算の前に、引数は DT_R8 データ型にキャストされます。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルの平方根が返されます。 返される結果は 12 です。  
  
```  
SQRT(144)  
```  
  
 この例では、式の平方根、つまり、 **Value1** 列の値から **Value2** 列の値を減算した結果の値の平方根が返されます。  
  
```  
SQRT(Value1 - Value2)  
```  
  
 この例では、SQUARE 関数を 2 つの変数に適用して、その合計の平方根を計算することにより、直角三角形の 3 番目の辺の長さが返されます。 **Side1** の値が 3、 **Side2** の値が 4 の場合、SQRT 関数は 5 を返します。  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  式に含まれる変数名には、常にプレフィックス \@ を付けます。  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
