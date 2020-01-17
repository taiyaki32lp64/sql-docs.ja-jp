---
title: SQL Server (SQL Server 構成マネージャー) のインスタンスの自動開始の回避 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6af4597a4ddf802c80bc98cb38363d59348fa0bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810052"
---
# <a name="prevent-automatic-startup-of-an-instance-of-sql-server-sql-server-configuration-manager"></a>SQL Server のインスタンスの自動開始の回避 (SQL Server 構成マネージャー)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で SQL Server 構成マネージャーを使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスが自動的に開始されないようにする方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は通常、自動的に開始するように構成されます。 インスタンスの開始モードを手動に設定することによって、その構成を変更できます。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>SQL Server のインスタンスの自動開始を回避するには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  [SQL Server 構成マネージャー] で **[サービス]** を展開し、 **[SQL Server]** をクリックします。  
  
3.  詳細ペインで、 **[MSSQLServer]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[SQL Server \<** _instancename_ **> のプロパティ]** ダイアログ ボックスの **[プロパティ]** ボックスで、 **[開始モード]** の値を **[手動]** に設定します。  
  
5.  **[OK]** をクリックして **[SQL Server \<** _instancename_ **> のプロパティ]** ダイアログ ボックスを閉じ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを閉じます。  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](start-stop-pause-resume-restart-sql-server-services.md)  
  
  
