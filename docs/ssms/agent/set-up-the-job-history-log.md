---
title: ジョブ履歴ログのセットアップ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e7a802b3bf5e3ef8842ba01f3c95237b67adb3d3
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263051"
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログをセットアップする方法について説明します。  
  
-   **作業を開始する準備:** [セキュリティ](#Security)  
  
-   **ジョブ履歴ログをセットアップするには、次を使用します。** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
**ジョブ履歴ログをセットアップするには**  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[SQL Server エージェントのプロパティ]** ダイアログ ボックスで **[履歴]** ページをクリックします。  
  
4.  次のいずれかのオプションを選択します。  
  
    1.  **[ジョブ履歴ログのサイズを制限する]** チェック ボックスをオンにして、ジョブ履歴ログの最大行数と、ジョブあたりの最大行数を入力します。  
  
    2.  **[自動的にエージェントの履歴を削除する]** チェック ボックスをオンにして、期間を指定します。この期間を過ぎると、履歴がログから削除されます。  
  
## <a name="see-also"></a>参照  
[ジョブの実装](../../ssms/agent/implement-jobs.md)  
[ジョブの利用状況の監視](../../ssms/agent/monitor-job-activity.md)  
[ジョブの作成](../../ssms/agent/create-jobs.md)  
  
