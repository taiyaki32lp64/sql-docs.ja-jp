---
title: 接続ハンドル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab8b94835fb9a6103436026a669c86f2401d57b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036431"
---
# <a name="connection-handles"></a>接続ハンドル
A*接続*ドライバーとデータ ソースで構成されます。 接続ハンドルでは、各接続を識別します。 接続ハンドルでは、ドライバーを使用するだけでなく、ドライバーを使用するデータ ソースを定義します。 ODBC ドライバー マネージャー (ドライバー) を実装するコードのセグメント内では、接続ハンドルは、次の接続情報を格納する構造体を識別します。  
  
-   接続の状態  
  
-   現在の接続レベルの診断  
  
-   ステートメントとの接続で現在割り当てられている記述子ハンドル  
  
-   各接続属性の現在の設定  
  
 ODBC は、ドライバーによってサポートされる場合、複数の同時接続を防止できません。 そのため、特定の ODBC 環境では、複数の接続ハンドルは、さまざまなドライバーと同じドライバーへのデータ ソースとデータ ソース、または同じドライバーとデータ ソースに対して複数の接続にもさまざまなをポイント可能性があります。 一部のドライバー サポート; アクティブな接続の数を制限します。オプション、SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo**特定のドライバーがサポートしているアクティブな接続の数を指定します。  
  
 接続ハンドルは、データ ソースに接続するときに主に使用 (**SQLConnect**、 **SQLDriverConnect**、または**SQLBrowseConnect**)、データから切断ソース (**SQLDisconnect**)、ドライバーとデータ ソースに関する情報の取得 (**SQLGetInfo**)、診断の取得 (**SQLGetDiagField**と**SQLGetDiagRec**)、トランザクションを実行して (**SQLEndTran**)。 設定および接続属性を取得するときにも使用されます (**SQLSetConnectAttr**と**SQLGetConnectAttr**) と、SQL ステートメントのネイティブ形式を取得するときに (**SQLNativeSql**).  
  
 使用して接続ハンドルが割り当てられた**SQLAllocHandle**およびに解放された**SQLFreeHandle**します。
