---
title: 演算子 (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b625b23dc45a3a5ed9abc00f0068ed3e7fbfeb58
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297449"
---
# <a name="operators-ssis-expression"></a>演算子 (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このセクションでは、式の言語が提供する演算子、および式エバリュエーターが使用する演算子の優先順位と結合性について説明します。  
  
 次の表に、演算子に関するこのセクションのトピックの一覧を示します。  
  
|演算子|[説明]|  
|--------------|-----------------|  
|[キャスト (SSIS 式)](../../integration-services/expressions/cast-ssis-expression.md)|式をあるデータ型から別のデータ型に変換します。|  
|[() (括弧) (SSIS 式)](../../integration-services/expressions/parentheses-ssis-expression.md)|式の評価順序を特定します。|  
|[+ (加算) (SSIS)](../../integration-services/expressions/add-ssis.md)|2 つの数値式を加算します。|  
|[+ (連結) (SSIS 式)](../../integration-services/expressions/concatenate-ssis-expression.md)|2 つの式を連結します。|  
|[- (減算) (SSIS 式)](../../integration-services/expressions/subtract-ssis-expression.md)|最初の数値式から 2 番目の数値式を減算します。|  
|[- (否定) (SSIS 式)](../../integration-services/expressions/negate-ssis-expression.md)|数値式を負数化します。|  
|[* (乗算) (SSIS 式)](../../integration-services/expressions/multiply-ssis-expression.md)|2 つの数値式を乗算します。|  
|[/ (除算) &#40;SSIS 式&#41;](../../integration-services/expressions/divide-ssis-expression.md)|最初の数値式を 2 番目の数値式で除算します。|  
|[% &#40;剰余&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/modulo-ssis-expression.md)|最初の数値式を 2 番目の数値式で割った剰余を整数値で返します。|  
|[&#124;&#124; (論理 OR) (SSIS 式)](../../integration-services/expressions/logical-or-ssis-expression.md)|論理 OR 演算を実行します。|  
|[&& (論理 AND) (SSIS 式)](../../integration-services/expressions/logical-and-ssis-expression.md)|論理 AND 演算を実行します。|  
|[\! &#40;論理 NOT&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/logical-not-ssis-expression.md)|ブール型のオペランドを否定します。|  
|[&#124; (ビット演算子包括的 OR) (SSIS 式)](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)|2 つの整数値の OR 演算をビット単位で実行します。|  
|[^ (ビット演算子排他的 OR) (SSIS 式)](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)|2 つの整数値の排他的 OR 演算をビット単位で実行します。|  
|[& (ビット演算子 AND) (SSIS 式)](../../integration-services/expressions/bitwise-and-ssis-expression.md)|2 つの整数値の AND 演算をビット単位で実行します。|  
|[~ &#40;ビット演算子 NOT&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/bitwise-not-ssis-expression.md)|整数の否定のビット演算を実行します。|  
|[== (等しい) (SSIS 式)](../../integration-services/expressions/equal-ssis-expression.md)|2 つの式が等しいかどうかを判別するための比較を実行します。|  
|[\!= &#40;等しくない&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/unequal-ssis-expression.md)|2 つの式が等しくないかどうかを判別するための比較を実行します。|  
|[> (より大きい) (SSIS 式)](../../integration-services/expressions/greater-than-ssis-expression.md)|最初の式が 2 番目の式より大きいかどうかを判別するための比較を実行します。|  
|[&#60; (より小さい) (SSIS 式)](../../integration-services/expressions/less-than-ssis-expression.md)|最初の式が 2 番目の式未満かどうかを判別するための比較を実行します。|  
|[&#62;= (以上) (SSIS 式)](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)|最初の式が 2 番目の式以上かどうかを判別するための比較を実行します。|  
|[&#60;= (以下) (SSIS 式)](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)|最初の式が 2 番目の式以下かどうかを判別するための比較を実行します。|  
|[? : &#40;条件&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/conditional-ssis-expression.md)|ブール式の評価に基づいて 2 つの式のうちのいずれかの式を返します。|  
  
 優先順位の階層内における各演算子の配置の詳細については、「 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)   
 [Integration Services 式の詳細の例](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services &#40;SSIS&#41; 式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
