---
title: ジョブ履歴ログのサイズの変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1a8c9ab517d1f6a122144604d6b147e6f5eeaf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650889"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログのサイズ制限を設定する方法について説明します。  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **ジョブ履歴ログのサイズ制限を設定する方法:**  
  
     [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-resize-the-job-history-log-based-on-raw-size"></a>生のサイズに基づいてジョブ履歴ログのサイズを変更するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[履歴]** ページを選択し、 **[ジョブ履歴ログのサイズを制限する]** チェック ボックスがオンになっていることを確認します。  
  
4.  **[ジョブ履歴ログの最大サイズ (行)]** ボックスで、ジョブ履歴ログに使用できる最大行数を入力します。  
  
5.  **[ジョブごとのジョブ履歴の最大行数]** ボックスで、1 つのジョブに使用できるジョブ履歴の最大行数を入力します。  
  
#### <a name="to-resize-the-job-history-log-based-on-time"></a>時間に基づいてジョブ履歴ログのサイズを変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[履歴]** ページを選択し、 **[自動的にエージェントの履歴を削除する]** チェック ボックスをオンにします。  
  
4.  適切な **[日]** 、 **[週]** 、または **[月]** を選択します。  
  
  
