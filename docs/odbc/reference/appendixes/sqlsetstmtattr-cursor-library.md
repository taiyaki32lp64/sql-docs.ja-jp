---
title: SQLSetStmtAttr (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc222c1c8669769060de4fc0a1390a9bf02e3f31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091695"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLSetStmtAttr**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLSetStmtAttr**を参照してください[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)します。  
  
 カーソル ライブラリでは、次のステートメント属性をサポートしている**SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 カーソル ライブラリでは、SQL_CURSOR_FORWARD_ONLY と SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE ステートメント属性の値のみをサポートします。  
  
 順方向専用カーソルでは、カーソル ライブラリではまた、ステートメント属性 SQL_ATTR_CONCURRENCY の SQL_CONCUR_READ_ONLY 値をサポートしています。 静的カーソル、カーソル ライブラリでは、SQL_ATTR_CONCURRENCY ステートメント属性の値の SQL_CONCUR_READ_ONLY と SQL_CONCUR_VALUES 値をサポートしています。  
  
 カーソル ライブラリでは、SQL_ATTR_SIMULATE_CURSOR ステートメント属性の SQL_SC_NON_UNIQUE 値のみをサポートします。  
  
 呼び出しをサポートしていますが、ODBC 仕様**SQLSetStmtAttr**後 SQL_ATTR_PARAM_BIND_TYPE または SQL_ATTR_ROW_BIND_TYPE 属性を持つ**SQLFetch**または**SQLFetchScroll**が呼び出されると、カーソル ライブラリはありません。 カーソル ライブラリのバインドの種類を変更することができます、前に、アプリケーションは、カーソルを閉じる必要があります。 カーソル ライブラリが SQL_ATTR_ROW_BIND_OFFSET_PTR、SQL_ATTR_PARAM_BIND_OFFSET_PTR、SQL_ATTR_ROWS_FETCHED_PTR、変更をサポートし、SQL_ATTR_PARAMS_PROCESSED_PTR ステートメント属性と、カーソルが開いています。  
  
 アプリケーションが呼び出すことができます**SQLSetStmtAttr**で、**属性**カーソルが開いている間、行セットのサイズを変更する sql_attr_row_array_size を指定します。 新しい行セットのサイズは、次回に効果にかかる**SQLFetchScroll**または**SQLFetch**が呼び出されます。  
  
 カーソル ライブラリでは、バインディングのオフセットを有効にする SQL_ATTR_PARAM_BIND_OFFSET_PTR または SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性の設定をサポートします。 バインディングのオフセットへの呼び出しには使用されません**SQLFetch** ODBC 2 と共にカーソル ライブラリを使用する場合 *。x*ドライバー。  
  
 カーソル ライブラリでは、SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS ステートメント属性に設定をサポートします。
