---
title: エージェント (スナップショット - SSMS)
description: SQL Server Management Studio (SSMS) の [スナップショット エージェント] ページの [エージェント] タブについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.snapshot.f1
ms.assetid: 599ff80b-392c-43aa-9db2-dc4ed33d4f6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 9dd77881ddcc235966333c95e4a5a18180926f8c
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321879"
---
# <a name="publication-information-agents-snapshot-publication"></a>パブリケーション情報、[エージェント] (スナップショット パブリケーション)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[エージェント]** タブには、選択したパブリケーションのスナップショット エージェントに関する概要情報が表示されます。  
  
## <a name="options"></a>オプション  
 スナップショット エージェントに関する詳細情報やタスクを調べるには、そのエージェントの行を右クリックし、ショートカット メニューのオプションをクリックします。 グリッドにデータを表示する方法を変更するには、グリッドを右クリックし、次のいずれかのオプションをクリックします。  
  
-   **[並べ替え]** : **[列の並べ替え]** ダイアログ ボックスで、1 つ以上の列を基準にして並べ替えを行います。  
  
-   **[表示する列の選択]** : **[列の選択]** ダイアログ ボックスで、表示する列とその表示順序を選択します。  
  
-   **フィルター**: **[フィルターの設定]** ダイアログ ボックスで、列の値に基づいてグリッドの行をフィルター処理します。  
  
-   **[フィルターのクリア]** :グリッドのフィルター設定をすべてクリアします。  
  
 フィルター設定は各グリッドに固有です。 列の選択と並べ替えは、各パブリッシャーのパブリケーション グリッドなど、同じ種類のすべてのグリッドに適用されます。  
  
 **状態**  
 スナップショット エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   エラー  
  
-   [失敗したコマンドの再試行]  
  
-   [実行されていません]  
  
-   [完了]  
  
 **エージェント**  
 スナップショット エージェント。 スナップショット パブリケーションに関連付けられた唯一のエージェントです。 ディストリビューション エージェントは、このパブリケーションに対するサブスクリプションに関連付けられます。 詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
 **[前回の開始時刻]**  
 エージェントが最後に起動された時刻です。  
  
 **Duration**  
 エージェントが実行された時間の長さです。 この時間は、エージェントが現在実行中の場合は経過時間、エージェントが以前に実行されている場合は合計時間を表します。  
  
 **[最後のアクション]**  
 エージェントが最後に実行されたときに最後に実行されたアクションです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
