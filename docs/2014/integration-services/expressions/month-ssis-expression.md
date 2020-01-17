---
title: MONTH (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f5e997f40f5af0a9f1c5cd0de4114714a1db8b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62897529"
---
# <a name="month-ssis-expression"></a>MONTH (SSIS 式)
  ある日付の、月の日付要素を表す整数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>引数  
 *date*  
 任意の日付形式の日付です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>コメント  
 引数が NULL の場合、MONTH は NULL を返します。  
  
 日付リテラルは、日付データ型のいずれかに明示的にキャストされる必要があります。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
> [!NOTE]  
>  日付リテラルが次のいずれかの日付データ型に明示的にキャストされると、式の検証は失敗します。DT_DBTIMESTAMPOFFSET および DT_DBTIMESTAMP2。  
  
 MONTH 関数を使用すると、DATEPART("MONTH", date) 関数を使用する場合と同じ結果を、より簡単に取得できます。  
  
## <a name="expression-examples"></a>式の例  
 この例では、日付リテラルの月を表す数値が返されます。 データが "mm/dd/yyyy" 形式の場合、この例では 11 が返されます。  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 この例では、 **ModifiedDate** 列内の月を表す整数が返されます。  
  
```  
MONTH(ModifiedDate)  
```  
  
 この例では、現在の日付の月を表す整数が返されます。  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>参照  
 [DATEADD &#40;SSIS 式&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 式&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS 式&#41;](datepart-ssis-expression.md)   
 [DAY &#40;SSIS 式&#41;](day-ssis-expression.md)   
 [YEAR &#40;SSIS 式&#41;](year-ssis-expression.md)   
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
