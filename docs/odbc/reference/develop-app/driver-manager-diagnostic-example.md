---
title: ドライバー マネージャー診断の例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95392367b70af3eb820f0943af5dc668783a3fe5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046964"
---
# <a name="driver-manager-diagnostic-example"></a>ドライバー マネージャー診断の例
ドライバー マネージャー診断メッセージを生成できます。 たとえば、アプリケーションに渡された無効な方向を**SQLDataSources**、ドライバー マネージャーが書式設定しから次の値を返す可能性があります**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 ドライバー マネージャーでエラーのため、そのプレフィックスに追加、診断メッセージ ([Microsoft]) のベンダーとその識別子 ([ODBC ドライバー マネージャー])。
