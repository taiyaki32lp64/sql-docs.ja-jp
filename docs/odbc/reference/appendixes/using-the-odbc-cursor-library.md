---
title: ODBC カーソル ライブラリを使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdddf2e757c549de460f5e22c2ea76ce91a2a969
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069970"
---
# <a name="using-the-odbc-cursor-library"></a>ODBC カーソル ライブラリの使用
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 ODBC カーソル ライブラリで、アプリケーションを使用します。  
  
1.  呼び出し**SQLSetConnectAttr**で、*属性*の SQL_ATTR_ODBC_CURSORS、特定の接続でのカーソル ライブラリの使用方法を指定します。 カーソル ライブラリは常にすることができます (SQL_CUR_USE_ODBC) の使用、ドライバーがスクロール可能なカーソル (SQL_CUR_USE_IF_NEEDED) をサポートしていない場合にのみ使用、または (SQL_CUR_USE_DRIVER) が使用されていません。  
  
2.  呼び出し**SQLConnect**、 **SQLDriverConnect**、または**SQLBrowseConnect**データ ソースに接続します。  
  
3.  呼び出し**SQLSetStmtAttr** (SQL_ATTR_CURSOR_TYPE) のカーソルの種類、同時実行 (SQL_ATTR_CONCURRENCY)、および行セットのサイズ (SQL_ATTR_ROW_ARRAY_SIZE) を指定します。 カーソル ライブラリでは、順方向専用カーソルと静的カーソルをサポートします。 静的カーソルは読み取り専用にすることができますまたは値を比較するオプティミスティック同時実行制御を使用することができます、順方向専用カーソルは読み取り専用をある必要があります。  
  
4.  バッファーの行セットおよび呼び出しの 1 つまたは複数割り当てる**SQLBindCol**結果セット列にこれらのバッファーをバインドする 1 つ以上の時間。  
  
5.  実行によって結果セットが生成されます、**選択**ステートメントまたはプロシージャ、またはカタログ関数を呼び出すことによって。 実行する場合は、アプリケーションが位置指定の update ステートメントを実行、**選択更新**結果セットを生成するステートメント。  
  
6.  呼び出し**SQLFetch**または**SQLFetchScroll**結果セットをスクロールする 1 つ以上の時間。  
  
 アプリケーションでは、行セットのバッファー内のデータ値を変更できます。 カーソル ライブラリのキャッシュからデータを行セットのバッファーを更新するアプリケーションを呼び出す**SQLFetchScroll**で、 *FetchOrientation*引数 SQL_FETCH_RELATIVE に設定し、 *FetchOffset*引数は 0 に設定します。  
  
 アプリケーションの呼び出し、バインドされていない列からデータを取得する**SQLSetPos**に目的の行にカーソルを移動します。 呼び出して**SQLGetData**データを取得します。  
  
 アプリケーションを呼び出しますが、データ ソースから取得された行の数を決定する**SQLRowCount**します。
