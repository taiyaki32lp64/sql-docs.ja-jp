---
title: SQL Server Native Client (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, about SQL Server Native Client OLE DB provider
- OLE DB, SQL Server Native Client OLE DB provider
- data access [SQL Server Native Client], OLE DB
- SQLNCLI, OLE DB
- OLE DB
- SQL Server Native Client OLE DB provider
- SQL Server Native Client, OLE DB
ms.assetid: da846da4-ec19-4a4f-81fb-7d5a2b2bf80a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a895b11786628a1a43103607337d4d972d81cdfd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031854"
---
# <a name="sql-server-native-client-ole-db"></a>SQL Server Native Client (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー (SQLNCLI) は、低レベルの COM API のデータにアクセスするために使用します。 高いパフォーマンスが必要なツール、ユーティリティ、または低レベルのコンポーネントを開発する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの使用をお勧めします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の表形式のデータ ストリーム (TDS) プロトコルに直接アクセスするパフォーマンスの高いネイティブ プロバイダーです。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続するアプリケーションに OLE DB サポートを提供します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、OLE DB バージョン 2.0 準拠のプロバイダー。  
 
> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB (SQLNCLI) は非推奨と新しい開発作業で使用する勧めしません。 代わりに、新しい使用[Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) server の最新の機能と更新されます。
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [SQL Server Native Client OLE DB プロバイダー アプリケーションの作成](../../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
-   [データ ソース オブジェクト&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
-   [[コマンド]](../../../relational-databases/native-client-ole-db-commands/commands.md)  
  
-   [行セット](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
-   [ストアド プロシージャ](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
-   [BLOB と OLE オブジェクト](../../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)  
  
-   [テーブルとインデックス](../../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
-   [データ型&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
-   [スキーマ行セットのサポート &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
-   [テーブル値パラメーター &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)  
  
-   [日付と時刻の強化機能 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
-   [大きな CLR ユーザー定義型 &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md)  
  
-   [FILESTREAM のサポート&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [トランザクション](../../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
-   [エラー](../../../relational-databases/native-client-ole-db-errors/errors.md)  
  
-   [クライアント接続 &#40;OLE DB&#41; でのサービス プリンシパル名 &#40;SPNs&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
-   [スパース列のサポート &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)  
  
-   [SQL Server Native Client &#40;OLE DB&#41;リファレンス](../../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)  
  
-   [OLE DB の使用法に関するトピック](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
