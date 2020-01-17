---
title: SQLSetConnectOption のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b512a795c3b9e2d1c6aa1c7c9e92fbc42a8c7862
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125589"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption のマッピング
ODBC 2 時にします。*x*アプリケーション呼び出し**SQLSetConnectOption**を通じて、ODBC 3 *.x*ドライバーへの呼び出し  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 次のようになります。  
  
-   場合*fOption*文字列、ドライバー マネージャーの呼び出しを必要とする接続の ODBC で定義された属性を示します  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   場合*fOption*ドライバー マネージャーの呼び出し、32 ビット整数値を返す ODBC で定義された接続属性を示します  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   場合*fOption*ドライバーの定義済みの接続属性、ドライバー マネージャーの呼び出しを示します  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 上記の 3 つのケース、 *ConnectionHandle*引数の値に設定されて*hdbc*、*属性*引数の値に設定されて*fOption*、および*ValuePtr*引数と同じ値に設定されて*vParam*します。  
  
 有効な値を渡す必要がある、ドライバー マネージャーでは、ドライバーの定義済みの接続属性が文字列または 32 ビット整数の値が必要かどうかがわからない、ため、 *BufferLength*の引数**SQLSetConnectAttr**. ドライバーでの特別な意味が定義されている場合ドライバー定義接続属性を使用して呼び出す必要があります**SQLSetConnectOption**、それをサポートする必要があります**SQLSetConnectOption**します。  
  
 ODBC 2 場合。*x*アプリケーション呼び出し**SQLSetConnectOption** 、ODBC 3 でドライバー固有のステートメントのオプションを設定する *.x*ドライバー、およびオプションは、ODBC 2 で定義された *。x* ODBC 3 のオプションのバージョンのドライバーでは、新しいマニフェスト定数を定義する必要があります *.x*ドライバー。 古いのマニフェスト定数への呼び出しで使用する場合**SQLSetConnectOption**、ドライバー マネージャーが呼び出す**SQLSetConnectAttr**で、 **StringLength**引数は 0 に設定します。  
  
 ODBC 3 の場合、 *.x*ドライバー、ドライバー マネージャーは不要になったかどうかを確認します*fOption* SQL_CONN_OPT_MIN と SQL_CONN_OPT_MAX、間、または SQL_CONNECT_OPT_DRVR_START よりも大きい。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>接続レベルのステートメントのオプションを設定  
 ODBC 2。*x*、アプリケーションを呼び出すことが**SQLSetConnectOption**ステートメント オプションを設定します。 ドライバーにステートメントのオプションを既定として確立が完了したら、その接続に割り当てられた後でステートメントをします。 これはドライバーの定義、ドライバーが指定された接続に関連付けられているすべての既存のステートメントのステートメント オプションを設定するかどうか。  
  
 ODBC 3 でこの機能が非推奨とされました *.x*します。 ODBC 3 *.x*ドライバーのみをサポートする必要 ODBC 2 を設定します *。x* ODBC 2 を使用する場合は、接続レベルでのステートメント属性 *。x*これを実行するアプリケーション。 ODBC 3 *.x*アプリケーションは接続レベルでステートメント属性を設定しない必要があります。 ODBC 3 *.x*で、これは、接続属性とステートメントの属性の両方を指定できます、SQL_ATTR_METADATA_ID および SQL_ATTR_ASYNC_ENABLE 属性を除く、接続レベルでのステートメント属性を設定することはできません接続レベルまたはステートメント レベルのいずれかに設定します。
