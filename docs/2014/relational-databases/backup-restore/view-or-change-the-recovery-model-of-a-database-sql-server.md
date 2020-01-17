---
title: データベースの復旧モデルの表示または変更 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4bc7254d8a3eafa3c7c7d152d323051a3c5bea94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875081"
---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>データベースの復旧モデルの表示または変更 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)]でデータベースの復旧モデルを表示または変更する方法について説明します。 *復旧モデル*は、トランザクションをログに記録する方法、トランザクション ログのバックアップを必須 (および可能) にするかどうか、利用できる復元操作の種類などを制御するデータベース プロパティです。 復旧モデルの種類は、単純、完全、および一括ログの 3 種類です。 通常、データベースには完全復旧モデルまたは単純復旧モデルが使用されます。 データベースは、任意の時点で別の復旧モデルに切り替えることができます。 **model** データベースは、新しいデータベースの既定の復旧モデルを設定します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **表示または変更、データベースの復旧モデルを使用します。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足の推奨事項。** [復旧モデルを変更した後](#FollowUp)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   完全復旧モデルまたは一括ログ復旧モデルから切り替える前に、トランザクション ログをバックアップしてください。  
  
-   一括ログ復旧モデルでは特定の時点に復旧できません。 そのため、一括ログ復旧モデルでトランザクション ログの復元を必要とするトランザクションを実行すると、データが失われる可能性があります。 災害復旧シナリオでデータをより確実に復旧するには、次の条件下でのみ一括ログ復旧モデルに切り替えることをお勧めします。  
  
    -   ユーザーが現在データベースで許可されていない場合。  
  
    -   一括処理中に行われたすべての変更が、ログ バックアップを行うかどうかに関係なく復旧可能な場合 (一括処理の再実行など)。  
  
     この 2 つの条件を満たす場合は、一括ログ復旧モデルでバックアップされたトランザクション ログの復元中に、データが失われることはありません。  
  
> [!NOTE]  
>  一括操作中に完全復旧モデルに切り替える場合は、一括操作のログ記録が最小ログ記録から完全ログ記録に変わり、また、その逆も同様です。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-change-the-recovery-model"></a>復旧モデルを表示または変更するには  
  
1.  適切な [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスへの接続後、オブジェクト エクスプローラーでサーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックし、 **[プロパティ]** をクリックすると、 **[データベースのプロパティ]** ダイアログ ボックスが開きます。  
  
4.  **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
5.  **[復旧モデル]** ボックスの一覧に現在の復旧モデルが表示されています。  
  
6.  復旧モデルを変更する必要がある場合は、別のモデルをこの一覧で選択します。 選択できるのは、 **[完全]** 、 **[一括ログ]** 、 **[単純]** のいずれかです。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-the-recovery-model"></a>復旧モデルを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) カタログ ビューにクエリを実行して、 **model** データベースの復旧モデルを確認する方法を示します。  
  
```sql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>復旧モデルを変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 `model` ALTER DATABASE `FULL` ステートメントの `SET RECOVERY` オプションを使用して、 [データベース内の復旧モデルを](/sql/t-sql/statements/alter-database-transact-sql-set-options) に変更する方法を示します。  
  
```sql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="FollowUp"></a> 補足の推奨事項。復旧モデルを変更した後  
  
-   **完全復旧モデルと一括ログ復旧モデルの切り替え後の処理**  
  
    -   一括操作の完了後、すぐに完全復旧モードに戻してください。  
  
    -   一括ログ復旧モデルから完全復旧モデルに戻した後に、ログをバックアップしてください。  
  
        > [!NOTE]  
        >  バックアップ ストラテジは変更されません。つまり、データベースのバックアップ、ログ バックアップ、および差分バックアップが引き続き定期的に実行されます。  
  
-   **単純復旧モデルからの切り替え後の処理**  
  
    -   完全復旧モデルまたは一括ログ復旧モデルに切り替えた直後に、データベースの完全バックアップまたはデータベースの差分バックアップを作成し、ログ チェーンを開始します。  
  
        > [!NOTE]  
        >  完全復旧モデルまたは一括ログ復旧モデルへの切り替えは、最初のデータ バックアップ後に有効になります。  
  
    -   定期的なログ バックアップをスケジュールし、それに応じて復元プランを更新します。  
  
        > [!IMPORTANT]  
        >  ログのバックアップ頻度が不十分な場合、トランザクション ログが拡大し、領域不足になる可能性があります。  
  
-   **単純復旧モデルへの切り替え後の処理**  
  
    -   トランザクション ログをバックアップするためのスケジュールが設定されたすべてのジョブを停止します。  
  
    -   定期的なデータベースのバックアップがスケジュールされていることを確認します。 データの保護と、トランザクション ログのアクティブでない部分の切り捨ての両方にとって、データベースのバックアップは重要です。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [ジョブの作成](../../ssms/agent/create-a-job.md)  
  
-   [ジョブの有効化または無効化](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [メンテナンス プラン](../maintenance-plans/maintenance-plans.md) ( [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] オンライン ブック)  
  
## <a name="see-also"></a>関連項目  
 [復旧モデル &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [復旧モデル &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
