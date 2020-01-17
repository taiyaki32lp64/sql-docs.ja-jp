---
title: FLOOR (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- largest integer less than or equal to expression
- FLOOR function [SSIS]
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 56f69743e8bbfb8290e492613daeb07885f5ed7d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71289622"
---
# <a name="floor-ssis-expression"></a>FLOOR (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  数値式以下で最大の整数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 有効な数値式です。  
  
## <a name="result-types"></a>戻り値の型  
 引数の式の数値データ型です。 結果は、 *numeric_expression*と同じデータ型の、計算値の整数部分になります。  
  
## <a name="remarks"></a>Remarks  
 引数が NULL の場合、FLOOR は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、正の値、負の値、および 0 に FLOOR 関数を適用します。  
  
```  
FLOOR(123.45)  
```  
  
 123.00 を返します  
  
```  
FLOOR(-123.45)  
```  
  
 -124.00 を返します  
  
```  
FLOOR(0.00)  
```  
  
 0\.00 を返します。  
  
## <a name="see-also"></a>参照  
 [CEILING (SSIS 式)](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
