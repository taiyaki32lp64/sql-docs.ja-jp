---
title: データベース ミラーリング セッションの一時停止または再開 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- resuming database mirroring
- database mirroring [SQL Server], sessions
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: 05ede3b4-6abe-4442-abb7-9f5aee1d6bc0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52781de1cd4b6309f3ebeb9a2c59ae85b0b32dbd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754593"
---
# <a name="pause-or-resume-a-database-mirroring-session-sql-server"></a>データベース ミラーリング セッションの一時停止または再開 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でデータベース ミラーリングを一時停止または再開する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **ReplaceThisText:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [一時停止またはデータベース ミラーリングを再開した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 データベース ミラーリング セッションをいつでも中断して、ボトルネックの発生中にパフォーマンスを向上させることができます。また、中断したセッションはいつでも再開できます。  
  
> [!CAUTION]  
>  強制的なサービスの後に、最初のプリンシパル サーバーが再接続されると、ミラーリングが中断します。 この状況でミラーリングを再開すると、元のプリンシパル サーバーのデータが失われる可能性があります。 データ損失の可能性への対処の詳細については、「[データベース ミラーリング セッション中の役割の交代 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 データベース ミラーリング セッションを一時停止または再開するには、 **[データベースのプロパティ]** の [ミラーリング] ページを使用します。  
  
#### <a name="to-pause-or-resume-database-mirroring"></a>データベース ミラーリングを一時停止または再開するには  
  
1.  データベース ミラーリング セッション中にプリンシパル サーバー インスタンスに接続します。次に、オブジェクト エクスプローラーで、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開し、データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[ミラー]** をクリックします。 **[データベースのプロパティ]** ダイアログ ボックスの **[ミラーリング]** ページが開きます。  
  
4.  セッションを一時停止するには、 **[一時停止]** をクリックします。  
  
     確認を求めるメッセージが表示されます。 **[はい]** をクリックすると、セッションが一時停止し、ボタンが **[再開]** に変わります。  
  
     セッションを一時停止した場合の影響の詳細については、「[データベース ミラーリングの一時停止と再開 &#40;SQL Server&#41;](database-mirroring-sql-server.md)」を参照してください。  
  
5.  セッションを再開するには、 **[再開]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-pause-database-mirroring"></a>データベース ミラーリングを一時停止するには  
  
1.  いずれかのパートナーの [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
     ALTER DATABASE *database_name* SET PARTNER SUSPEND  
  
     *database_name* は、セッションを中断しようとしているミラー化データベースです。  
  
     次の例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースを一時停止します。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER SUSPEND;  
    ```  
  
##### <a name="to-resume-database-mirroring"></a>データベース ミラーリングを再開するには  
  
1.  いずれかのパートナーの [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の Transact-SQL ステートメントを実行します。  
  
     ALTER DATABASE *database_name* SET PARTNER RESUME  
  
     *database_name* は、再開するセッションのミラー化されたデータベースです。  
  
     次の例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースを一時停止します。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER RESUME;  
    ```  
  
##  <a name="FollowUp"></a>補足情報: 一時停止またはデータベース ミラーリングを再開した後  
  
-   **データベース ミラーリングを一時停止した後**  
  
     プライマリ データベースで、トランザクション ログが満杯にならないように予防策をとります。 詳細については、「 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください。  
  
-   **データベース ミラーリングを再開した後**  
  
     データベース ミラーリングを再開することで、ミラー データベースを SYNCHRONIZING 状態にします。 安全性レベルが FULL の場合、プリンシパルに対するミラーの遅れが解消され、ミラー データベースが SYNCHRONIZED 状態になります。 この時点で、フェールオーバーが可能になります。 ミラーリング監視サーバーが存在していて、オンになっている場合は、自動フェールオーバーが可能です。 ミラーリング監視サーバーが存在しない場合は、手動フェールオーバーが可能です。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベース ミラーリングを削除する &#40;SQL Server&#41;](remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
