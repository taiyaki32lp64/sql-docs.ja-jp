---
title: SQLGetDiagRec および SQLGetDiagField の実装 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4b602d5ff4a94d2888395e6a62f03553fb50f98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216374"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec および SQLGetDiagField の実装
**SQLGetDiagRec**と**SQLGetDiagField**ドライバー マネージャーと各ドライバーによって実装されます。 ドライバー マネージャーと各ドライバーは、環境、接続、ステートメント、および記述子ハンドルの診断レコードの管理し、ハンドルまたはハンドルが解放されることで別の関数が呼び出されたときにのみ、これらのレコードを解放します。  
  
 ドライバー マネージャーと各ドライバーの両方に順位付けに従って最初の状態レコードを決定する必要がありますが[状態レコードのシーケンス](../../../odbc/reference/develop-app/sequence-of-status-records.md)、ドライバー マネージャーは、レコードの最後のシーケンスを決定します。  
  
 **SQLGetDiagRec**と**SQLGetDiagField**自体についての診断レコードを投稿できません。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [診断の処理規則](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [ドライバー マネージャーのロール](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [ドライバーのロール](../../../odbc/reference/develop-app/role-of-the-driver.md)
