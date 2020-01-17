---
title: REVERSE (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7a0e8974f781f5f69817cf3374416de7bc32580
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71288382"
---
# <a name="reverse-ssis-expression"></a>REVERSE (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  文字式を逆に並べ替えたものを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 逆に並べ替える対象となる文字式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 *character_expression* 引数は、DT_WSTR データ型である必要があります。  
  
 *character_expression* が NULL の場合、REVERSE は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、文字列リテラルを使用します。 返される結果は "ekiB niatnuoM" です。  
  
```  
REVERSE("Mountain Bike")  
```  
  
 この例では、変数を使用します。 **Name** に Touring Bike が含まれる場合、返される結果は "ekiB gniruoT" です。  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
