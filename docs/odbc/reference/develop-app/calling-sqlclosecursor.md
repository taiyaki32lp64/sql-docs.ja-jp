---
title: SQLCloseCursor の呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 447a0892049317813fa9fe6986e6219922a11e28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068688"
---
# <a name="calling-sqlclosecursor"></a>SQLCloseCursor の呼び出し
**SQLCloseCursor**とほぼ同じ**SQLFreeStmt** SQL_CLOSE で、ドライバー マネージャーがマップされていないこの関数。 置換関数は、既存するためのマップ ODBC *2.x* ODBC へのアプリケーションを簡単に移動できます*3.x*新しい関数を使用しています。 このような移動では、新しい ODBC の使用を開始するには、このようなアプリケーションを簡単に*3.x*モジュール方式で条件付きコード内で機能します。 **SQLCloseCursor**の新しい機能を表していません。 アプリケーションが移行することによってメリットを利用できない**SQLCloseCursor**から**SQLFreeStmt** SQL_CLOSE とします。
