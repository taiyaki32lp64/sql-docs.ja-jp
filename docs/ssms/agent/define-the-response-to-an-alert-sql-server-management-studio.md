---
title: 警告への応答の定義 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], responding to
- responding to alerts
ms.assetid: c86ca6eb-c59f-46e9-bc32-d474e7c3b170
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f1511e187fe18338aed364b43a5c75abc719574d
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553030"
---
# <a name="define-the-response-to-an-alert-sql-server-management-studio"></a>Define the Response to an Alert (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告に対して [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がどのように応答するかを定義する方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のバージョンでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントからポケットベル オプションと **net send** オプションが削除される予定です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  
  
-   SQL Server エージェントは、データベース メールを使用して、電子メールおよびポケットベルによる通知をオペレーターへ送信するように構成する必要があります。 詳細については、「 [オペレーターへの警告の割り当て](assign-alerts-to-an-operator.md)」を参照してください。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>Permissions  
警告に対する応答を定義できるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-define-the-response-to-an-alert"></a>警告に対する応答を定義するには  
  
1.  **オブジェクト エクスプローラー**で、応答を定義する警告を格納するサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[警告]** フォルダーを展開します。  
  
4.  応答を定義する警告を右クリックし、 **[プロパティ]** を選択します。  
  
5.  [_alert\_name_ **警告のプロパティ]** ダイアログ ボックスで、 **[ページの選択]** から **[応答]** を選択します。  
  
6.  **[ジョブの実行]** チェック ボックスをオンにし、 **[ジョブの実行]** チェック ボックスの下に表示されている一覧から、警告の発生時に実行するジョブを選択します。 **[新しいジョブ]** をクリックすることで、新しいジョブを作成できます。 **[ジョブの表示]** をクリックすると、ジョブに関するより詳しい情報を表示できます。 **[新しいジョブ]** ダイアログ ボックスと [**ジョブのプロパティ**_job\_name_] ダイアログ ボックスで使用できるオプションの詳細については、「[ジョブの作成](../../ssms/agent/create-a-job.md)」と「[ジョブの表示](../../ssms/agent/view-a-job.md)」を参照してください。  
  
7.  警告がアクティブになったときにオペレーターに通知する場合は、 **[オペレーターに通知する]** チェック ボックスをオンにします。 **[オペレーター一覧]** で、次のオペレーターに通知する方法を選択します (複数選択可)。 **[電子メール]** 、 **[ポケットベル]** 、または **[Net Send]** 。 **[新しいオペレーター]** をクリックすることで、新しいオペレーターを作成できます。 **[オペレーターの表示]** をクリックすることで、オペレーターに関するより詳しい情報を表示できます。 **[新しいオペレーター]** ダイアログ ボックスと **[オペレーターのプロパティの表示]** ダイアログ ボックスで使用できるオプションの詳細については、「 [Create an Operator](../../ssms/agent/create-an-operator.md) 」と「 [View Information About an Operator](../../ssms/agent/view-information-about-an-operator.md)」を参照してください。  
  
8.  完了したら、 **[OK]** をクリックします。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-define-the-response-to-an-alert"></a>警告に対する応答を定義するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- adds an e-mail notification for Test Alert.  
    -- assumes that Test Alert already exists and that
    -- François Ajenstat is a valid operator name   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
詳細については、「 [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)」を参照してください。  
  
