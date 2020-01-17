---
title: データベースの復元 ([オプション] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoredb.options.f1
ms.assetid: 9a75d48b-c25f-40f3-8ea1-32cfa8211754
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 266c127a8ef38a1a5701de24f9442861e604d84d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875631"
---
# <a name="restore-database-options-page"></a>[データベースの復元] \([オプション] ページ)
  **[データベースの復元]** ダイアログ ボックスの **[オプション]** ページを使用して、復元操作の動作と結果を変更します。  
  
 **SQL Server Management Studio を使用してデータベース バックアップを復元するには**  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
-   [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して復元タスクを指定するときに、この復元操作の RESTORE ステートメントを含む、対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを生成できます。 このスクリプトを生成するには、 **[スクリプト]** をクリックし、スクリプトの保存先を選択します。 RESTORE 構文については、「 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」を参照してください。  
  
## <a name="options"></a>[データベースの復元]  
  
### <a name="restore-options"></a>[復元オプション]  
 復元操作の動作の特徴を変更するには、 **[復元オプション]** パネルのオプションを使用します。  
  
 **[既存のデータベースを上書きする [WITH REPLACE]]**  
 データベースの名前が、 **[データベースの復元]** ダイアログ ボックスの [[全般]](../../integration-services/general-page-of-integration-services-designers-options.md) ページにある **[復元先]** フィールドで指定した名前と同じ場合は、そのデータベースのファイルが上書きされます。 別のデータベースのバックアップを既存のデータベース名に復元する場合でも、既存のデータベースのファイルが上書きされます。 このオプションを選択することは、 [RESTORE](/sql/t-sql/statements/restore-statements-arguments-transact-sql) ステートメント ([!INCLUDE[tsql](../../includes/tsql-md.md)]) で REPLACE オプションを使用することと同じです。  
  
> [!CAUTION]  
>  このオプションは、十分な検討を行った場合に限り使用してください。 詳細については、「[RESTORE の引数 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)」を参照してください。  
  
 **[レプリケーションの設定を保存する [WITH KEEP_REPLICATION]]**  
 パブリッシュされたデータベースを、そのデータベースが作成されたサーバー以外のサーバーに復元するときに、レプリケーションの設定を保存します。 このオプションは、バックアップ作成時にデータベースがレプリケートされた場合にのみ使用します。  
  
 このオプションは、この表で後に説明する **[コミットされていないトランザクションをロールバックして、データベースを使用可能な状態にする。別のトランザクション ログは復元できません。]** オプションをクリックした場合だけ使用できます。これは、RECOVERY オプションを指定してバックアップを復元するのと同じです。  
  
 このオプションを選択することは、 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントで KEEP_REPLICATION オプションを使用することと同じです。  
  
 詳細については、「 [レプリケートされたデータベースのバックアップと復元](../replication/administration/back-up-and-restore-replicated-databases.md)」を参照してください。  
  
 **[復元するデータベースへのアクセスを制限する [WITH RESTRICTED_USER]]**  
 復元するデータベースの使用を、 **db_owner**、 **dbcreator**、または **sysadmin**のメンバーだけに制限します。  
  
 このオプションを選択することは、RESTORE ステートメントで RESTRICTED_USER オプションを使用することと同じです。  
  
### <a name="recovery-state"></a>[復旧状態]  
 復元操作後にデータベースの状態を確認するには、 **[復旧状態]** パネルのいずれかのオプションを選択する必要があります。  
  
 **RESTORE WITH RECOVERY**  
 **[全般]** ページの [[復元するバックアップ セット]](../../integration-services/general-page-of-integration-services-designers-options.md)グリッドでチェック ボックスがオンになっている最後のバックアップを復元した後に、データベースを復旧します。 これは既定のオプションで、 [RESTORE](/sql/t-sql/statements/restore-statements-arguments-transact-sql) ステートメント ([!INCLUDE[tsql](../../includes/tsql-md.md)]) で WITH RECOVERY を指定することと同じです。  
  
> [!NOTE]  
>  完全復旧モデルまたは一括ログ復旧モデルでは、すべてのログ ファイルを復元する場合にのみこのオプションを選択してください。  
  
 **RESTORE WITH NORECOVERY**  
 データベースを復元状態のままにします。 これにより、現在の復旧パスで他のバックアップを復元できます。 データベースを復旧するには、RESTORE WITH RECOVERY オプションを使用して復元操作を実行する必要があります (上記のオプションを参照)。  
  
 このオプションを選択することは、RESTORE ステートメントで WITH NORECOVERY を使用することと同じです。  
  
 このオプションを選択すると、 **[レプリケーションの設定を保存する]** オプションを選択できなくなります。  
  
 **RESTORE WITH STANDBY**  
 データベースをスタンバイ状態のままにします。この状態では、データベースは、制限付きの読み取り専用アクセスで使用できます。 このオプションを選択することは、RESTORE ステートメントで WITH STANDBY を使用することと同じです。  
  
 このオプションを選択するには、 **[スタンバイ ファイル]** ボックスにスタンバイ ファイルを指定する必要があります。 スタンバイ ファイルを使用すると、復旧結果を元に戻すことができます。  
  
 **[スタンバイ ファイル]**  
 スタンバイ ファイルを指定します。 スタンバイ ファイルは、参照して指定するか、テキスト ボックスにパス名を直接入力します。  
  
### <a name="tail-log-backup"></a>[ログ末尾のバックアップ]  
 データベースの復元と共にログ末尾のバックアップを実行するように指定できます。  
  
 **[復元の前にログ末尾のバックアップを行う]**  
 ログ末尾のバックアップを行うように指定するには、このチェック ボックスをオンにします。  
  
> [!NOTE]  
>  [[バックアップのタイムライン]](backup-timeline.md) ダイアログ ボックスで選択した特定の時点がログ末尾のバックアップを必要としている場合は、このチェック ボックスがオンになり、それを変更することはできません。  
  
 **[バックアップ ファイル]**  
 ログ末尾のバックアップ ファイルを指定します。 バックアップ ファイルは、参照して指定するか、テキスト ボックスに名前を直接入力します。  
  
### <a name="server-connections"></a>サーバー接続  
 既存のデータベース接続を閉じることができます。  
  
 **[既存の接続を閉じる]**  
 データベースへのアクティブな接続がある場合、復元操作は失敗する可能性があります。 **とデータベース間のすべてのアクティブな接続を閉じるには、** [既存の接続を閉じる] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] オプションをオンにします。 このチェック ボックスをオンにすると、データベースは復元操作の実行前にシングル ユーザー モードに設定され、復元操作の完了後にマルチユーザー モードに設定されます。  
  
### <a name="prompt"></a>[プロンプト]  
 **[各バックアップを復元する前に確認する]**  
 各バックアップが復元された後、復元シーケンスを続行するかどうかを確認する **[復元の続行]** ダイアログ ボックスを表示することを指定します。 このダイアログ ボックスには、次のメディア セットの名前 (既知の場合) および次のバックアップ セットの名前と説明が表示されます。  
  
 このオプションを使用すると、バックアップの復元後に復元シーケンスを一時停止できます。 メディア セットごとにテープを交換する必要がある場合 (サーバーにテープ デバイスが 1 台しかない場合など) に特に便利です。 続行する準備ができたら、 **[OK]** をクリックします。  
  
 **[いいえ]** をクリックすると、復元シーケンスを中断できます。 これにより、データベースが復元状態のままになります。 その後、都合のよいときに、 **[復元の続行]** ダイアログ ボックスに表示されている次のバックアップから再開することで、復元シーケンスを続行できます。 次のバックアップを復元する方法は、そのバックアップに含まれているのがデータかトランザクション ログかによって、次のように異なります。  
  
-   次のバックアップが完全バックアップまたは差分バックアップの場合は、 **[データベースの復元]** タスクを再度使用します。  
  
-   次のバックアップがファイル バックアップの場合は、 **[ファイルおよびファイル グループの復元]** タスクを使用します。 詳細については、「[ファイルとファイル グループの復元 &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)」を参照してください。  
  
-   次のバックアップがログ バックアップの場合は、 **[トランザクション ログの復元]** タスクを使用します。 トランザクション ログの復元による復元シーケンスの再開については、「 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [デバイスからのバックアップ復元 &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)   
 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [[データベースの復元] &#40;[全般] ページ&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
