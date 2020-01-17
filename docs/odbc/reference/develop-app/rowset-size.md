---
title: 行セットのサイズ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fda38811fa876c9a0fad55e7f2ee7566ad3026d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943767"
---
# <a name="rowset-size"></a>行セット サイズ
使用するには、どの行セット サイズは、アプリケーションに依存します。 通常、画面ベースのアプリケーションでは、2 つの方法のいずれかに従います。 1 つは、行セット サイズを画面に表示される行の数に設定するのには場合は、ユーザーは、画面をサイズ変更、アプリケーションがそれに応じて行セットのサイズを変更します。 2 つ目より大きななどの番号を 100、データ ソースへの呼び出しの数が減少する行セットのサイズを設定します。 アプリケーションでは、可能な場合に、行セット内でローカルにスクロールし、スクロール、行セット外の場合にのみ新しい行がフェッチされます。  
  
 レポートなどの他のアプリケーションが適切に処理できるアプリケーションの最大行数を行セットのサイズを設定する傾向がありますより大きな行セットをネットワークの行ごとのオーバーヘッドは減少場合があります。 正確にどのように大規模な行セットできるは、各行と、使用可能なメモリの量のサイズによって異なります。  
  
 呼び出して行セットのサイズが設定されて**SQLSetStmtAttr**で、*属性*引数 sql_attr_row_array_size を指定します。 アプリケーションが行セット サイズを変更する、新しい行セットのバッファーをバインド (呼び出して**SQLBindCol**バインディングのオフセットを指定するか) 行がフェッチされた後でもまたはその両方です。 行セット サイズを変更する場合の影響は、関数に依存します。  
  
-   **SQLFetch**と**SQLFetchScroll**をフェッチする行の数を決定する、呼び出し時に行セットのサイズを使用します。 ただし、 **SQLFetchScroll**で、 *FetchOrientation* SQL_FETCH_NEXT インクリメントのカーソルに基づく、行セットをフェッチし、前回フェッチの現在の行セットのサイズに基づく行セット。  
  
-   **SQLSetPos**前の呼び出しの時点で有効になっている行セットのサイズを使用して**SQLFetch**または**SQLFetchScroll**ため、 **SQLSetPos**行セットで動作します。既に設定されています。 **SQLSetPos**場合を新しい行セットのサイズを選択も**SQLBulkOperations**が行セットのサイズが変更された後に呼び出されました。  
  
-   **SQLBulkOperations**フェッチされた行セットの独立したテーブルに対する操作を実行するため、呼び出し時に有効な行セットのサイズを使用します。
