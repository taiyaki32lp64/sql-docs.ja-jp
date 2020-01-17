---
title: YEAR (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4e677a4a0c36f52ae62dfc06cd597ad5401fc8e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768698"
---
# <a name="year-ssis-expression"></a>YEAR (SSIS 式)
  ある日付の、年の日付要素を表す整数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>引数  
 *date*  
 任意の日付形式の日付です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>コメント  
 引数が NULL の場合、YEAR は NULL を返します。  
  
 日付リテラルは、日付データ型のいずれかに明示的にキャストされる必要があります。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
> [!NOTE]  
>  日付リテラルが次のいずれかの日付データ型に明示的にキャストされると、式の検証は失敗します。DT_DBTIMESTAMPOFFSET および DT_DBTIMESTAMP2。  
  
 YEAR 関数を使用すると、DATEPART("Year", date) 関数を使用する場合と同じ結果を、より簡単に取得できます。  
  
## <a name="expression-examples"></a>式の例  
 この例では、日付リテラルの年を表す数値が返されます。 データが mm/dd/yyyy 形式の場合、この例では "2002" が返されます。  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 この例では、 **ModifiedDate** 列内の年を表す整数が返されます。  
  
```  
YEAR(ModifiedDate)  
```  
  
 この例では、現在の日付の年を表す整数が返されます。  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>参照  
 [DATEADD &#40;SSIS 式&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 式&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS 式&#41;](datepart-ssis-expression.md)   
 [DAY &#40;SSIS 式&#41;](day-ssis-expression.md)   
 [MONTH &#40;SSIS 式&#41;](month-ssis-expression.md)   
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
