---
title: レプリケーション メンテナンス ジョブの実行 (SSMS)
description: SQL Server management Studio (SSMS) でレプリケーション メンテナンス ジョブを開始および停止する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server replication]
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: a84af3482d7c0b30010b474be8d9f93e4c468e00
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322007"
---
# <a name="run-replication-maintenance-jobs-sql-server-management-studio"></a>レプリケーション メンテナンス ジョブの実行 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーションでは以下のメンテナンス ジョブを使用します。  
  
-   **データ検証で問題が見つかったサブスクリプションの再初期化**  
  
-   **エージェント履歴のクリーンアップ: ディストリビューション**  
  
-   **ディストリビューションのレプリケーション モニターの状態更新機能**  
  
-   **レプリケーション エージェントの検査**  
  
-   **ディストリビューションのクリーンアップ: ディストリビューション**  
  
-   **有効期限が切れたサブスクリプションのクリーンアップ**  
  
 上記のジョブの開始および停止は、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] の **[ジョブ]** フォルダー、およびレプリケーション モニターの **[エージェント]** タブから行います。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。 各ジョブのプロパティの表示および変更は、同じフォルダーおよびタブからアクセスできる **[ジョブのプロパティ - \<Job>]** ダイアログ ボックスで行います。  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-management-studio"></a>Management Studio でレプリケーション メンテナンス ジョブを開始または停止するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でディストリビューターに接続して、サーバー ノードを展開します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[ジョブ]** フォルダーを展開します。  
  
3.  ジョブを右クリックして **[ジョブの開始]** または **[ジョブの停止]** をクリックします。  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-replication-monitor"></a>レプリケーション モニターでレプリケーション メンテナンス ジョブを開始または停止するには  
  
1.  レプリケーション モニターでパブリッシャー グループを展開し、パブリッシャーを選択します。  
  
2.  **[エージェント]** タブをクリックします。  
  
3.  グリッド内のジョブを右クリックして **[ジョブの開始]** または **[ジョブの停止]** をクリックします。  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-management-studio"></a>Management Studio でレプリケーション メンテナンス ジョブのプロパティを表示および変更するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でディストリビューターに接続して、サーバー ノードを展開します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[ジョブ]** フォルダーを展開します。  
  
3.  ジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ジョブのプロパティ - \<Job>]** ダイアログ ボックスで、必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-replication-monitor"></a>レプリケーション モニターでレプリケーション メンテナンス ジョブのプロパティを表示および変更するには  
  
1.  レプリケーション モニターでパブリッシャー グループを展開し、パブリッシャーを選択します。  
  
2.  **[エージェント]** タブをクリックします。  
  
3.  グリッド内のジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ジョブのプロパティ - \<Job>]** ダイアログ ボックスで、必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [パブリッシャーの情報を表示し、タスクを実行する &#40;レプリケーション モニター&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [レプリケーション エージェントの管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
