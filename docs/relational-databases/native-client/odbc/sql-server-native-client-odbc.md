---
title: SQL Server Native Client (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 48fc5ccd2973a530010975171a90f35a2f18a7e7
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73760247"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC は、リレーショナル データベースまたは索引順次アクセス方式 (ISAM) データベースのデータへのアクセスに使用するアプリケーション プログラミング インターフェイス (API) の標準的な定義です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と通信する C および C++ アプリケーションの作成に使用されるネイティブ API の 1 つとして、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを介して ODBC をサポートしています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用して作成された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プログラムは、C 関数の呼び出しによって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と通信します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の ODBC 関数が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーに実装されています。 ドライバーは、SQL ステートメントを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に渡し、ステートメントの結果をアプリケーションに返します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは Microsoft Win32 ODBC 3.51 仕様に準拠しています。 以前のバージョンの ODBC を使用して作成されているアプリケーションは、ODBC 3.51 仕様で定義されている方法に従ってサポートされます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [データ ソース名と 64 ビット オペレーティング システム](../../../relational-databases/native-client/odbc/data-source-names-and-64-bit-operating-systems.md)  
  
-   [SQL Server Native Client ODBC ドライバー アプリケーションの作成](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
-   [SQL Server &#40;ODBC との通信&#41;](../../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [クエリ&#40;の実行 ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [結果&#40;の処理 (ODBC)&#41;](../../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
-   [カーソル&#40;を使用した ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [トランザクション&#40;の実行 ODBC&#41;](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
-   [エラーとメッセージの処理](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [ストアド プロシージャの実行](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [カタログ関数の使用](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  
  
-   [一括コピー操作&#40;の実行 (ODBC)&#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [text 列と image 列の管理](../../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [ODBC ドライバー パフォーマンスのプロファイル](../../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
-   [テーブル値パラメーター &#40;の ODBC&#41;](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [日付と時刻の&#40;機能強化 ODBC&#41;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [大きな CLR ユーザー定義型&#40;ODBC&#41;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)  
  
-   [FILESTREAM サポート&#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [クライアント接続&#40;の&#40;サービス&#41;プリンシパル名 spn ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [スパース列で&#40;ODBC がサポート&#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41;リファレンス](https://msdn.microsoft.com/library/06b7edee-8636-49d9-9b5c-2c710bf4fa2d)  
  
-   [ODBC の使用法に関するトピック](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [SQL Server Native Client のインストール](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
