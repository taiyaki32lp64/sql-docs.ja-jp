---
title: トランザクション ログ ファイルのサイズの管理 | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
- manage log size
- log size, manage
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ff886f2eea70b010a2e64513cd561cf7f78d8dee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084019"
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>トランザクション ログ ファイルのサイズの管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
このトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のトランザクション ログ サイズの監視、トランザクション ログの圧縮、トランザクション ログ ファイルの追加と拡大、**tempdb** トランザクション ログ増加率の最適化、トランザクション ログ ファイルのサイズ拡大の管理の方法について説明します。  

##  <a name="MonitorSpaceUse"></a>ログ領域の使用量の監視  
[sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) を利用し、ログ領域の使用量を監視します。 この DMV は、現在使用されているログ領域の量に関する情報を返し、いつトランザクション ログを切り捨てる必要があるかを示します。 

ログ ファイルの現在のサイズ、最大サイズ、およびファイルの自動拡張オプションについては、[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) にある、そのログ ファイルに関する **size**、**max_size**、**growth** の各列も使用できます。  
  
> [!IMPORTANT]
> ログ ディスクの過負荷を避けてください。 ログ ストレージがトランザクション負荷の [IOPS](https://wikipedia.org/wiki/IOPS) 要件と短い待ち時間要件に対応できることを確認してください。 
  
##  <a name="ShrinkSize"></a> ログ ファイルのサイズを圧縮する  
 物理ログ ファイルの物理サイズを削減するには、ログ ファイルを圧縮する必要があります。 トランザクション ログ ファイルに未使用領域が含まれていることがわかっている場合にはこの方法が有効です。 ログ ファイルの圧縮を実行できるのは、データベースがオンラインで、1 つ以上の[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) が解放されている間だけです。 場合によっては、次のログの切り捨てまでログを圧縮できないことがあります。  
  
> [!NOTE]
> 実行時間の長いトランザクションなど、長期間にわたって [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) がアクティブなままになる要因があると、ログの圧縮が制限されたり、ログがまったく圧縮できないことがあります。 詳細については、「[ログの切り捨てが遅れる原因となる要因](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)」を参照してください。  
  
ログ ファイルを圧縮すると、論理ログのどの部分も保持しない 1 つまたは複数の [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) (つまり、*非アクティブな VLF*) が削除されます。 トランザクション ログ ファイルを圧縮すると、ログ ファイルが目的のサイズにできるだけ近いサイズに縮小されるように、非アクティブな VLF がログ ファイルの末尾から削除されます。 

> [!IMPORTANT]
> トランザクション ログを圧縮する前に、[ログの切り捨てが遅れる原因となる要因](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)に留意してください。 ログの圧縮後、ストレージ領域が再び必要になると、トランザクション ログが再び増え、その分のパフォーマンスのオーバーヘッドが発生します。 詳細については、このトピックの「[推奨事項](#Recommendations)」を参照してください。
  
 **データベース ファイルを圧縮せずにログ ファイルを圧縮する**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [ファイルの圧縮](../../relational-databases/databases/shrink-a-file.md)  
  
 **ログ ファイルの圧縮イベントを監視する**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)。  
  
 **ログ領域の監視**  
  
-   [sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) (ログ ファイルまたはファイルの **size**、**max_size**、**growth** 列を参照してください。)  
  
##  <a name="AddOrEnlarge"></a> ログ ファイルの追加または拡大  
既存のログ ファイルを拡大するか (ディスク領域が十分にある場合)、通常、別のディスク上にあるデータベースにログ ファイルを追加することによって、領域を確保することができます。 ログ領域が不足し、さらにログ ファイルが保存されているボリュームでディスク容量が不足しない限り、トランザクション ログ ファイルは 1 つで十分です。   
  
-   データベースにログ ファイルを追加するには、`ALTER DATABASE` ステートメントの `ADD LOG FILE` 句を使用します。 ログ ファイルを追加すると、ログを大きくすることができます。  
-   ログ ファイルを大きくするには、`ALTER DATABASE` ステートメントの `MODIFY FILE` 句を使用します。`SIZE` および `MAXSIZE` 構文を指定します。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41; の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」を参照してください。  

詳細については、このトピックの「[推奨事項](#Recommendations)」を参照してください。
    
##  <a name="tempdbOptimize"></a> tempdb トランザクション ログのサイズの最適化  
 サーバー インスタンスを再起動すると、 **tempdb** データベースのトランザクション ログのサイズが、元の自動拡張前のサイズに変更されます。 これにより、 **tempdb** のトランザクション ログのパフォーマンスが低下することがあります。 
 
 このオーバーヘッドは、サーバー インスタンスを起動または再起動した後、 **tempdb** のトランザクション ログのサイズを増やすことで回避できます。 詳細については、「 [tempdb Database](../../relational-databases/databases/tempdb-database.md)」をご覧ください。  
  
##  <a name="ControlGrowth"></a> トランザクション ログ ファイルのサイズ拡大の管理  
 トランザクション ログ ファイルのサイズ拡大を管理するには、[ALTER DATABASE &#40;Transact-SQL&#41; の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) ステートメントを使用します。 次のことを考慮してください。  
  
-   現在のサイズを KB、MB、GB、TB 単位で変更するには、`SIZE` オプションを使用します。  
-   拡張増分値で変更するには、`FILEGROWTH` オプションを使用します。 0 は、自動拡張がオフで、領域を追加できないことを示します。  
-   ログ ファイルの最大サイズを KB、MB、GB、TB 単位で制御するか、拡張値を UNLIMITED に設定するには、`MAXSIZE` オプションを使用します。  

詳細については、このトピックの「[推奨事項](#Recommendations)」を参照してください。

## <a name="Recommendations"></a> 推奨事項
トランザクション ログ ファイルを使用して作業するときの一般的な推奨事項を次に示します。

-   トランザクション ログの自動拡張 (autogrow) の増分は `FILEGROWTH` オプションで設定されますが、トランザクションの作業負荷に対して常に余裕を持たせられるよう、十分な量にする必要があります。 ログ ファイルの拡張増分値は、拡張を頻繁に行わなくても済むように十分な大きさにする必要があります。 トランザクション ログのサイズは、次の時間のログ量を監視することで正しく判断できます。
    -  完全バックアップに必要な時間。完全バックアップが終わるまでログはバックアップされないためです。
    -  最も大規模なインデックス保守管理に必要な時間。
    -  データベースで最も大規模な一括処理を実行するときに必要な時間。

-   `FILEGROWTH` オプションを利用し、データとログのファイルに**自動拡張**を設定するとき、**パーセンテージ**より**サイズ**で設定したほうが増加の制御に優れている場合があります。割合は常に増加する量であるためです。
    -  トランザクション ログでは[ファイルの瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)を活用できないことに留意してください。そのため、ログ拡張の回数増加が重要になります。 
    -  ベスト プラクティスとしては、トランザクション ログに対して `FILEGROWTH` オプションの値を 1,024 MB 以上に設定しないでください。 `FILEGROWTH` オプションの既定値:  
  
      |バージョン|[既定値]|  
      |-------------|--------------------|  
      |[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降|データ 64 MB。 ログ ファイル 64 MB。|  
      |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降|データ 1 MB。 ログ ファイル 10%。|  
      |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] の前|データ 10%。 ログ ファイル 10%。|  

-   増分が少ないと小さな [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) が過度に生成され、パフォーマンスが低下します。 指定されたインスタンスにおいて、すべてのデータベースの現在のトランザクション ログ サイズに最適な VLF 配布と必要なサイズを得るために必要な増分を決定するには、この[スクリプト](https://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)をご覧ください。

-   増分が大きいと大きな [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) が生成される回数が極めて少なく、やはりパフォーマンスに影響が出ます。 指定されたインスタンスにおいて、すべてのデータベースの現在のトランザクション ログ サイズに最適な VLF 配布と必要なサイズを得るために必要な増分を決定するには、この[スクリプト](https://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)をご覧ください。 

-   自動拡張を有効にしても、増加が遅く、クエリのニーズを満たせなければ、トランザクション ログがいっぱいになったというメッセージが表示されます。 増分変更の詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41; の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」を参照してください。

-   データベースにログ ファイルが複数存在すると、パフォーマンスが向上しません。トランザクション ログ ファイルでは、同じファイル グループのデータ ファイルのように[比例配分](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill)を利用することがないためです。  

-   ログ ファイルは自動的に圧縮するように設定できます。 ただし、これは**推奨されません**。**auto_shrink** データベース プロパティは既定で FALSE に設定されています。 **auto_shrink** を TRUE に設定すると、ファイル領域の 25% を超える領域が未使用の場合にのみ、自動圧縮によってファイルのサイズが縮小されます。 
    -   ファイルは、ファイル領域の 25% のみが未使用領域になるサイズ、またはファイルの元のサイズの、どちらか大きい方のサイズまで圧縮されます。 
    -   **auto_shrink** プロパティの設定変更については、「[データベースのプロパティの表示または変更](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)」と「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。 
  
## <a name="see-also"></a>参照  
[BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
[満杯になったトランザクション ログのトラブルシューティング &#40;SQL Server エラー 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)    
[SQL Server トランザクション ログのアーキテクチャと管理ガイドのトランザクション ログ バックアップ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)    
[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)    
[ALTER DATABASE &#40;Transact-SQL&#41; の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)
