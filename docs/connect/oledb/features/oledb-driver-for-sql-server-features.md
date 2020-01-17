---
title: SQL Server 機能の OLE DB ドライバー |Microsoft Docs
description: OLE DB Driver for SQL Server の機能
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 46f7de1e57686a0f54368407580d90236152d147
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989049"
---
# <a name="ole-db-driver-for-sql-server-features"></a>OLE DB Driver for SQL Server の機能
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server では、Windows Data Access Components (WDAC。以前の Microsoft Data Access Components) の機能を公開するだけでなく、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の機能を公開するための機能が数多く実装されています。  
  
## <a name="in-this-section"></a>このセクションの内容    
 [データベース ミラーリングの使用](../../oledb/features/using-database-mirroring.md)  
 OLE DB Driver for SQL Server で、ミラー化されたデータベースの使用をサポートする方法について説明します。ミラー化されたデータベースによって、スタンバイ サーバー上に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースのコピー (ミラー) を保持することができます。  
  
 [非同期操作の実行](../../oledb/features/performing-asynchronous-operations.md)  
 OLE DB Driver for SQL Server で、非同期操作をサポートする方法について説明します。非同期操作では、呼び出し側のスレッドをブロックせずに直ちに操作を戻すことができます。  

[Azure Active Directory の使用](using-azure-active-directory.md)  
OLE DB driver 18.2.1 で導入された新しい認証方法について説明します。これにより、より安全な既定の設定が可能になり、フェデレーション id を使用して Azure SQL Database のインスタンスに接続できるようになります。

 [複数のアクティブな結果セット &#40;MARS&#41; の使用](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 OLE DB Driver for SQL Server が複数のアクティブな結果セット (MARS) をサポートする方法について説明します。 MARS では、単一のデータベース接続を使用して、複数の結果セットを実行したり受け取ったりできます。  
  
 [XML データ型の使用](../../oledb/features/using-xml-data-types.md)  
 OLE DB Driver for SQL Server で XML データ型をサポートする方法について説明します。XML データ型とは、XML ベースのデータ型で、列の型、変数の型、パラメーターの型、または関数の戻り値の型として使用できます。  
  
 [ユーザー定義型の使用](../../oledb/features/using-user-defined-types.md)  
 OLE DB Driver for SQL Server でユーザー定義型 (UDT) をサポートする方法について説明します。UDT を使用すると、オブジェクトやカスタムのデータ構造を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに格納できるため、SQL の型システムが拡張されます。  
  
 [大きな値の型の使用](../../oledb/features/using-large-value-types.md)  
 OLE DB Driver for SQL Server が、ラージオブジェクトデータ型 (LOB) である大きな値のデータ型をサポートする方法について説明します。  
  
 [プログラムによるパスワードの変更](../../oledb/features/changing-passwords-programmatically.md)  
 OLE DB Driver for SQL Server で、有効期限が切れたパスワードの処理をサポートする方法について説明します。この処理により、管理者の手を煩わせることなく、クライアント側でパスワードを変更できるようになりました。  
  
 [スナップショット分離を使用した作業](../../oledb/features/working-with-snapshot-isolation.md)  
 OLE DB Driver for SQL Server で、行のバージョン管理の機能強化をサポートする方法について説明します。この機能強化では、リーダーとライターとの間で発生するブロックを回避することにより、データベースのパフォーマンスが向上します。  
  
 [クエリ通知の操作](../../oledb/features/working-with-query-notifications.md)  
 OLE DB Driver for SQL Server が行セットの変更に関するコンシューマー通知をサポートする方法について説明します。  
  
 [一括コピー操作の実行](../../oledb/features/performing-bulk-copy-operations.md)  
 OLE DB Driver for SQL Server で一括コピー操作をサポートする方法について説明します。一括コピー操作を使用すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のテーブルやビューを対象とした大量データのやりとりが可能になります。  
  
 [検証を伴わない暗号化の使用](../../oledb/features/using-encryption-without-validation.md)  
 OLE DB Driver for SQL Server を使用して、証明書を検証せずにサーバーに送信されるデータを暗号化する方法について説明します。  
  
 [テーブル値パラメーター &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 テーブル値パラメーターの SQL Server サポートの OLE DB ドライバーについて説明します。  
  
 [大きな CLR ユーザー定義型](../../oledb/features/large-clr-user-defined-types.md)  
 大きな共通言語ランタイム (CLR) ユーザー定義型 (UDT) のサポートについて説明します。  
  
 [FILESTREAM のサポート](../../oledb/features/filestream-support.md)  
 拡張された FILESTREAM 機能の SQL Server サポートの OLE DB ドライバーについて説明します。  
  
 [クライアント接続でのサービス プリンシパル名 &#40;SPN&#41; のサポート](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 あらゆるプロトコルでの相互認証を可能にする、サービス プリンシパル名 (SPN) のサポート強化について説明します。  
  
 [OLE DB Driver for SQL Server のスパース列のサポート](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 スパース列の SQL Server サポートの OLE DB ドライバーについて説明します。  
  
 [日付と時刻の強化機能](../../oledb/features/date-and-time-improvements.md)  
 日付と時刻のデータ型の SQL Server の OLE DB ドライバーに追加されたサポートについて説明します。  
  
 [メタデータの検出](../../oledb/features/metadata-discovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] で行われたメタデータ検出の機能強化について説明します。  
  
 [OLE DB Driver for SQL Server の UTF-16 のサポート](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] で導入された動作の変更について説明します。 列の結果または出力パラメーターをバインドするときに固定長バッファーを指定した場合、終端文字の前にバッファーに書き込まれる **wchar** 文字がサロゲート ペアの上位サロゲート コード ポイントである場合、および次の **wchar** 文字が下位サロゲート コード ポイントである場合は、OLE DB Driver for SQL Server はバッファーに上位サロゲート コード ポイントを追加しません。  
 
 [OLE DB Driver for SQL Server の UTF-8 のサポート](../../oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
 Utf-8 でエンコードされたデータを使用する場合にユーザーが実行する必要がある、UTF-8 サーバーのエンコードと構成に関する予防策について説明します。
  
 [OLE DB Driver for SQL Server の高可用性、ディザスター リカバリーに関するサポート](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] に追加された高可用性のディザスター リカバリー機能をアプリケーションで利用するための構成方法について説明します。  
  
 [拡張イベント ログの診断情報へのアクセス](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 OLE DB Driver for SQL Server の機能強化とリング バッファーおよび XEvent ログの診断情報にアクセスできるデータ トレースについて説明します。  
  
 [LocalDB 用 OLE DB Driver for SQL Server のサポート](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 LocalDB 機能の SQL Server サポートの OLE DB ドライバーについて説明します。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server](../../oledb/oledb-driver-for-sql-server.md)      
 [OLE DB の使用法に関するトピック](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [OLE DB Driver for SQL Server のインストール](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
