---
title: Microsoft Azure に格納されたバックアップからの復元 | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6ae358b2-6f6f-46e0-a7c8-f9ac6ce79a0e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cda4fd3fa0bbb66e95d61ec87ff66dee809e2962
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155450"
---
# <a name="restoring-from-backups-stored-in-microsoft-azure"></a>Microsoft Azure に格納されたバックアップからの復元
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、Azure Blob Storage サービスに格納されたバックアップを使用してデータベースを復元するときの注意事項について説明します。 このトピックは、SQL Server Backup to URL または [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を使用して作成されたバックアップが対象です。  
  
 Azure Blob Storage サービスに格納されたバックアップを復元する計画がある場合は、このトピックを確認した後、データベースの復元方法 (オンプレミス バックアップでも Azure バックアップでも同じ) の手順が説明されているトピックを確認することをお勧めします。  
  
## <a name="overview"></a>概要  
 内部設置型バックアップからデータベースを復元するために使用するツールや方法は、クラウド バックアップからのデータベースの復元にも当てはまります。  以下のセクションでは、これらの注意事項に加えて、Azure Blob Storage サービスに格納されたバックアップを使用するときに知っておく必要がある相違点について説明します。  
  
### <a name="using-transact-sql"></a>Transact-SQL の使用  
  
-   SQL Server はバックアップ ファイルを取得するために外部ソースに接続する必要があるため、SQL 資格情報を使用してストレージ アカウントへの認証を行います。 そのため、RESTORE ステートメントには WITH CREDENTIAL オプションが必要です。 詳細については、「 [Microsoft Azure Blob Storage サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を使用してクラウドへのバックアップを管理している場合は、 **smart_admin.fn_available_backups** システム関数を使用すると、ストレージ内の使用可能なバックアップをすべて確認できます。 このシステム関数により、テーブル内のデータベースの使用可能なすべてのバックアップが返されます。 結果はテーブルで返されるため、結果のフィルター処理または並べ替えが可能です。 詳細については、「[managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)」を参照してください。  
  
### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用  
  
-   復元タスクは、SQL Server Management Studio を使用してデータベースを復元するために使用されます。 現在、バックアップ メディアのページには、Azure Blob Storage サービスに格納されたバックアップ ファイルを表示するための **[URL]** オプションがあります。 また、ストレージ アカウントへの認証に使用する SQL 資格情報を指定することも必要です。 その後、 **[復元するバックアップ セット]** グリッドには、Azure Blob Storage 内の使用可能なバックアップが表示されます。 詳細については、「[SQL Server Management Studio を使用した Microsoft Azure Storage からの復元](../../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS)」を参照してください。  
  
### <a name="optimizing-restores"></a>復元の最適化  
 復元の書き込み時間を短縮するには、SQL Server ユーザー アカウントに **[ボリュームの保守タスクを実行]** ユーザー権利を追加します。 詳細については、「 [データベース ファイルの初期化](https://go.microsoft.com/fwlink/?LinkId=271622)」を参照してください。 ファイルの瞬時初期化が有効な状態で復元が依然として低速な場合は、データベースをバックアップしたときに使用したインスタンスに対応するログ ファイルのサイズに注目します。 ログのサイズが非常に大きい場合 (数 GB) は、復元が低速であることが予期されます。 ログ ファイルの処理に長い時間が費やされるために、復元中はログ ファイルのサイズを 0 にする必要があります。  
  
 復元時間を短縮するには、圧縮されたバックアップを使用することをお勧めします。  バックアップ サイズが 25 GB を超える場合は、 [AzCopy ユーティリティ](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx) を使用してローカル ドライブにダウンロードしてから復元を実行します。 バックアップに関するその他のベスト プラクティスと推奨事項については、「 [SQL Server Backup to URL のベスト プラクティスとトラブルシューティング](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)」を参照してください。  
  
 復元を実行するときに詳細ログを生成するために、トレース フラグ 3051 を有効にすることもできます。 このログ ファイルはログ ディレクトリに配置され、次の形式を使用して名前が付けられます: BackupToUrl-\<インスタンス名>-\<DB 名>-action-\<PID>.log。 このログ ファイルには、問題の診断に役に立つタイミングも含め、Azure Storage への各ラウンド トリップが記録されます。  
  
### <a name="topics-on-performing-restore-operations"></a>復元操作の実行に関するトピック  
  
-   [データベースの全体復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [データベースの全体復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
-   [ファイル復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
  
-   [ファイル復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)  
  
-   [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
