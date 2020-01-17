---
title: 動的トレース |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8420589761a1f8cb1f9cf8a3022842863fd30758
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046891"
---
# <a name="dynamic-tracing"></a>動的トレース
トレースを有効になっているまたは実行するアプリケーションでいつでも無効になっていることができます。 これにより、任意の数の関数呼び出しをトレースするアプリケーションです。  
  
 変数**ODBCSharedTraceFlag**が動的にトレースを有効に設定します。 この変数は、すべての実行中のコピー、ドライバー マネージャーの間で共有されます。 任意のアプリケーションでは、この変数を設定、現在実行されているすべての ODBC アプリケーションのトレースが有効です。 アプリケーションが呼び出す動的トレースが有効な場合は、トレースを有効にする**SQLSetConnectAttr** SQL_TRACE_OFF SQL_ATTR_TRACE に設定します。 この呼び出しは、そのアプリケーションに対してのみトレースを無効になります。 Odbc32.lib とリンクされているアプリケーションは、この変数の使用を変更できます。 ODBC のセッション後に開く必要のあるトレース ファイルではなく、リアルタイムのウィンドウで、トレース データを表示できます。 コントロールでトレースをオンまたはオフは、アプリケーションの画面に追加できます。  
  
 DLL は、ODBC 3 に付属するトレース *.x*はスレッド セーフではありません。 グローバル トレースが有効になっている場合に、ログ ファイルが正しくに書き込むことは保証されません (変数**ODBCSharedTraceFlag**設定されている) と 1 つ以上のアプリケーションが同時に、トレース ファイルに書き込みます。 この条件では、エラーは返されません。
