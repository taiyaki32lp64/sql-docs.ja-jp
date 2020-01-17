---
title: ヘッダー レコード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7f5fe5cf6aae0d5953cc82b845396dd4164c7fa3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139024"
---
# <a name="header-record"></a>ヘッダー レコード
ヘッダー レコード内のフィールドには、リターン コード、行の数、実行されるステートメントの状態のレコードの数と種類などの関数の実行に関する一般的な情報が含まれています。 関数から SQL_INVALID_HANDLE が返さしない限り、ヘッダー レコードが常に作成されます。 ヘッダー レコードのフィールドの完全な一覧を参照してください、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)関数の説明。
