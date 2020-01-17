---
title: ディストリビューターからサブスクライバーまでの履歴 (スナップショット)
description: SQL Server Management Studio (SSMS) 内にあるスナップショット パブリケーションのレプリケーション モニターの [ディストリビューターからサブスクライバーまでの履歴] タブについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.pubtodist.snapshot.f1
ms.assetid: d3575964-f287-4bcf-8d2e-f81a33141b25
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 460ab1ee21fd09c423316e7f4893dd6875d43130
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321684"
---
# <a name="subscription-distributor-to-subscriber-history-snapshot-subscription"></a>サブスクリプション、[ディストリビューターからサブスクライバーまでの履歴] (スナップショット サブスクリプション)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[ディストリビューターからサブスクライバーまでの履歴]** タブでは、ステータス、履歴、情報メッセージ、およびすべてのエラー メッセージを含む、ディストリビューション エージェントの詳細情報が表示されます。  
  
## <a name="options"></a>オプション  
 表示するディストリビューション エージェントのセッションを **[表示]** メニューで選択した後、 **[ディストリビューション エージェントのセッション]** というラベルのグリッドで特定のセッションを選択します。 このセッションの詳細情報は、 **[選択されたセッションのアクション]** というラベルのグリッドに表示されます。 選択したセッションがエラーで終了した場合は、 **[選択されたセッションのエラーの詳細またはメッセージ]** というラベルのテキスト領域も表示されます。  
  
 **表示**  
 表示するディストリビューション エージェントのセッションを選択します。  
  
 **状態**  
 ディストリビューション エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   エラー  
  
-   [完了]  
  
-   [再試行中]  
  
-   実行中  
  
 **Start Time**  
 セッションの開始時刻です。  
  
 **[終了時刻]**  
 セッションの終了時刻です。 エージェントが停止していない場合は、このフィールドは空になっています。  
  
 **Duration**  
 このセッションでディストリビューション エージェントが実行された時間の合計です。 エージェントが現在実行中の場合、経過時間を表します。エージェントが終了している場合、セッションの合計時間を表します。  
  
 **エラー メッセージ**  
 セッションがエラーで終了した場合は、ディストリビューション エージェントによって記録された最新のエラー メッセージがこのフィールドに表示されます。 セッションがエラーで終了しなかった場合は、このフィールドは空白です。  
  
 **[動作メッセージ]**  
 選択したセッション中に、ディストリビューション エージェントによってログに記録された、すべての情報メッセージとエラー メッセージです。  
  
 **[動作時間]**  
 **[動作メッセージ]** 列で説明されたアクションが実行された時間です。  
  
 **[選択されたセッションのエラーの詳細またはメッセージ]**  
 選択したセッションの **[状態]** 列に **[エラー]** の値が表示されている場合にのみ表示されます。 このテキスト領域では、エラーの詳細情報とエラーの発生時に試行されたコマンドが表示されます。 エラーに関連する追加コンテンツへのリンクも含まれます。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
