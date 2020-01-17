---
title: 接続のオプション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4358756deaa595ee5e10df0490522631201b9c87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023375"
---
# <a name="connect-options"></a>接続のオプション
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 これらのオプションは、アプリケーション内でデータベース接続のカスタマイズを許可します。  
  
|接続オプション|メモ|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|アプリケーションのコミットまたはとのトランザクションをロールバックする必要があります明示的に SQL_AUTOCOMMIT_OFF 場合は、 [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)します。|  
|SQL_ODBC_CURSORS|この接続属性は、ドライバー マネージャーで実装されます。|  
|SQL_OPT_TRACE|この接続属性は、ドライバー マネージャーで実装されます。|  
|SQL_OPT_TRACEFILE|この接続属性は、ドライバー マネージャーで実装されます。|  
|SQL_TRANSLATE_DLL|エラーが返されます。"Driver できません。"|  
|SQL_TRANSLATE_OPTION|翻訳の .dll に 32 ビット値が渡されます。|  
|SQL_TXN_ISOLATION|ドライバーでは、SQL_TXN_READ_COMMITTED のみ使用できます。<br /><br /> 次の vParams がサポートされていません。<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|この ODBC 3.0 接続属性を使用すると、Oracle の Microsoft コンポーネント サービス (または Windows NT を使用している場合は、MTS) によってコーディネートされる分散トランザクションで ODBC ドライバーを使用できます。 インターフェイス ポインターを提供します*pITransaction*としてトランザクションに、 *vParam*引数。|  
|SQL_ATTR_CONNECTION_DEAD|この読み取り専用の 3.5 インチの ODBC 接続属性では、Oracle サーバーへの接続が失敗したかどうかを判断できます。 Get だけです。設定できません。|
