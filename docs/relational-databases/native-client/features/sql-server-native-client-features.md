---
title: SQL Server Native Client の機能 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8821a8c0c0ef095d46682e0e1ad07e1cd74be16b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761323"
---
# <a name="sql-server-native-client-features"></a>SQL Server Native Client の機能
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、Windows Data Access Components (WDAC、以前の Microsoft Data Access Components) の機能を公開するだけでなく、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の機能を公開するための機能が数多く実装されています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [文字変換処理での ODBC ドライバーの動作の変更](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client で変更された動作について説明します。  
  
 [データベース ミラーリングの使用](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、ミラー化されたデータベースの使用をサポートする方法について説明します。ミラー化されたデータベースは、スタンバイサーバーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースのコピー (ミラー) を保持することができます。  
  
 [非同期操作の実行](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で、非同期操作をサポートする方法について説明します。非同期操作では、呼び出し側のスレッドをブロックせずに直ちに操作を戻すことができます。  
  
 [複数のアクティブな結果セット &#40;MARS&#41; の使用](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client が複数のアクティブな結果セット (MARS) をサポートするしくみについて説明します。 MARS では、単一のデータベース接続を使用して、複数の結果セットを実行したり受け取ったりできます。  
  
 [XML データ型の使用](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で XML データ型をサポートする方法について説明します。XML データ型とは、XML ベースのデータ型で、列の型、変数の型、パラメーターの型、または関数の戻り値の型として使用できます。  
  
 [ユーザー定義型の使用](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ユーザー定義型 (UDT) をサポートする方法について説明します。 UDT を使用すると、オブジェクトやカスタムデータ構造を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに格納できるため、SQL 型システムが拡張されます。  
  
 [大きな値の型の使用](../../../relational-databases/native-client/features/using-large-value-types.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で大きな値のデータ型をサポートする方法について説明します。大きな値のデータ型とは、ラージ オブジェクト (LOB) データ型のことです。  
  
 [プログラムによるパスワードの変更](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で、有効期限が切れたパスワードの処理をサポートする方法について説明します。この処理により、管理者の手を煩わせることなく、クライアント側でパスワードを変更できるようになりました。  
  
 [スナップショット分離を使用した作業](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で、行のバージョン管理の機能強化をサポートする方法について説明します。この機能強化では、リーダーとライターとの間で発生するブロックを回避することにより、データベースのパフォーマンスが向上します。  
  
 [クエリ通知の操作](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で、行セット変更時のコンシューマーへの通知をサポートする方法について説明します。  
  
 [一括コピー操作の実行](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 Native Client が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のテーブルまたはビューとの間で大量のデータを転送できるようにする一括コピー操作をサポート [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 方法について説明します。  
  
 [検証を伴わない暗号化の使用](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用して、証明書の検証をせずに、サーバーに送信されるデータを暗号化する方法について説明します。  
  
 [テーブル値パラメーター &#40;SQL Server Native Client&#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client によるテーブル値パラメーターのサポートについて説明します。  
  
 [大きな CLR ユーザー定義型](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 大きな共通言語ランタイム (CLR) ユーザー定義型 (UDT) のサポートについて説明します。  
  
 [FILESTREAM のサポート](../../../relational-databases/native-client/features/filestream-support.md)  
 拡張 FILESTREAM 機能の Native Client のサポート [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] について説明します。  
  
 [クライアント接続でのサービス プリンシパル名 &#40;SPN&#41; のサポート](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 あらゆるプロトコルでの相互認証を可能にする、サービス プリンシパル名 (SPN) のサポート強化について説明します。  
  
 [SQL Server Native Client におけるスパース列のサポート](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client によるスパース列のサポートについて説明します。  
  
 [日付と時刻の強化機能](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 日付と時刻のデータ型のために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client に追加されたサポートについて説明します。  
  
 [メタデータの検出](../../../relational-databases/native-client/features/metadata-discovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] で行われたメタデータ検出の機能強化について説明します。  
  
 [SQL Server Native Client 11.0 での UTF-16 のサポート](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] で導入された動作の変更について説明します。 列の結果または出力パラメーターをバインドするときに固定長バッファーを指定する場合、および終端文字の前にバッファーに書き込まれる**wchar**文字がサロゲートペアの上位サロゲートコードポイントである場合、次の**wchar**の場合は。文字は下位サロゲートコードポイントです。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、上位サロゲートコードポイントがバッファーに追加されません。  
  
 [SQL Server Native Client の HADR サポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] に追加された高可用性のディザスター リカバリー機能をアプリケーションで利用するための構成方法について説明します。  
  
 [拡張イベント ログの診断情報へのアクセス](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の機能強化とリング バッファーおよび XEvent ログの診断情報にアクセスできるデータ トレースについて説明します。  
  
 [SQL Server Native Client における LocalDB のサポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client による LocalDB 機能のサポートについて説明します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC の操作方法に関するトピック](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB の使用法に関するトピック](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [SQL Server Native Client のインストール](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
