---
title: POWER (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- POWER function
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 818f99100150c366c3caf982555f802b2ca6fc68
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297437"
---
# <a name="power-ssis-expression"></a>POWER (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  指定された数値式の結果をべき乗値で返します。 power パラメーターは整数に評価される必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 有効な数値式です。  
  
 *power*  
 有効な数値式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 *numeric_expression* 引数と *power* 引数は、べき乗値の計算前に DT_R8 データ型にキャストされます。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 *numeric_expression* が 0 に評価され、 *power* が負の値の場合、式エバリュエーターはエラーを返し、返される結果を NULL に設定します。  
  
 *numeric_expression* または *power* の結果が不確定に評価される場合、返される結果は NULL になります。  
  
 *power* 引数には小数を使用できます。 たとえば、power 引数として値 0.5 を使用できます。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルを使用しています。 関数は、4 を 3 乗して 64 を返します。  
  
```  
POWER(4,3)  
```  
  
 この例では、 **Length** 列と **DimensionCount** 変数を使用します。 **Length** が 8、 **DimensionCount** が 2 の場合、返される結果は 64 になります。  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
