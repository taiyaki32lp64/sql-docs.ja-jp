---
title: トランザクション ログ ファイルのサイズの管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2ebcd653adebed5541b1d2cdf814f638d0af683
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144333"
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>トランザクション ログ ファイルのサイズの管理
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのトランザクション ログは、必要に応じて、その物理ログ ファイルを物理的に圧縮または展開することができます。 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のトランザクション ログ サイズの監視、トランザクション ログの圧縮、トランザクション ログ ファイルの追加と拡大、 **tempdb** トランザクション ログ増加率の最適化、トランザクション ログ ファイルのサイズ拡大の管理の方法について説明します。  
  
  
##  <a name="MonitorSpaceUse"></a> モニターのログ領域の使用  
 ログ領域の使用量は、DBCC SQLPERF (LOGSPACE) を使用して監視することができます。 このコマンドは、現在使用されているログ領域の量に関する情報を返し、いつトランザクション ログを切り捨てる必要があるかを示します。 詳細については、「 [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)」を参照してください。 ログ ファイルの現在のサイズ、最大サイズ、およびファイルの自動拡張オプションについては、**sys.database_files** にある、そのログ ファイルに関する **size**、**max_size**、**growth** の各列も使用できます。 詳細については、「[sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)」を参照してください。  
  
> [!IMPORTANT]  
>  ログ ディスクが過負荷にならないようにすることをお勧めします。  
  
  
##  <a name="ShrinkSize"></a> ログ ファイルのサイズを縮小します。  
 物理ログ ファイルの物理サイズを削減するには、ログ ファイルを圧縮する必要があります。 トランザクション ログ ファイルに不要な未使用領域が含まれていることがわかっている場合にはこの方法が有効です。 ログ ファイルの圧縮を実行できるのは、データベースがオンラインで、1 つ以上の仮想ログ ファイルが解放されている間だけです。 場合によっては、次のログの切り捨てまでログを圧縮できないことがあります。  
  
> [!NOTE]  
>  実行時間の長いトランザクションなど、長期間にわたって仮想ログ ファイルがアクティブなままになる要因があると、ログの圧縮が制限されたり、ログがまったく圧縮できないことがあります。 ログの切り捨てが遅れる要因については、「[トランザクション ログ &#40;SQL Server&#41;](the-transaction-log-sql-server.md)」を参照してください。  
  
 ログ ファイルを圧縮すると、論理ログのどの部分も保持しない 1 つまたは複数の仮想ログ ファイル (つまり、 *非アクティブな仮想ログ ファイル*) が削除されます。 トランザクション ログ ファイルを圧縮すると、ログ ファイルが目的のサイズにできるだけ近いサイズに縮小されるように、非アクティブな仮想ログ ファイルがログ ファイルの末尾から削除されます。  
  
 **(データベース ファイルを圧縮せずにログ ファイルを圧縮するには**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)  
  
-   [ファイルの圧縮](../databases/shrink-a-file.md)  
  
 **ログ ファイルの圧縮イベントを監視するには**  
  
-   [Log File Auto Shrink Event Class](../event-classes/log-file-auto-shrink-event-class.md)。  
  
 `To monitor log space`  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) (ログ ファイルまたはファイルの **size**、**max_size**、**growth** 列を参照してください。)  
  
> [!NOTE]  
>  データベースおよびログ ファイルの圧縮は、自動的に行われるように設定できます。 ただし、自動圧縮は推奨されず、`autoshrink` データベース プロパティは既定で FALSE に設定されています。 `autoshrink` を TRUE に設定すると、ファイル領域の 25% を超える領域が未使用の場合にのみ、自動圧縮によってファイルのサイズが縮小されます。 ファイルは、ファイル領域の 25% のみが未使用領域になるサイズ、またはファイルの元のサイズの、どちらか大きい方のサイズまで圧縮されます。 設定を変更する方法については、`autoshrink`プロパティを参照してください[データベースのプロパティ表示または変更](../databases/view-or-change-the-properties-of-a-database.md)-を使用して、 **Auto Shrink**プロパティを**オプション**ページ、または[ALTER DATABASE SET Options &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)-AUTO_SHRINK オプションを使用します。  
  
  
##  <a name="AddOrEnlarge"></a> 追加またはログ ファイルを拡大  
 既存のログ ファイルを拡大するか (ディスク領域が十分にある場合)、別のディスク上にあるデータベースにログ ファイルを追加することによって、領域を確保することもできます。  
  
-   データベースにログ ファイルを追加するには、ALTER DATABASE ステートメントの ADD LOG FILE 句を使用します。 ログ ファイルを追加すると、ログを大きくすることができます。  
  
-   ログ ファイルを拡大するには、ALTER DATABASE ステートメントの MODIFY FILE 句を使用し、SIZE および MAXSIZE 構文を指定します。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。  
  
  
##  <a name="tempdbOptimize"></a> Tempdb トランザクション ログのサイズを最適化します。  
 サーバー インスタンスを再起動すると、 **tempdb** データベースのトランザクション ログのサイズが、元の自動拡張前のサイズに変更されます。 これにより、 **tempdb** のトランザクション ログのパフォーマンスが低下することがあります。 このオーバーヘッドは、サーバー インスタンスを起動または再起動した後、 **tempdb** のトランザクション ログのサイズを増やすことで回避できます。 詳細については、「 [tempdb Database](../databases/tempdb-database.md)」をご覧ください。  
  
  
##  <a name="ControlGrowth"></a> トランザクション ログ ファイルのサイズ拡大を管理します。  
 トランザクション ログ ファイルのサイズの拡張を管理するには、[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) ステートメントを使用します。 次の点に注意してください。  
  
-   現在のサイズを KB、MB、GB、および TB 単位で変更する場合は、SIZE オプションを使用します。  
  
-   拡張増分値で変更するには、FILEGROWTH オプションを使用します。 0 は、自動拡張がオフで、領域を追加できないことを示します。 ログ ファイルの自動拡張の増分値が小さい場合も、パフォーマンスが低下することがあります。 ログ ファイルの拡張増分値は、拡張を頻繁に行わなくても済むように十分な大きさにする必要があります。 通常は、既定の拡張増分値 (10%) が適しています。  
  
     ログ ファイルのファイル拡張プロパティを変更する方法の詳細については、次を参照してください。 [ALTER DATABASE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)します。  
  
-   ログ ファイルの最大サイズを KB、MB、GB、および TB 単位で制御するか、拡張値を UNLIMITED に設定するには、MAXSIZE オプションを使用します。  
  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [満杯になったトランザクション ログのトラブルシューティング &#40;SQL Server エラー 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  
