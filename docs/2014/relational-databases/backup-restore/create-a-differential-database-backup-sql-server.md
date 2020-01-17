---
title: データベースの差分バックアップの作成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full differential backups [SQL Server]
- database backups [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
- backups [SQL Server], creating
ms.assetid: 70f49794-b217-4519-9f2a-76ed61fa9f99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4be1c196adbe21635c1339da3d5ec7ca519001fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876601"
---
# <a name="create-a-differential-database-backup-sql-server"></a>データベースの差分バックアップの作成 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、データベースの差分バックアップを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **データベースの差分バックアップを作成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   BACKUP ステートメントは、明示的または暗黙的なトランザクションでは使用できません。  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   データベースの差分バックアップを作成するには、データベースの以前の完全バックアップが存在している必要があります。 選択したデータベースをバックアップしたことがない場合は、差分バックアップを作成する前にデータベースの完全バックアップを実行してください。 詳細については、データベースの完全バックアップの作成 [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)を使用してデータベースの差分バックアップを作成します。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   差分バックアップのサイズが大きくなると、データベースを復元するときに、差分バックアップの復元に要する時間がかなり長くなる場合があります。 このため、定期的に新しい完全バックアップを実行することにより、データの新しい差分ベースを作成することをお勧めします。 たとえば、データベース全体のバックアップ (つまり、データベースの完全バックアップ) を週に 1 回実行し、次の週の完全バックアップまでの間、一連のデータベースの差分バックアップを定期的に実行します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 権限と BACKUP LOG 権限は、既定では、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。  
  
 バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)では、ファイル アクセスの権限は確認されません。 バックアップ デバイスの物理ファイルに関するこのような問題は、バックアップや復元が試行され、物理リソースがアクセスされるまで、表面化しない可能性があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-differential-database-backup"></a>データベースの差分バックアップを作成するには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開し、目的のデータベースに応じて、任意のユーザー データベースを選択するか、または **[システム データベース]** を展開して任意のシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[バックアップ]** をクリックします。 **[データベースのバックアップ]** ダイアログ ボックスが表示されます。  
  
4.  **[データベース]** ボックスに、適切なデータベース名が表示されていることを確認します。 必要に応じて、このボックスの一覧から別のデータベースを選択することもできます。  
  
     差分バックアップは、すべての復旧モデル (完全復旧モデル、一括ログ復旧モデル、または単純復旧モデル) に対して実行できます。  
  
5.  **[バックアップの種類]** ボックスの一覧の **[差分]** を選択します。  
  
    > [!IMPORTANT]  
    >  ときに**差分**が選択されていることを確認、**バックアップのみコピー**チェック ボックスをオフします。  
  
6.  **[バックアップ コンポーネント]** で、 **[データベース]** をクリックします。  
  
7.  **[名前]** ボックスに表示された既定のバックアップ セット名をそのまま使用するか、または別のバックアップ セット名を入力します。  
  
8.  必要に応じて、 **[説明]** ボックスに、バックアップ セットの説明を入力します。  
  
9. バックアップ セットの有効期限を指定します。  
  
    -   バックアップ セットが指定の日数後に期限切れになるようにするには、 **[期間指定]** \(既定のオプション) をクリックし、セットを作成してからセットが期限切れになるまでの日数を入力します。 0 ～ 99,999 日の値を指定できます。0 日を指定すると、バックアップ セットの有効期限は無期限になります。  
  
         既定値は、 **[サーバーのプロパティ]** ダイアログ ボックス ( **[データベースの設定]** ページ) の **[バックアップ メディアの既定の保有期間 (日)]** オプションで設定されています。 このオプションを表示するには、オブジェクト エクスプローラーでサーバー名を右クリックし、[プロパティ] をクリックします。次に、 **[データベースの設定]** ページをクリックします。  
  
    -   バックアップ セットが特定の日付に期限切れになるようにするには、 **[日時指定]** をクリックし、セットの有効期限が切れる日付を入力します。  
  
10. **[ディスク]** または **[テープ]** をクリックして、バックアップ先を選択します。 **[追加]** をクリックすると、1 つのメディア セットを含んでいる、最高で 64 個のディスク ドライブまたはテープ ドライブのパスを選択できます。 選択したパスは、 **[バックアップ先]** ボックスの一覧に表示されます。  
  
     バックアップ先を削除するには、バックアップ先を選択して **[削除]** をクリックします。 バックアップ先の内容を表示するには、バックアップ先を選択して **[内容]** をクリックします。  
  
11. 詳細設定オプションを表示または選択するには、 **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
12. 次のいずれかをクリックして、 **[メディアに上書きします]** オプションを選択します。  
  
    -   **[既存のメディア セットにバックアップする]**  
  
         このオプションでは、 **[既存のバックアップ セットに追加する]** または **[既存のすべてのバックアップ セットを上書きする]** をクリックします。 必要に応じて、 **[メディア セット名とバックアップ セットの有効期限を確認する]** チェック ボックスをオンにします。また、必要に応じて、 **[メディア セット名]** ボックスに名前を入力します。 名前を指定しなかった場合、空の名前でメディア セットが作成されます。 メディア セット名を指定した場合は、メディア (テープまたはディスク) を調べて、実際の名前とここで入力した名前が一致するかどうかが確認されます。  
  
         メディア名を指定せずに、このチェック ボックスをオンにしてこのメディアを確認するよう指定した場合は、実際のメディア名も空でないとエラーになります。  
  
    -   **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]**  
  
         このオプションでは、 **[新しいメディア セット名]** ボックスに名前を入力し、必要に応じて **[新しいメディア セットの説明]** ボックスにメディア セットの説明を入力します。  
  
13. **[信頼性]** セクションで、必要に応じて次の項目をオンにします。  
  
    -   **[完了時にバックアップを検証する]** 。  
  
    -   **[メディアに書き込む前にチェックサムを行う]** 、および、必要に応じて、 **[チェックサム エラーのまま続行する]** 。 詳細については、「[バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)」を参照してください。  
  
14. **[全般]** ページの **[バックアップ先]** セクションで、テープ ドライブにバックアップするように指定した場合は、 **[バックアップ後にテープをアンロードする]** チェック ボックスがアクティブになります。 このオプションをオンにすると、 **[アンロードの前にテープを巻き戻す]** オプションがアクティブになります。  
  
    > [!NOTE]  
    >  **[全般]** ページの **[バックアップの種類]** で、トランザクション ログをバックアップするように指定しなかった場合、 **[トランザクション ログ]** セクションの各オプションは無効になっています。  
  
15. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降では、 [バックアップの圧縮](backup-compression-sql-server.md)がサポートされています。 既定では、バックアップが圧縮されるかどうかは、 **[バックアップ圧縮の既定]** サーバー構成オプションの値によって決まります。 ただし、現在のサーバー レベルの既定の設定にかかわらず、 **[バックアップを圧縮する]** をオンにしてバックアップを圧縮することも、 **[バックアップを圧縮しない]** をオンにして圧縮しないようにすることもできます。  
  
     **現在の backup compression default 値を表示するには**  
  
    -   [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
    > [!NOTE]  
    >  メンテナンス プラン ウィザードを使用して、データベースの差分バックアップを作成することもできます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-differential-database-backup"></a>データベースの差分バックアップを作成するには  
  
1.  次の項目を指定した BACKUP DATABASE ステートメントを実行し、データベースの差分バックアップを作成します。  
  
    -   バックアップするデータベースの名前。  
  
    -   データベースの完全バックアップを書き込むバックアップ デバイス。  
  
    -   DIFFERENTIAL 句。この句は、データベースの前回の完全バックアップの作成後に変更されたデータベースの部分だけをバックアップするときに指定します。  
  
     必須の構文は次のとおりです。  
  
     BACKUP DATABASE *database_name* TO <backup_device> WITH DIFFERENTIAL  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、 `MyAdvWorks` データベースの完全バックアップおよび差分バックアップを作成します。  
  
```sql  
-- Create a full database backup first.  
BACKUP DATABASE MyAdvWorks   
   TO MyAdvWorks_1   
   WITH INIT;  
GO  
-- Time elapses.  
-- Create a differential database backup, appending the backup  
-- to the backup device containing the full database backup.  
BACKUP DATABASE MyAdvWorks  
   TO MyAdvWorks_1  
   WITH DIFFERENTIAL;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [データベースの差分バックアップの復元 &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)   
 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [メンテナンス プラン](../maintenance-plans/maintenance-plans.md)   
 [ファイルの完全バックアップ &#40;SQL Server&#41;](full-file-backups-sql-server.md)  
  
  
