---
title: バックアップの圧縮 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: af3e8d9184b12a726361643c563402242c6b04cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876799"
---
# <a name="backup-compression-sql-server"></a>バックアップの圧縮 (SQL Server)
  このトピックでは、バックアップの圧縮の制限、パフォーマンス面のトレードオフ、バックアップの圧縮の構成、圧縮比率など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップの圧縮について説明します。  
  
> [!NOTE]  
>  情報ののどのエディション[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]バックアップの圧縮のサポートを参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。 圧縮されたバックアップは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降の各エディションで復元できます。  
  
  
##  <a name="Benefits"></a> 利点  
  
-   圧縮されたバックアップは、同じデータの圧縮されていないバックアップよりも小さいため、バックアップを圧縮すると一般には必要なデバイス I/O が少なくなり、通常はバックアップの速度が大きく短縮されます。  
  
     詳細については、このトピックの「 [バックアップの圧縮がパフォーマンスに与える影響](#PerfImpact)」を参照してください。  
  
  
##  <a name="Restrictions"></a> 制限  
 圧縮されたバックアップには次の制限が適用されます。  
  
-   圧縮されたバックアップと圧縮されていないバックアップを 1 つのメディア セット内に共存させることはできません。  
  
-   以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、圧縮されたバックアップを読み取ることができません。  
  
-   圧縮された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのテープを複数の Ntbackup で共有することはできません。  
  
  
##  <a name="PerfImpact"></a> バックアップの圧縮がパフォーマンスに与える影響  
 既定の設定では、圧縮によって CPU 使用率が著しく増加し、圧縮処理によって CPU がさらに消費されるために、同時に実行される操作が悪影響を受ける場合があります。 このため、[リソース ガバナー](../resource-governor/resource-governor.md)によって CPU 使用率が制限されるセッションでは、優先度の低い圧縮バックアップを作成することができます。 詳細については、このトピックの「 [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)によって CPU 使用率が制限されるセッションでは、優先度の低い圧縮バックアップを作成することができます。  
  
 バックアップ I/O パフォーマンスの実態を把握するためには、次のようなパフォーマンス カウンターを評価することで、デバイスに対するバックアップ I/O を特定できます。  
  
-   物理ディスク カウンターなどの Windows I/O パフォーマンス カウンター  
  
-   **SQLServer:Backup Device** オブジェクトの [Device Throughput Bytes/sec](../performance-monitor/sql-server-backup-device-object.md) カウンター  
  
-   **SQLServer:Databases** オブジェクトの [Backup/Restore Throughput/sec](../performance-monitor/sql-server-databases-object.md) カウンター  
  
 Windows カウンターの詳細については、Windows ヘルプを参照してください。 SQL Server カウンターの使用方法の詳細については、「 [SQL Server オブジェクトの使用](../performance-monitor/use-sql-server-objects.md)」をご覧ください。  
  
  
##  <a name="CompressionRatio"></a> 圧縮されたバックアップの圧縮比率の計算  
 バックアップの圧縮比率を計算するには、 **backupset** 履歴テーブルの **backup_size** 列と [compressed_backup_size](/sql/relational-databases/system-tables/backupset-transact-sql) 列にある値を次のように使用します。  
  
 **backup_size**:**compressed_backup_size**  
  
 たとえば、圧縮比率が 3:1 の場合、ディスク領域を約 66% 節約できることを意味します。 これらの列に対するクエリを実行するには、次の Transact-SQL ステートメントを使用できます。  
  
```  
SELECT backup_size/compressed_backup_size FROM msdb..backupset;  
```  
  
 圧縮されたバックアップの圧縮比率は、圧縮対象のデータによって異なります。 実際の圧縮比率は、さまざまな要因の影響を受けます。 主な要因は次のとおりです。  
  
-   データの型  
  
     文字データは、他のデータ型よりも圧縮されます。  
  
-   ページ上の各行のデータの一貫性  
  
     一般に、ページ内の複数の行でフィールドに同じ値が格納されている場合、その値が大幅に圧縮される可能性があります。 これに対して、ランダムなデータが格納されたデータベースや、各ページにサイズの大きい行が 1 つだけ含まれているデータベースの場合、圧縮されたバックアップは、圧縮されていないバックアップとそれほど変わらないサイズになります。  
  
-   データが暗号化されているかどうか  
  
     暗号化されたデータは、暗号化されていない同等のデータより、圧縮比率が大幅に下がります。 透過的なデータ暗号化を使用してデータベース全体を暗号化すると、バックアップを圧縮しても、サイズが大幅に減少することはありません。  
  
-   データベースが圧縮されているかどうか  
  
     データベースが圧縮されている場合、バックアップを圧縮しても、サイズが大幅に減少することはありません。  
  
  
##  <a name="Allocation"></a> バックアップ ファイルの使用領域の割り当て  
 圧縮されたバックアップの場合、最終的なバックアップ ファイルのサイズは、データをどれくらい圧縮できるかによりますが、それはバックアップ操作が終了するまで不明です。  そのため、既定では、圧縮を使用してデータベースをバックアップする場合、データベース エンジンはバックアップ ファイルのために事前割り当てアルゴリズムを使用します。 このアルゴリズムでは、バックアップ ファイルに、データベースのサイズに対する定義済みの割合のサイズを事前に割り当てます。 バックアップ操作中に、より多くの領域が必要になった場合は、データベース エンジンによってファイルが拡張されます。 バックアップ操作の終了時の最終的なサイズが、割り当てられた領域のサイズを下回る場合は、データベース エンジンによってファイルがバックアップの実際の最終的なサイズに縮小されます。  
  
 バックアップ ファイルが、最終的なサイズに達するために必要な分だけを拡張できるようにするには、トレース フラグ 3042 を使用します。 トレース フラグ 3042 は、バックアップ操作が既定のバックアップ圧縮の事前割り当てアルゴリズムを使用しないようにします。 このトレース フラグは、圧縮されたバックアップに実際に必要なサイズだけを割り当てることによって、容量を節約する必要がある場合に便利です。 ただし、このトレース フラグを使用すると、わずかなパフォーマンスの低下 (バックアップ操作の期間が長くなる可能性) が発生することがあります。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [バックアップの圧縮の構成 &#40;SQL Server&#41;](backup-compression-sql-server.md)  
  
-   [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-transact-sql)  
  
-   [DBCC TRACEOFF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceoff-transact-sql)  
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [トレース フラグ &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)  
  
  
