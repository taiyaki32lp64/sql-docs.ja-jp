---
title: ドライバー マネージャー&#39;接続プロセスでの役割 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fdc7f82059579f23c9a1a1203aee5e45c87693e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046941"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>ドライバー マネージャー&#39;接続プロセスでの役割
いるアプリケーションはドライバー関数を直接呼び出すできませんに注意してください。 代わりに、同じ名前のドライバー マネージャーの関数を呼び出すし、ドライバー マネージャーがドライバー関数を呼び出します。 通常、これはほぼ瞬時に。 たとえば、アプリケーションが呼び出す**SQLExecute**ドライバー マネージャーは、ドライバー マネージャーで、いくつかのエラー チェックした後、 **SQLExecute**ドライバー。  
  
 接続プロセスは異なります。 アプリケーションを呼び出すと**SQLAllocHandle**を sql_handle_env としてと sql_handle_dbc としてオプションで、関数がハンドル ドライバー マネージャーでのみを割り当てます。 ドライバー マネージャーを呼び出すには、どのドライバーが知らないので、ドライバーでは、この関数は呼び出されません。 同様に、アプリケーションが接続されていない接続へのハンドルを渡すかどうか**SQLSetConnectAttr**または**SQLGetConnectAttr**、のみ、ドライバー マネージャーは、関数を実行します。 格納または取得の接続からの属性の値は、処理し、属性の値を取得するが設定されていないと ODBC の SQLSTATE 08003 (接続は開いていません) を返しますが、既定値を定義していません。  
  
 アプリケーションを呼び出すと**SQLConnect**、 **SQLDriverConnect**、または**SQLBrowseConnect**、ドライバー マネージャーは、最初に使用するドライバーを決定します。 これは、後、ドライバーが接続に現在読み込まれているかどうかを判断するためのチェックで:  
  
-   接続でドライバーが読み込まれていない場合、ドライバー マネージャーは、同じ環境内で他の接続に指定されたドライバーが読み込まれるかどうかを確認します。 かどうか、ドライバー マネージャーのドライバーがロードの呼び出し、接続で**SQLAllocHandle** sql_handle_env としてオプションを使用してドライバー。  
  
     ドライバー マネージャーを呼び出して**SQLAllocHandle**ドライバー sql_handle_dbc としてオプションを使用するには、かどうかが読み込まれただけです。 ドライバー マネージャーを呼び出す場合は、アプリケーションでは、任意の接続属性を設定、 **SQLSetConnectAttr**ドライバーでエラーが発生する場合、ドライバー マネージャーの接続を返します SQLSTATE IM006 (ドライバーの**SQLSetConnectAttr**できませんでした)。 最後に、ドライバー マネージャーは、ドライバーの接続関数を呼び出します。  
  
-   接続で指定されたドライバーが読み込まれる場合、ドライバー マネージャーは、ドライバーの接続関数のみを呼び出します。 この場合、ドライバーは接続上のすべての接続属性が、現在の設定を保持することを確認してください。  
  
-   ドライバー マネージャーを呼び出す場合は、接続で別のドライバーが読み込まれる**SQLFreeHandle**接続を解放するドライバー。 ドライバー マネージャーは、ドライバーを使用するその他の接続がない場合は、 **SQLFreeHandle**環境を解放するドライバーとドライバーをアンロードします。 ドライバー マネージャーは、ドライバーが接続に読み込まれていない場合と同じ操作を実行します。  
  
 ドライバー マネージャーは、環境ハンドルをロック (*henv*) ドライバーを呼び出す前に**SQLAllocHandle**と**SQLFreeHandle**とき*HandleType*に設定されている**sql_handle_dbc として**します。  
  
 アプリケーションを呼び出すと**SQLDisconnect**、ドライバー マネージャー呼び出し**SQLDisconnect**ドライバー。 ただし、アプリケーションがドライバーに再接続する場合に読み込まれるドライバーが残ります。 アプリケーションを呼び出すと**SQLFreeHandle**ドライバー マネージャーの呼び出しを sql_handle_dbc としてオプションで**SQLFreeHandle**ドライバー。 他の接続で、ドライバーを使用しない場合、ドライバー マネージャーは、呼び出し**SQLFreeHandle** sql_handle_env としてとドライバーのオプションを選択し、ドライバーをアンロードします。
