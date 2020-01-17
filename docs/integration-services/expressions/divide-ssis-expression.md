---
title: 除算 (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7341a6dad3633b95882ba1b06e5f27e8c7af50db
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71289924"
---
# <a name="divide-ssis-expression"></a>除算 (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  最初の数値式を 2 番目の数値式で除算します。  
  
## <a name="syntax"></a>構文  
  
```  
  
dividend / divisor  
  
```  
  
## <a name="arguments"></a>引数  
 *dividend*  
 除算される数値式です。 *dividend* には、有効な任意の数値式を指定できます。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 *divisor*  
 被除数を除算する数値式です。 *divisor* には、0 以外の有効な任意の数値式を指定できます。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳しくは、「 [式における Integration Services データ型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 オペランドのいずれかが NULL の場合、結果は NULL になります。  
  
 0 による除算は無効です。 *divisor* サブ式の評価方法に応じて、次のいずれかのエラーが発生します。  
  
-   0 に評価される *divisor* サブ式が定数の場合、デザイン時にエラーが表示され、式は検証に失敗します。  
  
-   0 に評価される *divisor* サブ式に、変数は含まれるが入力列は含まれない場合、式が属するコンポーネントは、パッケージの実行前に行われる事前検証に失敗します。  
  
-   0 に評価される *divisor* サブ式に入力列が含まれる場合、実行時にエラーが表示され、データ フロー コンポーネントのエラー フロー規則に応じて処理されます。  
  
## <a name="expression-examples"></a>式の例  
 この例では、2 つの数値リテラルを除算します。  
  
```  
25 / 5  
```  
  
 この例では、 **ListPrice** 列の値を **StandardCost** 列の値で除算します。  
  
```  
ListPrice / StandardCost  
```  
  
## <a name="see-also"></a>参照  
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
