---
title: DATEPART (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 22225f9a1791185ed78dfc75d92c3dbced7be3ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769339"
---
# <a name="datepart-ssis-expression"></a>DATEPART (SSIS 式)
  ある日付の、特定の日付要素を整数で返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DATEPART(datepart, date)  
```  
  
## <a name="arguments"></a>引数  
 *datepart*  
 新しい値を返す日付の要素を指定するパラメーターです。  
  
 *date*  
 有効な日付または日付形式の文字列を返す式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>コメント  
 引数が NULL の場合、DATEPART は NULL を返します。  
  
 日付リテラルは、日付データ型のいずれかに明示的にキャストされる必要があります。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
 次の表に、式エバリュエーターで認識される日付要素 (datepart) と省略形を示します。 日付要素の名前では大文字と小文字が区別されません。  
  
|datepart|省略形|  
|--------------|-------------------|  
|年|yy、yyyy|  
|Quarter|qq、q|  
|Month|mm、m|  
|Dayofyear|dy、y|  
|日|dd、d|  
|Week|wk、ww|  
|曜日|dw|  
|Hour|Hh|  
|Minute|mi、n|  
|第 2 週|ss、s|  
|Millisecond|Ms|  
  
## <a name="ssis-expression-examples"></a>SSIS 式の例  
 この例では、日付リテラル内の月を表す整数が返されます。 データが mm/dd/yyyy 形式の場合、この例では 11 が返されます。  
  
```  
DATEPART("month", (DT_DBTIMESTAMP)"11/04/2002")  
```  
  
 この例は、 **ModifiedDate** 列内の日を表す整数を返します。  
  
```  
DATEPART("dd", ModifiedDate)  
```  
  
 この例では、現在の日付の年を表す整数が返されます。  
  
```  
DATEPART("yy",GETDATE())  
```  
  
## <a name="see-also"></a>参照  
 [DATEADD &#40;SSIS 式&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF (SSIS 式)](datediff-ssis-expression.md)   
 [DAY (SSIS 式)](day-ssis-expression.md)   
 [MONTH &#40;SSIS 式&#41;](month-ssis-expression.md)   
 [YEAR &#40;SSIS 式&#41;](year-ssis-expression.md)   
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
