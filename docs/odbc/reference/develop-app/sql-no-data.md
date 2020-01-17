---
title: SQL_NO_DATA が |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f899e7a034e1ec5fc967d834caad3a4ccc4caa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041829"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
ODBC 3 時にします。*x*アプリケーション呼び出し**SQLExecDirect**、 **SQLExecute**、または**SQLParamData** 、ODBC 2 *。x*検索の更新の実行、または、ドライバーは、データ ソースで行には影響しませんステートメントを削除するドライバーが SQL_SUCCESS、いない SQL_NO_DATA を返す必要があります。 ODBC 2 時にします。*x*または ODBC 3 *。x*アプリケーションは、ODBC 3 の操作します *。x*ドライバー呼び出し**SQLExecDirect**、 **SQLExecute**、または**SQLParamData**と同じ結果が、ODBC 3 *。x*ドライバーが SQL_NO_DATA を返す必要があります。
