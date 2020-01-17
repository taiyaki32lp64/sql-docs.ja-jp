---
title: API 関数 (ODBC Driver for Oracle) でスレッド セーフの注意事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 926b2285bcce9a28579fffc4004c5454b2837392
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912431"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 関数 (ODBC Driver for Oracle) のスレッド セーフの注意事項
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 Microsoft ODBC Driver for Oracle がスレッド セーフです。ただし、Oracle は、1 つの接続で複数の同時実行ステートメントをできません。 ドライバーは、この制限を適用します。 つまり、マルチ スレッド アプリケーションで任意のスレッドは、ODBC Driver for Oracle にいつでもでも呼び出すことができますが、ドライバー ブロック、同じ接続で、ドライバーからの他のスレッド、元のスレッドが、ドライバーを離れるまでします。  
  
 ドライバーでは、2 つの異なる接続で 2 つのステートメントがある場合はブロックされません。 ただし、2 つのステートメントで 1 つの接続がある場合はブロックする可能性があります。
