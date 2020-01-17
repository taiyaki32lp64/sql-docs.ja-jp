---
title: 接続属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09b29277d74383abff1510ca7394aecad036fc7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036439"
---
# <a name="connection-attributes"></a>接続属性
接続属性は、接続の特性です。 たとえば、トランザクションは接続レベルで行われるので、トランザクション分離レベルは 1 つの接続属性になります。 同様に、ログイン タイムアウト、または、タイムアウトするまでに接続しているときに待機する秒数は、接続属性です。  
  
 接続属性が設定されて**SQLSetConnectAttr**で、現在の設定の取得と**SQLGetConnectAttr**します。 場合**SQLSetConnectAttr**ドライバーが読み込まれる、ドライバー マネージャー ストアの接続構造内の属性とドライバーの接続プロセスの一環としてそれらを設定する前に呼び出されます。 アプリケーションで任意の接続属性を設定する必要はありません。すべての接続属性では、その一部は、ドライバー固有の既定値があります。  
  
 接続、またはいずれかの属性と、ドライバーによって前に、または後、接続属性を設定できます。 ログイン タイムアウト (SQL_ATTR_LOGIN_TIMEOUT) が接続プロセスに適用され、有効な場合にのみ接続する前に設定します。 ドライバー マネージャーとドライバーの間に ODBC カーソル ライブラリが存在するため、接続する前に、ODBC カーソル ライブラリ (SQL_ATTR_ODBC_CURSORS) およびネットワーク パケット サイズ (SQL_ATTR_PACKET_SIZE) を使用するかどうかを指定する属性を設定する必要があり、そのため読み込む必要がある、ドライバーの前にします。  
  
 データ ソースが読み取り専用か前に、または、ドライバーによって、接続した後、読み取り/書き込み (SQL_ATTR_ACCESS_MODE) と、現在のカタログ (SQL_ATTR_CURRENT_CATALOG) を設定できますかを指定する属性。 ただし、相互運用可能なアプリケーション設定に接続する前に一部のドライバーが接続した後は、これらの変更をサポートしていないためです。  
  
 いくつかの接続属性では、そうでないときに、接続が行われる前に、既定値があります。 そうでは、SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE、SQL_ATTR_TRACEFILE です。  
  
 接続した後、翻訳接続属性 (SQL_ATTR_TRANSLATE_DLL および SQL_ATTR_TRANSLATE_OPTION) を設定する必要があります。  
  
 その他のすべての接続属性は、いつでも設定できます。 詳細については、次を参照してください。、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)関数の説明。 (への呼び出しによって環境レベルの接続属性を設定することはできません**SQLSetEnvAttr**)。
