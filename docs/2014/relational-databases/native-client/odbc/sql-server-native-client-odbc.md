---
title: SQL Server Native Client (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, ODBC
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], ODBC
- SQL Server Native Client ODBC driver
- ODBC
- SQL Server Native Client, ODBC
- ODBC, about SQL Server Native Client ODBC driver
ms.assetid: 811d5ba3-a2b8-48c0-adbc-8c91f041f458
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 570c0574357d9315f0e6b153f3eeabac79ec673b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63055662"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
  ODBC は、リレーショナル データベースまたは索引順次アクセス方式 (ISAM) データベースのデータへのアクセスに使用するアプリケーション プログラミング インターフェイス (API) の標準的な定義です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と通信する C および C++ アプリケーションの作成に使用されるネイティブ API の 1 つとして、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを介して ODBC をサポートしています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用して作成された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プログラムは、C 関数の呼び出しによって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と通信します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の ODBC 関数が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに実装されています。 ドライバーは、SQL ステートメントを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に渡し、ステートメントの結果をアプリケーションに返します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは Microsoft Win32 ODBC 3.51 仕様に準拠しています。 以前のバージョンの ODBC を使用して作成されているアプリケーションは、ODBC 3.51 仕様で定義されている方法に従ってサポートされます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [データ ソース名と 64 ビット オペレーティング システム](data-source-names-and-64-bit-operating-systems.md)  
  
-   [SQL Server Native Client ODBC ドライバー アプリケーションの作成](creating-a-driver-application.md)  
  
-   [SQL Server と通信する&#40;ODBC&#41;](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [クエリの実行&#40;ODBC&#41;](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [結果の処理&#40;ODBC&#41;](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [カーソルを使用して&#40;ODBC&#41;](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [トランザクションを実行する&#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [エラーとメッセージの処理](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [ストアド プロシージャの実行](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [カタログ関数の使用](using-catalog-functions.md)  
  
-   [一括コピー操作を実行する&#40;ODBC&#41;](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [text 列と image 列の管理](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [ODBC ドライバー パフォーマンスのプロファイル](profiling-odbc-driver-performance.md)  
  
-   [テーブル値パラメーター &#40;ODBC&#41;](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [日付と時刻の強化&#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [大きな CLR ユーザー定義型&#40;ODBC&#41;](large-clr-user-defined-types-odbc.md)  
  
-   [FILESTREAM のサポート&#40;ODBC&#41;](filestream-support-odbc.md)  
  
-   [サービス プリンシパル名&#40;Spn&#41;クライアント接続で&#40;ODBC&#41;](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [スパース列のサポート&#40;ODBC&#41;](sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41;リファレンス](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [ODBC の使用法に関するトピック](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../sql-server-native-client-programming.md)   
 [SQL Server Native Client のインストール](../applications/installing-sql-server-native-client.md)  
  
  
