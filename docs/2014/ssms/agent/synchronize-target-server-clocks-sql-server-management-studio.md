---
title: ターゲット サーバーのクロックの同期 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 769b2b9caba541af3a1ea38e1969d8a6422950be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68188764"
---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>ターゲット サーバーのクロックの同期 (SQL Server Management Studio)
  このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のターゲット サーバーのクロックとマスター サーバーのクロックを同期する方法について説明します。 これらのシステム クロックの同期をとると、ジョブのスケジュールを効果的に管理できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **対象サーバーのクロックの同期をとる方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-synchronize-target-server-clocks"></a>ターゲット サーバーのクロックを同期するには  
  
1.  **オブジェクト エクスプローラー** で、対象サーバーのクロックとマスター サーバーのクロックの同期をとるサーバーをプラス記号をクリックして展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして、 **[対象サーバーの管理]** を選択します。  
  
3.  **[対象サーバーの管理]** ダイアログ ボックスで **[命令を通知]** をクリックします。  
  
4.  **[命令の種類]** ボックスの一覧で、 **[クロックの同期]** を選択します。  
  
5.  **[受信者]** で、次のいずれかの操作を行います。  
  
    -   すべてのターゲット サーバーのクロックとマスター サーバーのクロックを同期するには、 **[すべてのターゲット サーバー]** をクリックします。  
  
    -   特定のサーバーのクロックを同期するには、 **[特定のターゲット サーバー]** をクリックし、マスター サーバーのクロックと同期するターゲット サーバーを選択します。  
  
6.  完了したら、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-synchronize-target-server-clocks"></a>ターゲット サーバーのクロックを同期するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_resync_targetserver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)します。  
  
  
