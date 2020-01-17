---
title: '[データベースのバックアップ] ([メディア オプション] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- swb.backupdatabase.mediaoptions.f1
- sql12.swb.backupdatabase.mediaoptions.f1
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d1995ca52507a3027438cac21677517059d3d219
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154838"
---
# <a name="back-up-database-media-options-page"></a>[データベースのバックアップ] ([メディア オプション] ページ)
  **[データベースのバックアップ]** ダイアログ ボックスの **[メディア オプション]** ページを使用すると、データベースのメディアのオプションを表示または変更できます。  
  
 **SQL Server Management Studio を使用してバックアップを作成するには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  データベース メンテナンス プランを定義して、データベース バックアップを作成できます。 詳細については、「 [メンテナンス プラン](../maintenance-plans/maintenance-plans.md) 」および「 [メンテナンス プラン ウィザードの使用](../maintenance-plans/use-the-maintenance-plan-wizard.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してバックアップ タスクを指定する場合、 [!INCLUDE[tsql](../../includes/tsql-md.md)][[スクリプト]](/sql/t-sql/statements/backup-transact-sql) ボタンをクリックしてスクリプトの保存先を選択することにより、対応する **BACKUP** スクリプトを生成できます。  
  
## <a name="options"></a>および  
  
### <a name="overwrite-media"></a>[メディアに上書きします]  
 **[メディアに上書きします]** パネルのオプションでは、バックアップをメディアに書き込む方法を制御します。 [データベースのバックアップ] ダイアログ ボックスの [全般] ページでバックアップ先として [URL] (Azure Storage) を選択した場合、[メディアに上書きします] セクションのオプションは無効になります。 Transact-SQL の `BACKUP TO URL.. WITH FORMAT` ステートメントを使用してバックアップを上書きすることもできます。 詳細については、「 [SQL Server Backup to URL](sql-server-backup-to-url.md)」を参照してください。  
  
 暗号化オプションとの併用がサポートされているのは、 **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]** オプションのみです。 **[既存のメディア セットにバックアップする]** セクションのオプションを選択すると、 **[バックアップ オプション]** ページの暗号化オプションが無効になります。  
  
> [!NOTE]  
>  メディア セットの詳細については、[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md) を参照してください。  
  
 **[既存のメディア セットにバックアップする]**  
 データベースを既存のメディア セットにバックアップします。 このオプション ボタンをクリックすると、3 つのオプションが有効になります。  
  
 次のいずれかのオプションを選択します。  
  
 **[既存のバックアップ セットに追加する]**  
 バックアップ セットを既存のメディア セットに追加し、以前のバックアップをすべて保持します。  
  
 **[既存のすべてのバックアップ セットを上書きする]**  
 既存のメディア セット上にある以前のバックアップをすべて現在のバックアップに置き換えます。  
  
 **[メディア セット名とバックアップ セットの有効期限を確認する]**  
 既存のメディア セットをバックアップする場合は、必要に応じて、バックアップ操作でバックアップ セットの名前と有効期限を確認することを指定します。  
  
 **[メディア セット名]**  
 **[メディア セット名とバックアップ セットの有効期限を確認する]** チェック ボックスがオンの場合、必要に応じて、このバックアップ操作で使用するメディア セットの名前を指定します。  
  
 **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]**  
 新しいメディア セットを使用して、以前のバックアップ セットを消去します。  
  
 このオプションをクリックすると、次のオプションを指定できるようになります。  
  
 **[新しいメディア セット名]**  
 必要に応じて、メディア セットの新しい名前を入力します。  
  
 **[新しいメディア セットの説明]**  
 必要に応じて、新しいメディア セットのわかりやすい説明を入力します。 この説明は、内容について正確に伝えられるだけの具体性が必要です。  
  
### <a name="reliability"></a>[信頼性]  
 **[トランザクション ログ]** パネルのオプションでは、バックアップ操作によるエラー管理を制御します。  
  
 **[完了時にバックアップを検証する]**  
 バックアップ セットが完全で、すべてのボリュームが読み取り可能であることを検証します。  
  
 **[メディアに書き込む前にチェックサムを行う]**  
 バックアップ メディアに書き込む前にチェックサムを検証します。 このチェック ボックスをオンにすることは、 [!INCLUDE[tsql](../../includes/tsql-md.md)]の BACKUP ステートメントで CHECKSUM オプションを指定することと同じです。 このオプションをオンにするとワークロードが増加し、バックアップ操作のバックアップ スループットが低下する可能性があります。 バックアップ チェックサムの詳細については、「[バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)」を参照してください。  
  
 **[エラーのまま続行する]**  
 エラーが 1 回以上発生しても、バックアップ操作を続行します。  
  
### <a name="transaction-log"></a>トランザクション ログ  
 **[トランザクション ログ]** パネルのオプションでは、トランザクション ログ バックアップの動作を制御します。 これらのオプションは、完全復旧モデルと一括ログ復旧モデルにのみ適用されます。 これらのオプションは、 **[データベースのバックアップ]** ダイアログ ボックスの **[全般]** ページにある [[バックアップの種類]](../../integration-services/general-page-of-integration-services-designers-options.md) フィールドで **[トランザクション ログ]** を選択した場合のみアクティブになります。  
  
> [!NOTE]  
>  トランザクション ログのバックアップの詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)」を参照してください。  
  
 **[トランザクション ログを切り捨てる]**  
 トランザクション ログをバックアップし、それを切り捨てることでログの領域を解放します。 データベースはオンラインを維持します。 既定のオプションです。  
  
 **[ログの末尾をバックアップし、データベースを復元中の状態にしておく]**  
 ログの末尾をバックアップし、データベースを復元中の状態にします。 このオプションでは、 *ログ末尾のバックアップ*を作成します。このバックアップでは、データベースの復元に備えて、通常、まだバックアップされていないログ (アクティブなログ) をバックアップします。 復元が完了するまで、ユーザーはデータベースを使用できなくなります。  
  
 このオプションを選択することは、 [BACKUP](/sql/t-sql/statements/backup-transact-sql) ステートメント ([!INCLUDE[tsql](../../includes/tsql-md.md)]) で WITH NO_TRUNCATE および NORECOVERY を指定することと同じです。 詳細については、「[ログ末尾のバックアップ &#40;SQL Server&#41;](tail-log-backups-sql-server.md)」を参照してください。  
  
### <a name="tape-drive"></a>[テープ ドライブ]  
 **[テープ ドライブ]** パネルのオプションでは、バックアップ操作時のテープ管理を制御します。 これらのオプションは、 **[データベースのバックアップ]** ダイアログ ボックスの **[全般]** ページにある [[バックアップ先]](../../integration-services/general-page-of-integration-services-designers-options.md) パネルで **[テープ]** を選択した場合のみアクティブになります。  
  
> [!NOTE]  
>  テープ デバイスの使用方法については、「[バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)」を参照してください。  
  
 **[バックアップ後にテープをアンロードする]**  
 バックアップの完了後、テープをアンロードします。  
  
 **[アンロードの前にテープを巻き戻す]**  
 テープをアンロードする前にテープを解放し、巻き戻します。 このオプションは、 **[バックアップ後にテープをアンロードする]** チェック ボックスをオンにした場合のみ有効になります。  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [データベースが破損したときのトランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
