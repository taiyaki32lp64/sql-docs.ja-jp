---
title: () (かっこ) (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 968ab3afbdb5d184364758797180102d65293eb7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71288528"
---
# <a name="-parentheses-ssis-expression"></a>() (かっこ) (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  式の評価順序を特定します。 かっこで囲まれた式は、評価の優先順位が最も高くなります。 かっこで囲まれ、入れ子になっている式は、内側から外側の順に評価されます。  
  
 かっこは、複合式を理解しやすくするためにも使用されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 有効な式を指定します。  
  
## <a name="result-types"></a>戻り値の型  
 *expression*のデータ型。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、かっこを使用して演算子の優先順位を変更する方法を示します。 最初の式は 100 と評価され、2 番目の式は 31 と評価されます。  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>参照  
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
