---
title: Dbms でのトランザクションのサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72353e9917996ecacdc5971b4a11f9c73718ba43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037631"
---
# <a name="transaction-support-in-dbmss"></a>DBMS でのトランザクションのサポート
特にデスクトップ データベース dBASE、Paradox、市販など、一部のデータベースでは、トランザクションはサポートされません。 トランザクションをサポートするデータベースの間でもはバリエーションの 1 つの SQL ステートメントの種類がトランザクションにすることができます。 詳細についてで SQL_TXN_CAPABLE オプションを参照して、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明。
