---
title: 記述子の遷移 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44e9d92c7371451d6bfdd2e1513c3f8fdac8447b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130000"
---
# <a name="descriptor-transitions"></a>記述子の遷移
ODBC 記述子では、次の 3 つの状態があります。  
  
|状態|説明|  
|-----------|-----------------|  
|D0|未割り当ての記述子|  
|D1i|暗黙的に割り当てられた記述子|  
|D1e|明示的に割り当てられた記述子|  
  
 次の表では、各 ODBC 関数が、記述子の状態にどのように影響する方法を示します。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 未割り当て|D1i<br /><br /> 暗黙的|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|D1i[1]|--|--|  
|D1e [2]|--|--|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_stmt としてでした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* SQL_HANDLE_DESC でした。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 未割り当て|D1i<br /><br /> 暗黙的|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(組み込み)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 未割り当て|D1i<br /><br /> 暗黙的|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(組み込み)[2]|(HY017)|D0|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_stmt としてでした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* SQL_HANDLE_DESC でした。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField および SQLGetDescRec  
  
|D0<br /><br /> 未割り当て|D1i<br /><br /> 暗黙的|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(組み込み)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField および SQLSetDescRec  
  
|D0<br /><br /> 未割り当て|D1i<br /><br /> 暗黙的|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(組み込み)[1]|--|--|  
  
 [1] この行は、移行を示していますときに*DescriptorHandle*が ARD、APD、または、IPD のハンドルまたは (の**SQLSetDescField**) と*DescriptorHandle* 、IRD のハンドルが。*FieldIdentifier* SQL_DESC_ARRAY_STATUS_PTR または SQL_DESC_ROWS_PROCESSED_PTR でした。  
  
## <a name="all-other-odbc-functions"></a>他のすべての ODBC 関数  
  
|D0<br /><br /> 未割り当て|D1i<br /><br /> 暗黙的|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--|--|--|
