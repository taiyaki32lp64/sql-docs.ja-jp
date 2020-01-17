---
title: SQLBindParam のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ecec6116ee16f4affa615518a690d2c665648464
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091246"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam のマッピング
**SQLBindParam**は本当に呼び出せません非推奨れていないため、あるで ODBC、ただし、まだを表す重複している機能 - ドライバー マネージャーは、ISO と開いているグループに準拠しているアプリケーションで使用されて、エクスポートする必要があります。 **SQLBindParameter**のすべての機能が含まれています**SQLBindParam**、 **SQLBindParam**の上にマップする**SQLBindParameter**(基になるドライバーが、ODBC の場合*3.x*ドライバー)。 ODBC *3.x*ドライバーが実装する必要はありません**SQLBindParam**します。  
  
## <a name="remarks"></a>コメント  
 ときに、次の呼び出し**SQLBindParam**されます。  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 ドライバー マネージャー呼び出し**SQLBindParameter**ドライバーとして次のとおりです。  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 参照してください[ODBC 64 ビットの情報](../../../odbc/reference/odbc-64-bit-information.md)場合、アプリケーションが 64 ビットのオペレーティング システムで実行します。  
  
## <a name="see-also"></a>関連項目  
 [非推奨の関数のマッピング](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
