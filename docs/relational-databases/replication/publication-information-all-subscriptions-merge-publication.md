---
title: すべてのサブスクリプション (マージ - SSMS)
description: SQL Server Management Studio (SSMS) で選択したマージ パブリケーションの [すべてのサブスクリプション] タブを選択します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.allsubscriptions.merge.f1
ms.assetid: 0f4fa946-a0d9-4d3b-b90b-53503c40fba2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 619406c884ec5067f569178094f9a3a0c05634e6
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321422"
---
# <a name="publication-information-all-subscriptions-merge-publication"></a>パブリケーション情報、[すべてのサブスクリプション] (マージ パブリケーション)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[すべてのサブスクリプション]** タブには、選択したマージ パブリケーションに対するすべてのサブスクリプションの情報が表示されます。  
  
## <a name="options"></a>オプション  
 サブスクリプションに関する詳細情報やタスクを調べるには、そのサブスクリプションの行を右クリックし、ショートカット メニューのオプションをクリックします。 グリッドにデータを表示する方法を変更するには、グリッドを右クリックし、次のいずれかのオプションをクリックします。  
  
-   **[並べ替え]** : **[列の並べ替え]** ダイアログ ボックスで、1 つ以上の列を基準にして並べ替えを行います。  
  
-   **[表示する列の選択]** : **[列の選択]** ダイアログ ボックスで、表示する列とその表示順序を選択します。  
  
-   **フィルター**: **[フィルターの設定]** ダイアログ ボックスで、列の値に基づいてグリッドの行をフィルター処理します。  
  
-   **[フィルターのクリア]** :グリッドのフィルター設定をすべてクリアします。  
  
 フィルター設定は各グリッドに固有です。 列の選択と並べ替えは、各パブリッシャーのパブリケーション グリッドなど、同じ種類のすべてのグリッドに適用されます。  
  
 **[表示]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 サブスクリプション状態を選択すると、選択した種類の状態のサブスクリプションが表示されます。 たとえば、エラーを含むサブスクリプションのみを表示するように設定できます。  
  
 **状態**  
 各サブスクリプションの状態です。これは、マージ エージェントの状態により決定されます。  
  
 既定では、サブスクリプションの情報を表示するグリッドは **[状態]** 列の順序で並べられています (同じ状態のサブスクリプションは、 **[パフォーマンス]** 列の順序で並べられています)。 表示される状態の値と、その値の並べ替え順 (たとえば、エラーは常にグリッドの上部に表示されます) を次に示します。  
  
-   エラー  
  
-   [パフォーマンス クリティカル]\([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみ)  
  
-   [長期マージ]\([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみ)  
  
-   [まもなく期限切れ/期限切れ] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみ)  
  
-   [初期化されていないサブスクリプション]\([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみ)  
  
-   [失敗したコマンドの再試行]  
  
-   [同期中]  
  
-   [同期されていません]  
  
 特定のサブスクリプションが複数の状態である場合に表示される値も、並べ替え順によって決まります。 たとえば、サブスクリプションにエラーがあり、まもなく期限切れになる場合、 **[状態]** 列には **[エラー]** と表示されます。  
  
 状態値 **[パフォーマンス クリティカル]** 、 **[長期マージ]** 、 **[まもなく期限切れ/期限切れ]** 、および **[初期化されていないサブスクリプション]** は警告です。 警告が表示される場合、 **[状態]** 列にはエージェントが同期中かどうかも表示されます。 たとえば、 **[同期中]、[パフォーマンス クリティカル]** という形で状態が表示されます。  
  
 状態値 **[まもなく期限切れ/期限切れ]** および **[長期マージ]** は、しきい値が設定されている場合のみ表示されます。 **[パフォーマンス クリティカル]** の状態の値は、同じ種類の接続 (ダイヤルアップまたは LAN) によるサブスクリプションの同期が 5 回行われた後にのみ表示されます。 パフォーマンスの測定としきい値の設定については、「[Monitor Performance with Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)」 (レプリケーション モニターを使用したパフォーマンスの監視) と「[レプリケーション モニターのしきい値と警告の設定](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」を参照してください。  
  
 **サブスクリプション**  
 各サブスクリプションの名前です。*SubscriberName:SubscriptionDatabaseName* という形式になります。  
  
 **表示名**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 各サブスクリプションの説明です。 この説明は、 **[サブスクリプションのプロパティ]** ダイアログ ボックスで入力するか、[sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) または [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md) の `@description` パラメーターで示します。 多くの場合、この説明は "表示名"、つまりサブスクリプションの通称として使用されます。  
  
 **パフォーマンス**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 各サブスクリプションのパフォーマンス評価です。これはレプリケーション モニターにより取得された、最新の配信率の計測結果に基づいています。 パフォーマンス評価は、接続の種類が同じ (ダイヤルアップまたは LAN) パブリケーションに対するサブスクリプションの履歴の平均パフォーマンスと、個々のサブスクリプションのパフォーマンスを比較することで決定されます。 レプリケーション モニターには、50 以上の変更を伴う同期がそれぞれ同じ種類の接続により 5 回行われた後で、値が表示されます。 50 以上の変更を伴う同期が 5 回未満の場合、または最新の同期における変更が 50 未満の場合には、この列は空白になります。  
  
> [!NOTE]  
>  パフォーマンスは、 **[接続]** 列に表示される接続の種類に基づいて決まります。したがって、配信率が低いサブスクリプションが低速の接続で同期されている場合、配信率が高いサブスクリプションよりも高いパフォーマンスが表示される可能性があります。  
  
 パフォーマンス評価は、次のいずれかの値になります。  
  
-   [非常に良い]  
  
-   [良い]  
  
-   [普通]  
  
-   悪い  
  
 パフォーマンス評価の定義方法とパフォーマンスしきい値の設定方法については、「[Monitor Performance with Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)」 (レプリケーション モニターを使用したパフォーマンスの監視) を参照してください。  
  
 **[配信率]**  
 マージ エージェントにより 1 秒間に処理される行数です。  
  
 **[最後の同期]**  
 マージ エージェントが最後に実行された時刻です。 この同期では変更が処理されていることも、処理されていないこともあります。 同期が進行中の場合、進行状況を示すパーセント値が表示されます。  
  
 **Duration**  
 最後の同期中におけるマージ エージェントの実行時間です。 マージ エージェントが現在同期中の場合、これは経過時間を表します。マージ エージェントが以前に同期された場合、これは合計時間を表します。  
  
 **[接続]**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 サブスクライバーとパブリッシャーの接続の種類です。 **[LAN]** 、 **[ダイヤルアップ]** 、 **[インターネット]** のいずれかの値になります。 サブスクリプションで Web 同期が使用されている場合、 **[インターネット]** が表示されます。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [マージ レプリケーションの Web 同期](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
