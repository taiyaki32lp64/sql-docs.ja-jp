---
title: SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f8aee4e47fa655a95130860a517a3ffb3dff9304
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267339"
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
このトピックでは、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] で、SQL Server ツールにサーバーの状態を表示するように WMI を構成する方法について説明します。 サーバーに接続する際には、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]構成マネージャーだけでなく [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のコンポーネントである登録済みサーバーおよびオブジェクト エクスプローラーの両方で、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER) サービスおよび [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント (MSSQLSERVER) サービスの状態を取得するために、WMI (Windows Management Instrumentation) が使用されます。 サービスの状態を表示するには、WMI オブジェクトに対するリモート アクセスの権限が必要です。 このアクセス許可を構成するには、サーバーに WMI をインストールする必要があります。  
  
## <a name="SSMSProcedure"></a>WMI のアクセス許可を構成するには  
  
1.  リモート サーバーの **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。  
  
2.  **[名前]** ボックスに「 **wmimgmt.msc**」と入力し、 **[OK]** をクリックします。  
  
3.  **[Windows Management Infrastructure (WMI)]** の **[WMI コントロール (ローカル)]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[WMI コントロール (ローカル) のプロパティ]** ダイアログ ボックスの **[セキュリティ]** タブで、 **[Root]** を展開し、 **[CIMV2]** をクリックします。  
  
5.  **[セキュリティ]** をクリックして **[セキュリティ ROOT\CIMV2]** ダイアログ ボックスを開きます。  
  
6.  **[グループ名またはユーザー名]** ボックスにグループまたはユーザーを追加して選択します。  
  
7.  **[** _<group or user> のアクセス許可]_ ボックスで、サービスの状態をリモートから確認できるようにするユーザーの **[リモートの有効化]** の **[許可]** 列にあるチェック ボックスをオンにします。  
  
## <a name="see-also"></a>参照  
[SQL Server エージェント サービスの開始、停止、または一時停止](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
