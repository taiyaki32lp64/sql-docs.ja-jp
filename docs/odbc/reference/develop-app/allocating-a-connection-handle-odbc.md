---
title: ODBC 接続ハンドルの割り当て |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bd3a44fe4f0466dfcf11a72fa0377564c1cf02f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077206"
---
# <a name="allocating-a-connection-handle-odbc"></a>接続ハンドルの割り当て (ODBC)
アプリケーションは、データ ソースまたはドライバーに接続できる、ように、接続ハンドルを割り当てますする必要があります。  
  
1.  アプリケーションは、SQLHDBC 型の変数を宣言します。 呼び出して**SQLAllocHandle**環境を接続、および sql_handle_dbc としてオプションを割り当てるのハンドルは、この変数のアドレスを渡します。 以下に例を示します。  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  ドライバー マネージャーは、ステートメントの情報を格納する構造体を割り当てるし、変数内の接続ハンドルを返します。  
  
 ドライバー マネージャーは呼び出しません**SQLAllocHandle**このドライバーで時間を呼び出すには、どのドライバーがわからないためです。 呼び出し元を遅らせる**SQLAllocHandle**ドライバー、アプリケーションがデータ ソースに接続する関数を呼び出すまでにします。 詳細については、次を参照してください。[接続処理でドライバー マネージャーの役割](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)、このセクションで後述します。  
  
 接続ハンドルの割り当てではありません、ドライバーの読み込みと同じに重要です。 接続の関数が呼び出されるまでは、ドライバーは読み込まれません。 そのため、接続ハンドルの割り当て後に、ドライバーまたはデータ ソースに接続する前に、接続ハンドルを使用して、アプリケーションが呼び出すことができますのみの機能は**SQLSetConnectAttr**、 **SQLGetConnectAttr**、または**SQLGetInfo** SQL_ODBC_VER オプションを使用します。 接続ハンドルで他の関数の呼び出し**SQLEndTran**、SQLSTATE 08003 (接続は開いていません) を返します。 詳細については、次を参照してください[付録 b:。ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)します。  
  
 接続ハンドルの詳細については、次を参照してください。[接続ハンドル](../../../odbc/reference/develop-app/connection-handles.md)します。
