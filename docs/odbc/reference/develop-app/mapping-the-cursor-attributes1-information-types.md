---
title: Cursor Attributes1 の情報の種類のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d95d3e67fdcd7159074e2f20ffa558f4c80bbcb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036361"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Cursor Attributes1 の情報の種類のマッピング
ODBC 3 時にします。*x*アプリケーション呼び出し**SQLGetInfo** ODBC 2 で *.x* SQL_XXXX_CURSOR_ATTRIBUTES1 情報の種類のドライバー (dynamic、順方向専用、キーセットのドライバーの場合、または静的カーソル)、ドライバー マネージャーによって返されるビットの設定は、どのような ODBC 2 に依存します。*x*ドライバーは、対応する ODBC 2 を返します *。x*情報の種類。 次の表に示すように、ビットが設定されます。  
  
|内のビットします。<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|カーソルの種類|ODBC 2。*x*情報<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE、SQL_CA1_BOOKMARK|動的、キーセット、静的|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE、SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|動的、キーセット、静的|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE、SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|動的、キーセット、静的|SQL_POS_OPERATIONS|
