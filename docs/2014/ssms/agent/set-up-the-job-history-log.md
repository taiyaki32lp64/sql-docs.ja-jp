---
title: ジョブ履歴ログのセットアップ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 613c0ccae7be912bd3bec63905b838b7f07b59b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033581"
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
  このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログをセットアップする方法について説明します。  
  
-   **作業を開始する準備:** [Security](#Security)  
  
-   **ジョブ履歴ログをセットアップするには、次を使用します。** [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
 **ジョブ履歴ログをセットアップするには**  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[SQL Server エージェントのプロパティ]** ダイアログ ボックスで **[履歴]** ページをクリックします。  
  
4.  次のいずれかのオプションを選択します。  
  
    1.  **[ジョブ履歴ログのサイズを制限する]** チェック ボックスをオンにして、ジョブ履歴ログの最大行数と、ジョブあたりの最大行数を入力します。  
  
    2.  **[自動的にエージェントの履歴を削除する]** チェック ボックスをオンにして、期間を指定します。この期間を過ぎると、履歴がログから削除されます。  
  
## <a name="see-also"></a>参照  
 [ジョブの実装](implement-jobs.md)   
 [モニターのジョブの利用状況](monitor-job-activity.md)   
 [ジョブの作成](create-jobs.md)  
  
  
