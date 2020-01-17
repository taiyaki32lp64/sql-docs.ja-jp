---
title: CPU のアイドル時間と期間の設定 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a355108635799d03c2859b6c47eaaf8acc87dc7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63185553"
---
# <a name="set-cpu-idle-time-and-duration-sql-server-management-studio"></a>CPU のアイドル時間と期間の設定 (SQL Server Management Studio)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、サーバーの CPU アイドル状態を定義する方法について説明します。 CPU アイドルの定義は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがイベントに応答する方法に影響します。 たとえば、CPU の平均使用率が 10% 未満になり、そのレベルで 10 分間経過したときを CPU アイドル状態であると定義するとします。 この場合に、サーバーの CPU がアイドル状態になるたびにジョブが実行されるように定義していると、CPU 使用率が 10% 未満になり、その使用率のまま 10 分間経過したときにジョブが開始されます。 このジョブがサーバーのパフォーマンスに大きな影響を及ぼす場合、CPU アイドル状態をどのように定義するかが重要になります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>CPU のアイドル時間と期間を設定するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックして、 **[詳細設定]** ページをクリックします。  
  
3.  **[CPU のアイドル状態]** で、次の操作を行います。  
  
    -   **[CPU のアイドル状態を定義する]** チェック ボックスをオンにします。  
  
    -   **[CPU の平均使用量が次の値以下になったとき]** ボックスで、比率を指定します (全 CPU 共通)。 これにより、CPU がその値を下回ったときにアイドル状態と見なす使用率が設定されます。  
  
    -   **[かつ、この使用率以下で次の期間を経過]** ボックスで、秒数を指定します。 低い CPU 使用率のまま、ここで設定した秒数が経過すると、CPU がアイドル状態であると見なされます。  
  
  
