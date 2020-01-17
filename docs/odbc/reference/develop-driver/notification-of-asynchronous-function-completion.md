---
title: 非同期関数の完了の通知 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de3496661f2ab329e5bf662a9cb8fa749cb81bfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129319"
---
# <a name="notification-of-asynchronous-function-completion"></a>非同期関数の完了の通知
Windows 8 SDK とでは、ODBC は、非同期操作が完了したら、完了時に通知する"として参照するアプリケーションに通知するためのメカニズムを追加します。 (を参照してください[非同期実行 (通知方法)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)詳細についてはします)。このトピックでは、ドライバー開発者向けの問題の一部を説明します。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>ドライバー マネージャーとドライバーの間のインターフェイス  
 ドライバー マネージャーが内部的にコールバック関数を提供[SQLAsyncNotificationCallback 関数](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)します。 **SQLAsyncNotificationCallback**呼び出すことができますのみ - ドライバーでアプリケーションを直接呼び出すことはできません。 ドライバー呼び出し**SQLAsyncNotificationCallback**返す SQL_STILL_EXECUTING が最後に、サーバーから新しいデータ受信されるたびにします。  
  
 ドライバーは、対応する関数に SQL_STILL_EXECUTING が返された後に、非同期操作を実行するのにはいくつかの進行状況ときに、ドライバー マネージャーに通知できるように、ドライバー マネージャーはコールバック機構を提供します。  
  
 ドライバー マネージャーの種類の通知モードで動作するドライバーの SQL_ASYNC_NOTIFICATION_CALLBACK は、NULL 以外の関数のポインターでドライバー接続ハンドルで SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 属性を設定する非同期そのハンドルに対する操作。 ドライバー マネージャーが、これは、型の通知モードで動作するドライバーの SQL_ASYNC_NOTIFICATION_CALLBACK のも NULL 以外の関数ポインターを使用してドライバー ステートメント ハンドルで SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性を設定する同様に、そのハンドルのすべての非同期操作。  
  
 ドライバー ハンドルに対して非同期操作を実行すると、非同期のドライバー関数は非ブロッキングのスタイルで動作します。 操作はすぐに完了できず、ドライバー関数は SQL_STILL_EXECUTING を返す必要があります。 この要件は、ポーリング モードと通知モードの両方に当てはまります。  
  
 ドライバーがアドレスを持つ SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK または SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性の値は、通知のコールバック関数を呼び出す必要があります、ハンドルが通知非同期モードの場合は後に、1 回SQL_STILL_EXECUTING が返されます。 つまり、1 つ返す SQL_STILL_EXECUTING は、通知のコールバック関数の 1 つの呼び出しとペアにする必要があります。 ドライバーは呼び出しのコールバック関数のパラメーターの値として SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT または SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT ハンドルの属性の現在の値を使用する必要があります*pContext*します。  
  
 ドライバーがドライバーはこの関数を呼び出すスレッドで戻る呼び出す必要がありますいません。関数が戻る前に、進行状況を通知する理由はありません。 ドライバーは、コールバックに独自のスレッドを使用する必要があります。 ドライバー マネージャーでは、広範な処理ロジックを実行するため、ドライバーのコールバック スレッドは使用しません。  
  
 ドライバー マネージャーは、ドライバーはコールバックの後に、元の関数をもう一度呼び出します。 ドライバー マネージャーは、アプリケーション スレッドもドライバーのスレッドにあるスレッドを使用できます。 ドライバーが初期の非同期呼び出しに必要な情報を保存し、全体の非同期操作の前に保存されている値を使用してドライバー (たとえば、セキュリティ トークンまたはユーザー識別子) のスレッドに関連付けられている一部の情報を使用する場合完了します。 通常、のみ**SQLDriverConnect**、 **SQLConnect**、または**SQLBrowseConnect**その種の情報を使用する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
