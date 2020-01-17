---
title: SQLSetPos (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87ff006e7bead36c2aa6476b99552d1524c213b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091711"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLSetPos**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLSetPos**を参照してください[SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)します。  
  
 カーソル ライブラリのみ SQL_POSITION 操作をサポートする、*操作*引数**SQLSetPos**します。 SQL_LOCK_NO_CHANGE 値のみがサポートしている、 *LockType*引数。  
  
 ドライバーが一括操作をサポートしていない場合、カーソル ライブラリは SQLSTATE HYC00 を返します (ドライバーに対応していない) 場合**SQLSetPos**を使用して呼び出した*RowNumber*を 0 に等しい。 このドライバーの動作は推奨されません。  
  
 カーソル ライブラリがへの呼び出しで、SQL_UPDATE および SQL_DELETE 操作をサポートしていない**SQLSetPos**します。 位置指定更新または作成を検索して SQL ステートメントを削除、カーソル ライブラリが実装を更新またはバインドされた各列には、そのキャッシュに格納されている値を列挙する WHERE 句を使用したステートメントを削除します。 詳細については、次を参照してください。[配置されている更新プログラムの処理と削除ステートメント](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)します。  
  
 ドライバーが静的カーソルをサポートしていない場合、アプリケーションのカーソル ライブラリの操作を呼び出す必要があります**SQLSetPos**によってフェッチされる行セットでのみ**SQLExtendedFetch**または**SQLFetchScroll**ではなく**SQLFetch**します。 カーソル ライブラリを実装する**SQLExtendedFetch**と**SQLFetchScroll**の繰り返しを呼び出すことで**SQLFetch** (1 の行セット サイズ) のドライバーにします。 カーソル ライブラリへの呼び出しに渡します**SQLFetch**、on、もう一方に渡して、を通じてドライバー。 場合**SQLSetPos**によってフェッチされる複数行の行セットで呼び出される**SQLFetch**呼び出しは失敗しますので、ドライバーが静的カーソルをサポートしていない場合**SQLSetPos**は機能しません順方向専用カーソル。 アプリケーションが正常に呼び出された場合でも、これは発生**SQLSetStmtAttr**に設定する SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC で、ドライバーが静的カーソルをサポートしていない場合でも、カーソル ライブラリをサポートしています。
