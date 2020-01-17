---
title: SQL Server データベースのバックアップと復元 | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c948c6e26655b8a450aee22f1ca6a6a178e0db76
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176325"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>SQL Server データベースのバックアップと復元
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをバックアップする利点、バックアップと復元に関する基本的な用語、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップと復元の方法を紹介します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップと復元のセキュリティに関する考慮事項についても取り上げます。 

> この記事では SQL Server のバックアップについて説明します。 SQL Server データベースをバックアップする具体的な手順については、「[バックアップの作成](#creating-backups)」を参照してください。
  
 SQL Server のバックアップと復元コンポーネントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納されている大切なデータを保護するうえで不可欠な保護対策を提供します。 致命的なデータ損失のリスクを最小限に抑えるには、データベースをバックアップして、データに対する変更内容を定期的に保存しておく必要があります。 バックアップと復元方法を十分に計画することで、さまざまな障害に起因するデータの損失からデータベースを保護できます。 バックアップを復元し、データベースを復旧するテストを実施することで、障害発生時に適切に対応できるようになります。
  
 バックアップを格納するローカル ストレージに加えて、SQL Server では、バックアップおよび Azure Blob Storage サービスからの復元がサポートされます。 詳細については、「 [Microsoft Azure Blob Storage サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。 Microsoft Azure BLOB ストレージ サービスを使用して格納したデータベース ファイルの場合、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] では、Azure スナップショットを使用してほぼ瞬時にバックアップし、より迅速に復元するためのオプションが提供されます。 詳細については、「 [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
##  <a name="why-back-up"></a>バックアップする理由  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをバックアップしたり、既存のバックアップの復元テストを実行したりできるほか、離れた安全な場所にバックアップのコピーを保管することによって、致命的な損失からデータを保護することができます。 **バックアップは、データを保護できる唯一の方法です。**

     データベースの有効なバックアップがあれば、次に示したようなさまざまな障害からデータを復旧することができます。  
  
    -   メディアの障害    
    -   ユーザー エラー (テーブルの誤削除など)    
    -   ハードウェア障害 (ディスク ドライブの損傷や、復旧の可能性のないサーバー障害など)    
    -   自然災害。 Azure Blob Storage サービスへの SQL Server バックアップを使用すると、オンプレミスの場所に影響する自然災害が発生した場合に使用できるように、オンプレミスの場所とは異なるリージョンにオフサイト バックアップを作成できます。  
  
-   また、データベースのバックアップは、サーバー間でのデータベースのコピー、 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] やデータベース ミラーリングのセットアップ、およびアーカイブなど、日常的な管理作業を行ううえでも便利です。  
  
##  <a name="glossary-of-backup-terms"></a>バックアップの用語集
 **バックアップ (back up)** (動詞)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータ レコードまたはそのトランザクション ログのログ レコードをコピーすることによって、**バックアップ (名詞)** を作成するプロセス。  
  
 **バックアップ (backup)** (名詞)  
 障害の発生後、データの復元と復旧に使用できるデータのコピー。 データベースのバックアップを使用して、コピー (データベース) を新しい場所に復元することもできます。  
  
**バックアップ デバイス (backup device)**  
 SQL Server のバックアップの書き込みと復元に使用されるディスクまたはテープ デバイス。 SQL Server のバックアップは、Azure Blob Storage サービスに書き込むこともできます。バックアップ先とバックアップ ファイルの名前を指定するには **URL** 形式を使用します。 詳細については、「 [Microsoft Azure Blob Storage サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
**バックアップ メディア (backup media)**  
 バックアップの書き込み先となる 1 つまたは複数のテープまたはディスク ファイル。  
  
**データ バックアップ (data backup)**  
 データのバックアップ。データベース全体 (データベース バックアップ)、データベースの一部 (部分バックアップ)、または一連のデータ ファイルやファイルグループ (ファイル バックアップ) の形式で存在します。  
  
**データベース バックアップ (database backup)**  
 データベースのバックアップ。 データベースの完全バックアップは、バックアップが完了した時点のデータベース全体を表します。 差分データベース バックアップには、最新の完全バックアップ以降に行われたデータベースへの変更のみが含まれます。  
  
**差分バックアップ (differential backup)**  
 データベース全体、データベースの一部、または一連のデータ ファイル (またはファイル グループ) の最新の完全バックアップ (差分ベース) をベースとし、その差分ベース以後に変更されたデータのみを含んだデータ バックアップ。  
  
**完全バックアップ (full backup)**  
 特定のデータベース (または一連のファイルやファイル グループ) 内のデータがすべて含まれ、さらに、データを復旧するために必要なログも含んだデータ バックアップ。  
  
**ログ バックアップ (log backup)**  
 前回のログ バックアップでバックアップされなかったすべてのログ レコードを含むトランザクション ログのバックアップ (完全復旧モデル)。  
  
**復元 (recover)**  
 安定し一貫した状態にデータベースを戻すこと。  
  
**復旧 (recovery)**  
 データベースをトランザクションの一貫性が保たれた状態にする、データベース起動時または RESTORE WITH RECOVERY 時のフェーズ。  
  
**復旧モデル (recovery model)**  
 データベースのトランザクション ログのメンテナンスを制御するデータベース プロパティ。 復旧モデルの種類は、単純、完全、および一括ログの 3 種類です。 データベースのバックアップと復元の要件は、その復旧モデルによって決まります。  
  
**復元 (restore)**  
 データを直近の状態まで戻す複数フェーズから成る処理。指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップからすべてのデータおよびログ ページを指定されたデータベースにコピーするフェーズと、バックアップにログとして記録されているすべてのトランザクションをロールフォワード (ログに記録されている変更を適用) するフェーズとで構成されます。  
  
 ##  <a name="backup-and-restore-strategies"></a>バックアップと復元の方法  
 データのバックアップと復元は、特定の環境向けにカスタマイズし、使用可能なリソースと連動させる必要があります。 したがって、信頼性が確保された状態でバックアップと復元を使用して復旧するには、バックアップと復元のストラテジが必要です。 バックアップと復元のストラテジ設計が良ければ、特定のビジネス要件を考慮しながら、データの可用性を最大にし、データ損失を最小限に抑えることができます。  
  
  > [!IMPORTANT] 
  > データベースとバックアップは異なるデバイスに置いてください。 そうしないと、データベースを置いているデバイスに障害が発生した場合、バックアップも使用できなくなります。 データとバックアップを異なるデバイスに置くと、バックアップの書き込みでもデータベースの運用でも I/O パフォーマンスが向上します。**  
  
 バックアップと復元のストラテジには、バックアップに関する部分と復元に関する部分があります。 ストラテジで扱うバックアップ部分では、バックアップの種類と頻度、バックアップに必要なハードウェアの性質と速度、バックアップのテスト方法、およびバックアップ メディアの保管場所と保管方法 (セキュリティ上の考慮事項も含む) を定義します。 ストラテジで扱う復元部分では、復元の実行責任者と、データベースの可用性とデータ損失の最小化という目標を達成するためにどのように復元を実行するのかを定義します。 バックアップと復元の手順をドキュメント化し、そのドキュメントを運用手順書に含めて保管することをお勧めします。  
  
 バックアップと復元について効果的なストラテジをデザインするには、慎重に計画、実装、およびテストする必要があります。 テストは必ず行ってください。 復元ストラテジに含まれるすべての組み合わせでバックアップを正常に復元できるようになって初めて、バックアップ ストラテジは完成します。 さまざまな要因を検討する必要があります。 その一部を次に示します。  
  
-   組織がそのデータベースに求める生産目標。特に、可用性とデータ損失からの保護に関する要件。  
  
-   各データベースの性質。サイズ、使用パターン、内容の性質、保持しているデータの要件など。  
  
-   リソースについての制約。ハードウェア、スタッフ、バックアップ メディアを保管する場所、保管されたメディアの物理的なセキュリティなど。  

### <a name="impact-of-the-recovery-model-on-backup-and-restore"></a>バックアップおよび復元に対する復旧モデルの影響  
 バックアップ操作および復元操作は、復旧モデルのコンテキストで発生します。 復旧モデルは、トランザクション ログの管理方法を制御するデータベース プロパティです。 また、データベースの復旧モデルでは、そのデータベースでサポートされるバックアップの種類および復元シナリオが判断されます。 通常、データベースは単純復旧モデルまたは完全復旧モデルを使用します。 完全復旧モデルを補完するには、一括操作を行う前に一括ログ復旧モデルに切り替えます。 これらの復旧モデルの概要とトランザクション ログの管理への影響については、「 [トランザクション ログ (SQL Server)](../logs/the-transaction-log-sql-server.md)」を参照してください。  
  
 データベースに対する復旧モデルの最善の選択は、ビジネス要件によって異なります。 トランザクション ログの管理を不要にし、バックアップと復元を簡単にするには、単純復旧モデルを使用します。 作業損失の可能性を最小に抑えるには、管理のオーバーヘッドが発生するという犠牲を払っても、完全復旧モデルを使用します。 バックアップおよび復元に対する復旧モデルの影響については、「 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)」を参照してください。  
  
### <a name="design-your-backup-strategy"></a>バックアップ戦略を設計する  
 特定のデータベースに対するビジネス要件を満たす復旧モデルを選択した後、対応するバックアップ ストラテジを計画して実装する必要があります。 最適なバックアップ ストラテジはさまざまな要因に依存しますが、その中でも以下の要因が特に重要です。  
  
-   アプリケーションがデータベースにアクセスする必要があるのは 1 日に何時間か。  
  
     オフピーク時間が予測できる場合は、その時間にデータベースの完全バックアップをスケジュールすることをお勧めします。  
  
-   変更や更新はどの程度の頻度で行われるか。  
  
     変更が頻繁に行われる場合は、次のことを考慮してください。  
  
    -   単純復旧モデルでは、データベースの完全バックアップの合間に差分バックアップをスケジュールすることを検討します。 差分バックアップは、データベースの最後の完全バックアップ以降の変更だけをキャプチャします。  
  
    -   完全復旧モデルでは、ログ バックアップを頻繁に行うようスケジュールする必要があります。 完全バックアップの合間に差分バックアップを行うようにスケジュールすると、データを復元した後で復元する必要のあるログ バックアップの数が減るので、復元時間を短縮することができます。  
  
-   変更は、データベースの一部分でのみ行われるか、データベースの大部分で行われるか。  
  
     ファイルまたはファイル グループの一部分に変更が集中する大規模なデータベースでは、部分バックアップまたはファイル バックアップが有効です。 詳細については、「[部分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md)」と「[完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)」を参照してください。  
  
-   データベースの完全バックアップにはどの程度のディスク領域が必要か。  
  
 ### <a name="estimate-the-size-of-a-full-database-backup"></a>データベースの完全バックアップのサイズの推計  
 バックアップと復元のストラテジを実装する前に、データベースの完全バックアップで使用するディスク領域を推計する必要があります。 バックアップ操作では、データベース内のデータをバックアップ ファイルにコピーします。 バックアップにはデータベース内の実際のデータだけが入っており、未使用の領域は入っていません。 そのため、通常、バックアップはデータベースそのものよりも小さくなります。 データベースの完全バックアップのサイズは、**sp_spaceused** システム ストアド プロシージャを使用して推計することができます。 詳細については、「[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)」を参照してください。  
  
### <a name="schedule-backups"></a>バックアップのスケジュール  
 バックアップの実行によって、実行中のトランザクションが受ける影響はわずかです。したがってバックアップは、通常の運用時に実行できます。 実稼働ワークロードへの影響は最小限にとどめて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップを実行できます。  
   
>  バックアップ中のコンカレンシーの制限については、「[バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)」を参照してください。  
  
 必要なバックアップの種類、および各種類のバックアップを実行する必要のある頻度を決定した後、データベースに対するデータベース メンテナンス プランの一部として、定期的なバックアップをスケジュールすることをお勧めします。 メンテナンス プランと、データベース バックアップおよびログ バックアップ用のメンテナンス プランの作成方法については、「 [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)」を参照してください。
  
### <a name="test-your-backups"></a>バックアップのテスト  
 バックアップをテストするまでは、復元ストラテジが完成したことにはなりません。 データベースのコピーをテスト システムに復元することで、各データベースに対するバックアップ ストラテジを十分にテストすることが重要です。 使用するすべての種類のバックアップの復元をテストする必要があります。
  
 データベースごとに操作マニュアルを用意しておくことをお勧めします。 この操作マニュアルには、バックアップの場所、バックアップ デバイス名 (ある場合)、およびテスト バックアップの復元に必要な時間を記載しておきます。

## <a name="monitor-progress-with-xevent"></a>xEvent で進捗状況を監視する
バックアップと復元の操作は、関連するデータベースのサイズと処理の複雑さによって、相当の時間がかかる場合があります。 いずれの処理で問題が発生した場合は、**backup_restore_progress_trace** 拡張イベントを使用して進捗状況をライブで監視できます。 拡張イベントの詳細については、「 [拡張イベント](../extended-events/extended-events.md)」を参照してください。

  >[!WARNING]
  > backup_restore_progress_trace 拡張イベントを使用すると、パフォーマンスの問題が発生し、大量のディスク領域を消費する場合があります。 使用するのは短時間にし、慎重に実行し、実稼働環境で実装する前には徹底的なテストを行ってください。


```sql
-- Create the backup_restore_progress_trace extended event esssion
CREATE EVENT SESSION [BackupRestoreTrace] ON SERVER 
ADD EVENT sqlserver.backup_restore_progress_trace
ADD TARGET package0.event_file(SET filename=N'BackupRestoreTrace')
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=5 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
GO

-- Start the event session  
ALTER EVENT SESSION [BackupRestoreTrace]  
ON SERVER  
STATE = start;  
GO  

-- Stop the event session  
ALTER EVENT SESSION [BackupRestoreTrace]  
ON SERVER  
STATE = stop;  
GO  
```

### <a name="sample-output-from-extended-event"></a>拡張イベントからの出力例 

![xEvent の出力のバックアップ例](media/back-up-and-restore-of-sql-server-databases/backup-xevent-example.png)
![xEvent の出力の復元例](media/back-up-and-restore-of-sql-server-databases/restore-xevent-example.png)
 
  
## <a name="more-about-backup-tasks"></a>バックアップ タスクの詳細  
-   [メンテナンス プランの作成](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
-   [ジョブの作成](../../ssms/agent/create-a-job.md)  
  
-   [ジョブのスケジュール設定](../../ssms/agent/schedule-a-job.md)  
  
## <a name="working-with-backup-devices-and-backup-media"></a>バックアップ デバイスとバックアップ メディアの操作  
-   [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [バックアップ先としてディスクまたはテープを指定する &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [バックアップ デバイスの削除 &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [バックアップの有効期限の設定 &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [バックアップ セットに含まれているデータ ファイルおよびログ ファイルの表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [デバイスからのバックアップ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="creating-backups"></a>バックアップの作成  
**注:** 部分バックアップまたはコピーのみのバックアップでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) ステートメントにそれぞれ PARTIAL オプションまたは COPY_ONLY オプションを使う必要があります。  
  
 ### <a name="using-ssms"></a>SSMS の使用   
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 ### <a name="using-t-sql"></a>T-SQL の使用  
-   [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [データベースが破損したときのトランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [バックアップ中または復元中にバックアップ チェックサムを有効または無効にする &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [バックアップまたは復元の操作をエラー発生後に続行するか停止するかを指定する &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="restore-data-backups"></a>データのバックアップを復元する 
### <a name="using-ssms"></a>SSMS の使用 
-   [SSMS を使用してデータベース バックアップを復元する](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [データベースを新しい場所に復元する &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [データベースの差分バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
### <a name="using-t-sql"></a>T-SQL の使用
-   [単純復旧モデルでのデータベース バックアップの復元 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [完全復旧モデルで障害発生時点までデータベースを復元する &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [既存のファイルにファイルとファイル グループを復元する &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [新しい場所へのファイルの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [master データベースの復元 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  

## <a name="restore-transaction-logs-full-recovery-model"></a>トランザクション ログを復元する (完全復旧モデル)
### <a name="using-ssms"></a>SSMS の使用  
-   [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 ### <a name="using-t-sql"></a>T-SQL の使用 
-   [SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
 
-   [中断された復元操作の再開 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [データを復元しないデータベースの復旧 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
 
## <a name="more-information-and-resources"></a>詳細情報とリソース
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Analysis Services データベースのバックアップと復元](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)   
 [フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [レプリケートされたデータベースのバックアップと復元](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
