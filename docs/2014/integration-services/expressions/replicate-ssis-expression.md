---
title: REPLICATE (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REPLICATE function
ms.assetid: e7a37b93-6d1d-42d5-9a65-de1790abf6a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 349a100a295ef00b19b2de69214fdd7af8bd2d32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62897351"
---
# <a name="replicate-ssis-expression"></a>REPLICATE (SSIS 式)
  指定された回数だけレプリケートされた文字式を返します。 *times* 引数は整数に評価される必要があります。  
  
> [!NOTE]  
>  REPLICATE 関数では長い文字列が使用される場合が多いため、式の長さに対する 4,000 文字の制限が発生する可能性が高くなります。 式の評価結果が Integration Services データ型の DT_WSTR または DT_STR である場合、式は 4,000 文字に切り捨てられます。 サブ式の結果のデータ型が DT_STR または DT_WSTR である場合、式全体の結果のデータ型に関係なく、そのサブ式も同様に 4,000 文字に切り捨てられます。 切り捨ての結果を効率よく処理できる場合もあれば、結果により警告またはエラーが発生する場合もあります。 詳しくは、「[構文 &#40;SSIS&#41;](syntax-ssis.md)」をご覧ください。  
  
## <a name="syntax"></a>構文  
  
```  
  
REPLICATE(character_expression,times)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 レプリケートする文字式です。  
  
 *times*  
 *character_expression* がレプリケートされる回数を指定する整数式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>コメント  
 *times* が 0 の場合、関数は長さが 0 の文字列を返します。  
  
 *times* が負の値の場合、関数はエラーを返します。  
  
 *times* 引数には、変数や列も使用できます。  
  
 REPLICATE は、DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、REPLICATE による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](cast-ssis-expression.md)」をご覧ください。  
  
 引数のいずれかが NULL の場合、REPLICATE は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、文字列リテラルを 3 回レプリケートします。 返される結果は、"Mountain BikeMountain BikeMountain Bike" です。  
  
```  
REPLICATE("Mountain Bike", 3)  
```  
  
 この例では、 **Name** 列の値を変数 **Times** の値の回数だけレプリケートします。 **Times** が 3、 **Name** が Touring Front Wheel の場合、返される結果は "Touring Front WheelTouring Front WheelTouring Front Wheel" になります。  
  
```  
REPLICATE(Name, @Times)  
```  
  
 この例では、変数 **Name** の値を **Times** 列の値の回数だけレプリケートします。 **Times** の値は整数データ型でなく、式には整数データ型への明示的なキャストが含まれています。 **Name** に Helmet が含まれ、 **Times** が 2 の場合、返される結果は "HelmetHelmet" になります。  
  
```  
REPLICATE(@Name, (DT_I4(Times))  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
