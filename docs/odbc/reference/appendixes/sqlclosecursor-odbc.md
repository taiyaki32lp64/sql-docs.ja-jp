---
title: SQLCloseCursor_ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4d0f88d2d9eaba7d95ba887ffbe11e728320b17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123378"
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLCloseCursor**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLCloseCursor**を参照してください[SQLCloseCursor 関数](../../../odbc/reference/syntax/sqlclosecursor-function.md)します。  
  
 カーソル ライブラリは、呼び出し元をサポートしていません**SQLCloseCursor**開いているカーソルなし。 この作業を行うと、SQLSTATE 24000 (無効なカーソル状態) が返されます。 呼び出す**SQLFreeStmt**で、*オプション*SQL_CLOSE のカーソル ライブラリによってサポートされているが場合カーソルが開いていません。
