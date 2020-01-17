---
title: オペレーターへの警告の割り当て | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- assigning alerts to operator
- SQL Server Agent, alerts
- alerts [SQL Server], assigning to operator
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: aa818155-6fa2-4565-a09f-5c7e31c89754
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 905114d0190a7d1e8441e98249664c985a433988
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473213"
---
# <a name="assign-alerts-to-an-operator"></a>オペレーターへの警告の割り当て
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告をオペレーターに割り当てて、ジョブに関する通知を受信できるようにする方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **オペレーターに警告を割り当てる方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。 警告システムを構成するときには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用することをお勧めします。  
  
-   警告に対応して通知を送るには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがメールを送れるようにあらかじめ構成しておく必要があります。 詳細については、「 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)」を参照してください。  
  
-   電子メールのメッセージやポケットベルによる通知に失敗した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス エラー ログに失敗がレポートされます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 オペレーターに警告を割り当てることができるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-assign-alerts-to-an-operator"></a>オペレーターに警告を割り当てるには  
  
1.  **オブジェクト エクスプローラー**で、警告を割り当てるオペレーターを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[オペレーター]** フォルダーを展開します。  
  
4.  警告を割り当てるオペレーターを右クリックし、 **[プロパティ]** を選択して、 **[通知]** ページを選択します。  
  
5.  [_operator_name_ **のプロパティ]** ダイアログ ボックスで、 **[ページの選択]** の **[通知]** を選択します。  
  
6.  **[このユーザーに送信された通知の表示方法]** で、 **[警告]** を選択してこのオペレーターに送信する警告の一覧を表示するか、または **[ジョブ]** を選択してこのオペレーターに通知を送信するジョブの一覧を表示します。 次のチェック ボックスの中から 1 つまたは複数を選択し、必要に応じて通知ごとに通知方法を定義します: **[電子メール]** 、 **[ポケットベル]** 、または **[Net Send]** 。  
  
7.  完了したら、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-assign-alerts-to-an-operator"></a>オペレーターに警告を割り当てるには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists and that Fran??ois Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'Fran??ois Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_add_notification &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)します。  
  
  
