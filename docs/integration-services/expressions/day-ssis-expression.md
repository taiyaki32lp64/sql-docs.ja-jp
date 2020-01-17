---
title: DAY (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 344e3eca9359d3bafa0dd0fd529c939f84575921
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297617"
---
# <a name="day-ssis-expression"></a>DAY (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ある日付の、日の日付要素を表す整数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>引数  
 *date*  
 有効な日付または日付形式の文字列を返す式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 引数が NULL の場合、DAY は NULL を返します。  
  
 日付リテラルは、日付データ型のいずれかに明示的にキャストされる必要があります。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
> [!NOTE]  
>  日付リテラルが次のいずれかの日付データ型に明示的にキャストされると、式の検証は失敗します。DT_DBTIMESTAMPOFFSET および DT_DBTIMESTAMP2。  
  
 DAY 関数を使用すると、DATEPART("DAY", date) 関数を使用する場合と同じ結果を、より簡単に取得できます。  
  
## <a name="expression-examples"></a>式の例  
 この例は、日付リテラルの日数を返します。 データ形式が "mm/dd/yyyy" 形式の場合、この例は 23 を返します。  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 この例は、 **ModifiedDate** 列内の日を表す整数を返します。  
  
```  
DAY(ModifiedDate)  
```  
  
 この例は、現在の日付の日を表す整数を返します。  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>参照  
 [DATEADD &#40;SSIS 式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 式&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS 式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [MONTH &#40;SSIS 式&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS 式&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
