---
title: NULL (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- NULL function
- null values [Integration Services]
ms.assetid: df144237-3fbb-41ac-8624-efd92b6522b9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4a796b0ab746468ffef3cab5b3480e73b4cf637
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768828"
---
# <a name="null-ssis-expression"></a>NULL (SSIS 式)
  要求されたデータ型の NULL 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
NULL(typespec)  
```  
  
## <a name="arguments"></a>引数  
 *typespec*  
 有効なデータ型です。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 NULL 値である任意の有効なデータ型です。  
  
## <a name="remarks"></a>コメント  
 引数が NULL の場合、NULL 関数は NULL を返します。  
  
 一部のデータ型の NULL 値を要求する場合は、パラメーターが必要となります。 次の表に、パラメーターが必要なデータ型とそのパラメーターの一覧を示します。  
  
|データ型|パラメーター|例|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) は、1252 コード ページを使用して、30 文字を DT_STR データ型にキャストします。|  
|DT_WSTR|*charcount*|(DT_WSTR,20) は、20 文字を DT_WSTR データ型にキャストします。|  
|DT_BYTES|*bytecount*|(DT_BYTES,50) は、50 バイトを DT_BYTES データ型にキャストします。|  
|DT_DECIMAL|*scale*|(DT_DECIMAL,2) は、数値を小数点以下 2 桁の DT_DECIMAL データ型にキャストします。|  
|DT_NUMERIC|*有効桁数 (precision)*<br /><br /> *scale*|(DT_NUMERIC,10,3) は、数値を有効桁数 10 桁で小数点以下 3 桁の DT_NUMERIC データ型にキャストします。|  
|DT_TEXT|*codepage*|(DT_TEXT,1252) は、1252 コード ページを使用して、値を DT_TEXT データ型にキャストします。|  
  
## <a name="expression-examples"></a>式の例  
 これらの例は、DT_STR、DT_DATE、DT_BOOL データ型の NULL 値を返します。  
  
```  
NULL(DT_STR,10,1252)  
NULL(DT_DATE)  
NULL(DT_BOOL)  
```  
  
## <a name="see-also"></a>参照  
 [ISNULL &#40;SSIS 式&#41;](null-ssis-expression.md)   
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
