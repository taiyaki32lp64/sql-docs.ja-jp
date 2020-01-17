---
title: SQLSetConnectAttr (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73d1369a2bce0327ac3367d33f0894bdcfab8205
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125579"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLSetConnectAttr**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLSetConnectAttr**を参照してください[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)します。  
  
 アプリケーションを呼び出す**SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 属性をカーソル ライブラリが常に使用になっていること、ドライバーは、スクロール可能なカーソルをサポートしていない場合に使用または使用しないかどうかを指定します。 カーソル ライブラリは、ドライバーでは、SQL_CA1_RELATIVE で SQL_STATIC_CURSOR_ATTRIBUTES1 情報の種類を返す場合に、スクロール可能なカーソルがサポートしている前提としています。 **SQLGetInfo**します。  
  
 アプリケーションを呼び出す必要があります**SQLSetConnectAttr**呼び出した後、カーソル ライブラリの使用量を指定する**SQLAllocHandle**で、 *HandleType*の割り当てを sql_handle_dbc として接続およびデータ ソースに接続する前にします。 アプリケーションを呼び出す場合**SQLSetConnectAttr** SQL_ATTR_ODBC_CURSORS 属性を持つ接続がまだアクティブなときに、カーソル ライブラリ エラーが返されます。  
  
 接続に関連付けられているすべてのステートメントのカーソル ライブラリでサポートされているステートメント属性を設定するアプリケーションを呼び出す必要があります**SQLSetConnectAttr**とその前に、データ ソースに接続した後は、そのステートメント属性カーソルを開きます。 アプリケーションを呼び出す場合**SQLSetConnectAttr**ステートメントで属性と、カーソルが開いている接続に関連付けられているステートメントで、カーソルが閉じられるまで、ステートメント属性をそのステートメントに適用されませんが、再度開きます。
