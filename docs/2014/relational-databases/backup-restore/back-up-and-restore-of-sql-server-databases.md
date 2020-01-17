---
title: SQL Server データベースのバックアップと復元 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: a94ec756e86cb814d0e3b3f624b4a9b3eb180533
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176027"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>SQL Server データベースのバックアップと復元
  このトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをバックアップする利点、バックアップと復元に関する基本的な用語、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップと復元の方法を紹介します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップと復元のセキュリティに関する考慮事項についても取り上げます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップと復元コンポーネントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納されている大切なデータを保護するうえで不可欠な保護対策を提供します。 致命的なデータ損失のリスクを最小限に抑えるには、データベースをバックアップして、データに対する変更内容を定期的に保存しておく必要があります。 バックアップと復元方法を十分に計画することで、さまざまな障害に起因するデータの損失からデータベースを保護できます。 バックアップを復元し、データベースを復旧するテストを実施することで、障害発生時に適切に対応できるようになります。  
  
 バックアップを格納するローカル ストレージに加えて、SQL Server では、バックアップおよび Azure Blob Storage サービスからの復元がサポートされます。 詳細については、「 [Azure Blob Storage サービスを使用したバックアップと復元の SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  

  
##  <a name="Benefits"></a> 利点  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをバックアップしたり、既存のバックアップの復元テストを実行したりできるほか、離れた安全な場所にバックアップのコピーを保管することによって、致命的な損失からデータを保護することができます。  
  
    > [!IMPORTANT]  
    >  これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータを確実に保護する唯一の手段です。  
  
     データベースの有効なバックアップがあれば、次に示したようなさまざまな障害からデータを復旧することができます。  
  
    -   メディアの障害  
  
    -   ユーザー エラー (テーブルの誤削除など)  
  
    -   ハードウェア障害 (ディスク ドライブの損傷や、復旧の可能性のないサーバー障害など)  
  
    -   自然災害。 Azure Blob Storage サービスへの SQL Server バックアップを使用すると、オンプレミスの場所に影響する自然災害が発生した場合に使用できるように、オンプレミスの場所とは異なるリージョンにオフサイト バックアップを作成できます。  
  
-   また、データベースのバックアップは、サーバー間でのデータベースのコピー、 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] やデータベース ミラーリングのセットアップ、およびアーカイブなど、日常的な管理作業を行ううえでも便利です。  
  

  
##  <a name="TermsAndDefinitions"></a> コンポーネントおよび概念  
 バックアップ (back up) (動詞)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースまたはそのトランザクション ログからバックアップ デバイス (ディスクなど) にデータまたはログ レコードをコピーすることによって、データ バックアップまたはログ バックアップを作成します。  
  
 バックアップ (backup) (名詞)  
 障害の発生後、データの復元と復旧に使用できるデータのコピー。 データベースのバックアップを使用して、コピー (データベース) を新しい場所に復元することもできます。  
  
 バックアップ デバイス (backup device)  
 SQL Server のバックアップの書き込みと復元に使用されるディスクまたはテープ デバイス。 SQL Server のバックアップは、Azure Blob Storage サービスに書き込むこともできます。バックアップ先とバックアップ ファイルの名前を指定するには **URL** 形式を使用します。 詳細については、「 [Azure Blob Storage サービスを使用したバックアップと復元の SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
 バックアップ メディア (backup media)  
 バックアップの書き込み先となる 1 つまたは複数のテープまたはディスク ファイル。  
  
 データ バックアップ (data backup)  
 データのバックアップ。データベース全体 (データ バックアップ)、データベースの一部 (部分バックアップ)、または一連のデータ ファイルやファイル グループ (ファイル バックアップ) の形式で存在します。  
  
 データベース バックアップ (database backup)  
 データベースのバックアップ。 データベースの完全バックアップは、バックアップが完了した時点のデータベース全体を表します。 差分データベース バックアップには、最新の完全バックアップ以降に行われたデータベースへの変更のみが含まれます。  
  
 差分バックアップ (differential backup)  
 データベース全体、データベースの一部、または一連のデータ ファイル (またはファイル グループ) の最新の完全バックアップ (差分ベース) をベースとし、その差分ベース以後に変更されたデータのみを含んだデータ バックアップ。  
  
 完全バックアップ (full backup)  
 特定のデータベース (または一連のファイルやファイル グループ) 内のデータがすべて含まれ、さらに、データを復旧するために必要なログも含んだデータ バックアップ。  
  
 ログ バックアップ (log backup)  
 前回のログ バックアップでバックアップされなかったすべてのログ レコードを含むトランザクション ログのバックアップ (完全復旧モデル)。  
  
 復元 (recover)  
 安定し一貫した状態にデータベースを戻すこと。  
  
 復旧 (recovery)  
 データベースをトランザクションの一貫性が保たれた状態にする、データベース起動時または RESTORE WITH RECOVERY 時のフェーズ。  
  
 復旧モデル (recovery model)  
 データベースのトランザクション ログのメンテナンスを制御するデータベース プロパティ。 復旧モデルの種類は、単純、完全、および一括ログの 3 種類です。 データベースのバックアップと復元の要件は、その復旧モデルによって決まります。  
  
 復元 (restore)  
 データを直近の状態まで戻す複数フェーズから成る処理。指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップからすべてのデータおよびログ ページを指定されたデータベースにコピーするフェーズと、バックアップにログとして記録されているすべてのトランザクションをロールフォワード (ログに記録されている変更を適用) するフェーズとで構成されます。  
  

  
##  <a name="BnrStrategies"></a>バックアップと復元の方法の概要  
 データのバックアップと復元は、特定の環境向けにカスタマイズし、使用可能なリソースと連動させる必要があります。 したがって、信頼性が確保された状態でバックアップと復元を使用して復旧するには、バックアップと復元のストラテジが必要です。 バックアップと復元のストラテジ設計が良ければ、特定のビジネス要件を考慮しながら、データの可用性を最大にし、データ損失を最小限に抑えることができます。  
  
> [!IMPORTANT]  
>  データベースとバックアップは異なるデバイスに置いてください。 そうしないと、データベースを置いているデバイスに障害が発生した場合、バックアップも使用できなくなります。 データとバックアップを異なるデバイスに置くと、バックアップの書き込みでもデータベースの運用でも I/O パフォーマンスが向上します。  
  
 バックアップと復元のストラテジには、バックアップに関する部分と復元に関する部分があります。 ストラテジで扱うバックアップ部分では、バックアップの種類と頻度、バックアップに必要なハードウェアの性質と速度、バックアップのテスト方法、およびバックアップ メディアの保管場所と保管方法 (セキュリティ上の考慮事項も含む) を定義します。 ストラテジで扱う復元部分では、復元の実行責任者と、データベースの可用性とデータ損失の最小化という目標を達成するためにどのように復元を実行するのかを定義します。 バックアップと復元の手順をドキュメント化し、そのドキュメントを運用手順書に含めて保管することをお勧めします。  
  
 バックアップと復元について効果的なストラテジをデザインするには、慎重に計画、実装、およびテストする必要があります。 テストは必ず行ってください。 復元ストラテジに含まれるすべての組み合わせでバックアップを正常に復元できるようになって初めて、バックアップ ストラテジは完成します。 さまざまな要因を検討する必要があります。 その一部を次に示します。  
  
-   組織がそのデータベースに求める生産目標。特に、可用性とデータ損失からの保護に関する要件。  
  
-   各データベースの性質。サイズ、使用パターン、内容の性質、保持しているデータの要件など。  
  
-   リソースについての制約。ハードウェア、スタッフ、バックアップ メディアを保管する場所、保管されたメディアの物理的なセキュリティなど。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のディスク上ストレージ形式は、64 ビット環境でも 32 ビット環境でも同じです。 このため、バックアップと復元は 32 ビット環境と 64 ビット環境の間でも機能します。 一方の環境で実行中のサーバー インスタンスで作成したバックアップは、他方の環境で実行中のサーバー インスタンスで復元できます。  
  

  
### <a name="impact-of-the-recovery-model-on-backup-and-restore"></a>バックアップおよび復元に対する復旧モデルの影響  
 バックアップ操作および復元操作は、復旧モデルのコンテキストで発生します。 復旧モデルは、トランザクション ログの管理方法を制御するデータベース プロパティです。 また、データベースの復旧モデルでは、そのデータベースでサポートされるバックアップの種類および復元シナリオが判断されます。 通常、データベースは単純復旧モデルまたは完全復旧モデルを使用します。 完全復旧モデルを補完するには、一括操作を行う前に一括ログ復旧モデルに切り替えます。 これらの復旧モデルの概要とトランザクション ログの管理への影響については、「[トランザクション ログ &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)」を参照してください。  
  
 データベースに対する復旧モデルの最善の選択は、ビジネス要件によって異なります。 トランザクション ログの管理を不要にし、バックアップと復元を簡単にするには、単純復旧モデルを使用します。 作業損失の可能性を最小に抑えるには、管理のオーバーヘッドが発生するという犠牲を払っても、完全復旧モデルを使用します。 バックアップおよび復元に対する復旧モデルの影響については、「[バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)」を参照してください。  
  
### <a name="design-the-backup-strategy"></a>バックアップ ストラテジの設計  
 特定のデータベースに対するビジネス要件を満たす復旧モデルを選択した後、対応するバックアップ ストラテジを計画して実装する必要があります。 最適なバックアップ ストラテジはさまざまな要因に依存しますが、その中でも以下の要因が特に重要です。  
  
-   アプリケーションがデータベースにアクセスする必要があるのは 1 日に何時間か。  
  
     オフピーク時間が予測できる場合は、その時間にデータベースの完全バックアップをスケジュールすることをお勧めします。  
  
-   変更や更新はどの程度の頻度で行われるか。  
  
     変更が頻繁に行われる場合は、次のことを考慮してください。  
  
    -   単純復旧モデルでは、データベースの完全バックアップの合間に差分バックアップをスケジュールすることを検討します。 差分バックアップは、データベースの最後の完全バックアップ以降の変更だけをキャプチャします。  
  
    -   完全復旧モデルでは、ログ バックアップを頻繁に行うようスケジュールする必要があります。 完全バックアップの合間に差分バックアップを行うようにスケジュールすると、データを復元した後で復元する必要のあるログ バックアップの数が減るので、復元時間を短縮することができます。  
  
-   変更は、データベースの一部分でのみ行われるか、データベースの大部分で行われるか。  
  
     ファイルまたはファイル グループの一部分に変更が集中する大規模なデータベースでは、部分バックアップまたはファイル バックアップが有効です。 詳細については、「[部分バックアップ &#40;SQL Server&#41;](partial-backups-sql-server.md)」と「[完全バックアップ &#40;SQL Server&#41;](full-file-backups-sql-server.md)」を参照してください。  
  
-   データベースの完全バックアップにはどの程度のディスク領域が必要か。  
  
     詳細については、このセクションの「[データベースの完全バックアップのサイズの推計](#EstimateDbBuSize)」を参照してください。  
  
####  <a name="EstimateDbBuSize"></a>データベースの完全バックアップのサイズの見積もり  
 バックアップと復元のストラテジを実装する前に、データベースの完全バックアップで使用するディスク領域を推計する必要があります。 バックアップ操作では、データベース内のデータをバックアップ ファイルにコピーします。 バックアップにはデータベース内の実際のデータだけが入っており、未使用の領域は入っていません。 そのため、通常、バックアップはデータベースそのものよりも小さくなります。 データベースの完全バックアップのサイズは、**sp_spaceused** システム ストアド プロシージャを使用して推計することができます。 詳細については、「[sp_spaceused &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)」を参照してください。  
  
### <a name="schedule-backups"></a>バックアップのスケジュール  
 バックアップの実行によって、実行中のトランザクションが受ける影響はわずかです。したがってバックアップは、通常の運用時に実行できます。 実稼働ワークロードへの影響は最小限にとどめて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップを実行できます。  
  
> [!NOTE]  
>  バックアップ中のコンカレンシーの制限については、「[バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)」を参照してください。  
  
 必要なバックアップの種類、および各種類のバックアップを実行する必要のある頻度を決定した後、データベースに対するデータベース メンテナンス プランの一部として、定期的なバックアップをスケジュールすることをお勧めします。 メンテナンス プランと、データベース バックアップおよびログ バックアップ用のメンテナンス プランの作成方法については、「 [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md)」を参照してください。  
  
### <a name="test-your-backups"></a>バックアップのテスト  
 バックアップをテストするまでは、復元ストラテジが完成したことにはなりません。 データベースのコピーをテスト システムに復元することで、各データベースに対するバックアップ ストラテジを十分にテストすることが重要です。 使用するすべての種類のバックアップの復元をテストする必要があります。  
  
 データベースごとに操作マニュアルを用意しておくことをお勧めします。 この操作マニュアルには、バックアップの場所、バックアップ デバイス名 (ある場合)、およびテスト バックアップの復元に必要な時間を記載しておきます。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
### <a name="scheduling-backup-jobs"></a>バックアップ ジョブのスケジュール設定  
  
-   [メンテナンス プランの作成](../maintenance-plans/create-a-maintenance-plan.md)  
  
-   [ジョブの作成](../../ssms/agent/create-a-job.md)  
  
-   [ジョブのスケジュール設定](../../ssms/agent/schedule-a-job.md)  
  
### <a name="working-with-backup-devices-and-backup-media"></a>バックアップ デバイスとバックアップ メディアの操作  
  
-   [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [バックアップ先としてディスクまたはテープを指定する &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [バックアップ デバイスの削除 &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [バックアップの有効期限の設定 &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [バックアップ セットに含まれているデータ ファイルおよびログ ファイルの表示 &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [デバイスからのバックアップ復元 &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
### <a name="creating-backups"></a>バックアップの作成  
  
> [!NOTE]  
>  部分バックアップまたはコピーのみのバックアップでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) ステートメントにそれぞれ PARTIAL オプションまたは COPY_ONLY オプションを使う必要があります。  
  
 **SQL Server Management Studio の使用**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
 **Transact-SQL の使用**  
  
-   [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [データベースが破損したときのトランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [バックアップ中または復元中にバックアップ チェックサムを有効または無効にする &#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [バックアップまたは復元の操作をエラー発生後に続行するか停止するかを指定する &#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  

  
### <a name="restoring-data-backups"></a>データ バックアップの復元  
 **SQL Server Management Studio の使用**  
  
-   [データベースバックアップ&#40;の復元 SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [データベースを新しい場所に復元する &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [データベースの差分バックアップの復元 &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
-   [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
 **Transact-SQL の使用**  
  
-   [単純復旧モデルでのデータベース バックアップの復元 &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [完全復旧モデルで障害発生時点までデータベースを復元する &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [既存のファイルにファイルとファイル グループを復元する &#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [新しい場所へのファイルの復元 &#40;SQL Server&#41;](restore-files-to-a-new-location-sql-server.md)  
  
-   [master データベースの復元 &#40;Transact-SQL&#41;](restore-the-master-database-transact-sql.md)  
  

  
### <a name="restoring-transaction-logs-full-recovery-model"></a>トランザクション ログの復元 (完全復旧モデル)  
 **SQL Server Management Studio の使用**  
  
-   [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 **Transact-SQL の使用**  
  
-   [SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  

  
### <a name="additional-restore-tasks"></a>その他の復元タスク  
 **Transact-SQL の使用**  
  
-   [中断された復元操作の再開 &#40;Transact-SQL&#41;](restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [データを復元しないデータベースの復旧 &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)  
  

  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Analysis Services データベースのバックアップと復元](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)   
 [フルテキスト カタログとフルテキスト インデックスのバックアップおよび復元](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [レプリケートされたデータベースのバックアップと復元](../replication/administration/back-up-and-restore-replicated-databases.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
