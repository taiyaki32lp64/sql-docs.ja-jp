---
title: パブリッシャー情報、[パブリケーション] | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: a0590a339b6357bdc102420c4c68d4a92fc0519c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764078"
---
# <a name="publisher-information-publications"></a>パブリッシャー情報、[パブリケーション]
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[パブリケーション]** タブを使用すると、左ペインで選択したパブリッシャーにおけるすべてのパブリケーションに関する要約情報を取得できます。  
  
## <a name="options"></a>オプション  
 グリッドにデータを表示する方法を変更するには、グリッドを右クリックし、次のいずれかのオプションをクリックします。  
  
-   **[並べ替え]** : **[列の並べ替え]** ダイアログ ボックスで、1 つ以上の列を基準にして並べ替えを行います。  
  
-   **[表示する列の選択]** : **[列の選択]** ダイアログ ボックスで、表示する列とその表示順序を選択します。  
  
-   **[フィルター]** : **[フィルターの設定]** ダイアログ ボックスで、列の値に基づいてグリッドの行をフィルター処理します。  
  
-   **[フィルターのクリア]** :グリッドのフィルター設定をすべてクリアします。  
  
 フィルター設定は各グリッドに固有です。 列の選択と並べ替えは、各パブリッシャーのパブリケーション グリッドなど、同じ種類のすべてのグリッドに適用されます。  
  
 **ステータス**  
 各パブリケーションの状態です。これは、サブスクリプションの最も優先度の高い状態により決定されます。 既定では、パブリケーション情報を表示するグリッドは **[状態]** 列の順序で並べられています。 表示される状態の値と、その値の並べ替え順 (たとえば、エラーは常にグリッドの上部に表示されます) を次に示します。  
  
-   Error  
  
-   [パフォーマンス クリティカル]  
  
-   [失敗したコマンドの再試行]  
  
-   [OK]  
  
 **[パフォーマンス クリティカル]** 状態は、トランザクション サブスクリプションとマージ サブスクリプションに関連しています。トランザクション サブスクリプションの場合は、しきい値が設定されている場合にのみ表示されます。 パフォーマンスの測定としきい値の設定については、「[Monitor Performance with Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)」 (レプリケーション モニターを使用したパフォーマンスの監視) と「[レプリケーション モニターのしきい値と警告の設定](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」を参照してください。  
  
 **パブリケーション**  
 各パブケーションの名前です。*PublicationDatabaseName:PublicationName* という形式になります。  
  
 **サブスクリプション**  
 各パブリケーションのサブスクリプションの数です。  
  
 **[同期中]**  
 各パブリケーションにおいて現在同期しているサブスクリプションの数です。  
  
-   トランザクション サブスクリプションが "同期" している場合、ディストリビューション エージェントが実行されていても、データは必ずしもレプリケートされるとは限りません。  
  
-   マージ レプリケーションが "同期" している場合、マージ エージェントは実行されており、データは現在レプリケートされています。  
  
-   スナップショット レプリケーションが "同期" している場合、ディストリビューション エージェントは実行されており、データは現在レプリケートされています。  
  
 **[現在の平均パフォーマンス]** と **[現在の最低パフォーマンス]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンのみです。 それぞれ、パブリケーションに対するすべてのサブスクリプションの、平均パフォーマンスと最低パフォーマンスの評価を表します。 評価は、レプリケーション モニターにより取得された最新の計測結果に基づいています。サブスクリプションの経過的なパフォーマンスは反映されません。  
  
 トランザクション レプリケーションの場合、レプリケーション モニターには、パフォーマンスしきい値が定義されているパブリケーションに対してのみ値が表示されます。 パブリケーションにパフォーマンスしきい値が定義されていない場合、この列には **[有効になっていません]** と表示されます。 マージ レプリケーションの場合、レプリケーション モニターには、50 以上の変更を伴う同期がそれぞれ同じ種類の接続 (ダイヤルアップまたは LAN) により 5 回行われた後で、値が表示されます。 50 以上の変更を伴う同期が 5 回未満の場合、または最新の同期における変更が 50 未満の場合には、この列は空白になります。  
  
 パフォーマンス評価は、次のいずれかの値になります。  
  
-   [非常に良い]  
  
-   [良い]  
  
-   [普通]  
  
-   悪い  
  
-   重大  
  
 パフォーマンス評価の定義方法とパフォーマンスしきい値の設定方法については、「[Monitor Performance with Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)」 (レプリケーション モニターを使用したパフォーマンスの監視) を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [パブリッシャーの情報を表示し、タスクを実行する &#40;レプリケーション モニター&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
