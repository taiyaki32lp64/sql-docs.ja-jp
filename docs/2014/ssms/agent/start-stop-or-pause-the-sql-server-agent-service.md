---
title: SQL Server エージェント サービスの開始、停止、または一時停止 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, starting
- SQL Server Agent, pausing
- SQL Server Agent, stopping
ms.assetid: c95a9759-dd30-4ab6-9ab0-087bb3bfb97c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f21d13149ffa90a2383e8f090b205b50efa54641
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63246136"
---
# <a name="start-stop-or-pause-the-sql-server-agent-service"></a>Start, Stop, or Pause the SQL Server Agent Service
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の SQL Server エージェント サービスを開始、停止、または一時停止する方法について説明します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスは、オペレーティング システムの起動時に自動的に開始するよう構成したり、ジョブの完了が必要なときに手動で開始できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを停止または一時停止して、ジョブ、オペレーターへの通知、および警告を中断できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [SQL Server Management Studio を使用して SQL Server エージェント サービスを開始、停止、または一時停止するには](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがサービスとして実行されている必要があります。 詳細については、「 [Configure SQL Server Agent](configure-sql-server-agent.md)」をご覧ください。  
  
-   オブジェクト エクスプローラーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ノードが表示されるのは、このノードの使用権限がある場合に限られます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの機能を実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定サーバー ロールの **sysadmin** のメンバーであるアカウントの資格情報を使用するように構成する必要があります。 このアカウントには、次の Windows 権限が必要です。  
  
-   サービスとしてログオン (SeServiceLogonRight)  
  
-   プロセス レベル トークンを置き換える (SeAssignPrimaryTokenPrivilege)  
  
-   スキャン チェックを行わない (SeChangeNotifyPrivilege)  
  
-   プロセスに対してメモリ クォータを調整する (SeIncreaseQuotaPrivilege)  
  
 必要な Windows 権限の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント サービス アカウントを参照してください[のアカウント、SQL Server エージェント サービスの選択](select-an-account-for-the-sql-server-agent-service.md)と[Windows サービス アカウントの構成とアクセス許可](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-start-stop-or-restart-the-sql-server-agent-service"></a>SQL Server エージェント サービスを開始、停止、または一時停止するには  
  
1.  **オブジェクト エクスプ ローラー**で、プラス記号をクリックして、管理する SQL Server エージェント サービスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[開始]**、 **[停止]**、または **[再起動]** を選択します。  
  
3.  **[ユーザー アカウント制御]** ダイアログ ボックスで、 **[はい]** をクリックします。  
  
4.  アクションを実行するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。  
  
 詳細については、以下をご覧ください。  
  
-   [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
-   [SQL Server エージェントの自動起動 (SQL Server Management Studio)](autostart-sql-server-agent-sql-server-management-studio.md)  
  
  
