---
title: '- (減算) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e26df3ba35f81fb386cd208e8df207360510254c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297380"
---
# <a name="--subtract-ssis-expression"></a>- (減算) (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  最初の数値式から 2 番目の数値式を減算します。  
  
## <a name="syntax"></a>構文  
  
```  
  
numeric_expression1 - numeric_expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression1、numeric_expression2*  
 数値データ型の有効な式です。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳しくは、「 [式における Integration Services データ型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 式が正しい順序で評価されるようにするために、マイナス単項式はかっこで囲みます。  
  
## <a name="remarks"></a>Remarks  
 オペランドのいずれかが NULL の場合、結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルを減算します。  
  
```  
5 - 6.09  
```  
  
 この例では、 **ListPrice** 列の値から **StandardCost** 列の値を減算します。  
  
```  
ListPrice - StandardCost  
```  
  
 この例では、計算した値を **ListPrice** 列から減算します。 変数 **Discount%** は、名前に % 文字が含まれているため、角かっこで囲む必要があります。 詳細については、「[識別子 &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)」を参照してください。  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>参照  
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
