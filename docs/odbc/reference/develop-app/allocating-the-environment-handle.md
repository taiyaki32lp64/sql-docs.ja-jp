---
title: 環境ハンドルの割り当て |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 823ea02a2acb6a28f56c58bb40fe684a2589bd24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077182"
---
# <a name="allocating-the-environment-handle"></a>環境ハンドルの割り当て
ODBC アプリケーションの最初のタスクが、ドライバー マネージャーの読み込みにはこれを行う方法は、オペレーティング システムに依存します。 たとえば、Microsoft® Windows NT® Server または Windows 2000 Server、Windows NT ワークステーション/Windows 2000 Professional、または Microsoft Windows® 95/98 を実行するコンピューターでアプリケーションかへのリンク ドライバー マネージャーのライブラリまたは呼び出し**LoadLibrary**ドライバー マネージャーの DLL を読み込めません。  
  
 次のタスクは、アプリケーションが、他の ODBC 関数を呼び出す前に完了する必要がありますが、ODBC 環境を初期化し、次のように、環境ハンドルを割り当てるには。  
  
1.  アプリケーションは、SQLHENV 型の変数を宣言します。 呼び出して**SQLAllocHandle**し、この変数と sql_handle_env としてオプションのアドレスを渡します。 以下に例を示します。  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  ドライバー マネージャーは、環境に関する情報を格納する構造体を割り当てるし、変数内の環境ハンドルを返します。  
  
 ドライバー マネージャーは呼び出しません**SQLAllocHandle**このドライバーで時間を呼び出すには、どのドライバーがわからないためです。 呼び出し元を遅らせる**SQLAllocHandle**ドライバー、アプリケーションがデータ ソースに接続する関数を呼び出すまでにします。 詳細については、次を参照してください。[接続処理でドライバー マネージャーの役割](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)、このセクションで後述します。  
  
 アプリケーションは、ODBC を使用してが完了したら、使用して、環境ハンドルが解放されます**SQLFreeHandle**します。 これは、環境を解放した後、ODBC 関数呼び出しで、環境のハンドルを使用するアプリケーション プログラミング エラーこれには結果が未定義であるが、致命的な可能性があります。  
  
 ときに**SQLFreeHandle**を呼び出すと、ドライバーのリリースの環境に関する情報を格納する構造体を使用します。 なお**SQLFreeHandle**その環境ハンドルのすべての接続ハンドルが解放されるまでの環境ハンドルを呼び出すことができません。  
  
 環境ハンドルの詳細については、次を参照してください。[環境処理](../../../odbc/reference/develop-app/environment-handles.md)します。
