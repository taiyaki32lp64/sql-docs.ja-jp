---
title: C データ型の旧バージョンとの互換性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcfc4dd2ef1bee2783f073fbb85c0d911f84305a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037803"
---
# <a name="backward-compatibility-of-c-data-types"></a>C データ型の下位互換性
SQL_C_SHORT、SQL_C_LONG、および SQL_C_TINYINT に置換された ODBC の符号付きと符号なし型。SQL_C_SSHORT、SQL_C_USHORT、SQL_C_SLONG、SQL_C_ULONG と SQL_C_STINYINT および SQL_C_UTINYINT。 ODBC *3.x*動作する ODBC ドライバー *2.x*アプリケーションは、そのドライバー マネージャーを使用して渡されるから呼び出されると、SQL_C_SHORT、SQL_C_LONG、SQL_C_TINYINT、サポートする必要があります、ドライバー。
