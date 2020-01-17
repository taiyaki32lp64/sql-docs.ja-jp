---
title: ジョブ履歴ログのサイズの変更 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5dea3b0a7eb9076bb778a14a4c8ab1834df0b93e
ms.sourcegitcommit: 58f1d5498c87bfe0f6ec4fd9d7bbe723be47896b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995838"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md.md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログのサイズ制限を設定する方法について説明します。
  
-   **作業を開始する準備:**  
  
    [セキュリティ](#Security)  
  
-   **ジョブ履歴ログのサイズ制限を設定する方法:**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
*生のサイズに基づいてジョブ履歴ログのサイズを変更するには*
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[履歴]** ページを選択し、 **[ジョブ履歴ログのサイズを制限する]** がオンになっていることを確認します。  
  
4.  **[ジョブ履歴ログの最大サイズ (行)]** ボックスで、ジョブ履歴ログに使用できる最大行数を入力します。  
  
5.  **[ジョブごとのジョブ履歴の最大行数]** ボックスで、1 つのジョブに使用できるジョブ履歴の最大行数を入力します。  
  
**時間に基づいてジョブ履歴ログのサイズを変更するには:**
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[履歴]** ページを選択し、 **[自動的にエージェントの履歴を削除する]** チェック ボックスをオンにします。  
  
4.  適切な **[日]** 、 **[週]** 、または **[月]** を選択します。  
  
