---
title: データを挿入する SQLSetPos の呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e07bf71f0d622ad9095974cd7020001625edf1f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037709"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>データを挿入するための SQLSetPos の呼び出し
ときに、ODBC *2.x* odbc 作業アプリケーション*3.x*ドライバー呼び出し**SQLSetPos**で、*操作*SQL_ADD の引数、ドライバー マネージャーにこの呼び出しにマップされていない**SQLBulkOperations**します。 場合、ODBC *3.x*ドライバーを呼び出すアプリケーションを使用する必要があります**SQLSetPos** SQL_ADD で、ドライバーが操作をサポートする必要があります。  
  
 動作の 1 つの大きな違いと**SQLSetPos**を使用して呼び出した SQL_ADD は S6 の状態で呼び出された場合に発生します。 ODBC で*2.x*、ドライバーに返される S1010 とき**SQLSetPos**状態 S6 SQL_ADD で呼び出されました (後で、カーソルが位置付けられている**SQLFetch**)。 ODBC で*3.x*、 **SQLBulkOperations**で、*操作*状態 S6 SQL_ADD の呼び出すことができます。 動作の 2 つ目の主要な違いは**SQLBulkOperations**で、*操作*SQL_ADD のできるは while S5 の状態で呼び出されると、 **SQLSetPos**で、 **操作**SQL_ADD のことはできません。 ステートメントの遷移は、同じの発生を呼び出す odbc *3.x*を参照してください[付録 b:ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)します。
