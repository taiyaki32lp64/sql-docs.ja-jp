---
title: 複数のアクティブなステートメントと接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76b74ff748a62a401955e4ea4a995f507314124e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942825"
---
# <a name="multiple-active-statements-and-connections"></a>複数のアクティブなステートメントと接続
一部のドライバーと Dbms は、ステートメントと同時にアクティブにできる接続の数を制限します。 これらの数値は、いずれかのような小さいできます。 詳細については、SQL_MAX_CONCURRENT_ACTIVITIES と SQL_MAX_DRIVER_CONNECTIONS のオプションを参照してください、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明、および[ステートメントが処理](../../../odbc/reference/develop-app/statement-handles.md)と[接続ハンドル](../../../odbc/reference/develop-app/connection-handles.md)します。
