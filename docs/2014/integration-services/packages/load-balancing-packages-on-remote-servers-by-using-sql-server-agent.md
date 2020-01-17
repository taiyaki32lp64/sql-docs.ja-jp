---
title: リモート サーバー上での SQL Server エージェントを使用したパッケージの負荷分散 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- load-balancing [Integration Services]
- parent packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 9281c5f8-8da3-4ae8-8142-53c5919a4cfe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7c1f4792d97ae82561f0d05fe9754daae0a2bf3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62890175"
---
# <a name="load-balancing-packages-on-remote-servers-by-using-sql-server-agent"></a>リモート サーバー上での SQL Server エージェントを使用したパッケージの負荷分散
  実行する必要のあるパッケージが数多くある場合、使用可能な他のサーバーでパッケージを実行すると便利です。 すべてのパッケージを 1 つの親パッケージで管理している場合に、他のサーバーを使用してパッケージを実行するこの方法を、負荷分散といいます。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の負荷分散は、手動による方法であり、パッケージの所有者が構築する必要があります。 負荷分散は、サーバーで自動的には実行されません。 また、リモート サーバーで実行するパッケージは、他のパッケージ内の個別のタスクではなく、完全なパッケージである必要があります。  
  
 負荷分散は、次のようなシナリオで役に立ちます。  
  
-   複数のパッケージを同時実行できる。  
  
-   個々のパッケージが大きく、順番に実行すると、処理許容時間を超えて実行される可能性がある。  
  
 管理者や設計者は、処理に他のサーバーを使用することに利点があるかどうかを判断できます。  
  
## <a name="illustration-of-load-balancing"></a>負荷分散の図  
 次の図は、サーバー上の親パッケージを示します。 親パッケージには、SQL Server エージェント ジョブの実行タスクが複数含まれています。 親パッケージ内の各タスクは、リモート サーバー上の SQL Server エージェントを呼び出します。 これらのリモート サーバーには、そのサーバー上のパッケージを呼び出すステップを含む SQL Server エージェント ジョブがあります。  
  
 ![SSIS 負荷分散アーキテクチャの概要](../media/loadbalancingoverview.gif "SSIS 負荷分散アーキテクチャの概要")  
  
 このアーキテクチャで負荷分散に必要な手順は、新しい概念ではありません。 負荷分散は、既存の概念と一般的な SSIS オブジェクトを新しい方法で使用して実現されています。  
  
## <a name="execution-of-packages-on-a-remote-instance-by-using-sql-server-agent"></a>リモート インスタンスで SQL Server エージェントを使用したパッケージの実行  
 リモート パッケージの実行の基本的なアーキテクチャでは、中心となるパッケージは、他のリモート パッケージを制御する SQL Server のインスタンスに常駐します。 図では、SSIS Parent という名前の中心となるパッケージを示しています。 この親パッケージが常駐するインスタンスによって、子パッケージを実行する SQL Server エージェント ジョブの実行が制御されます。 子パッケージの実行は、リモート サーバーの SQL Server エージェントで制御される固定的なスケジュールに基づくわけではありません。 子パッケージは、親パッケージから呼び出されたときに SQL Server エージェントによって開始され、SQL Server エージェントが常駐している同じ SQL Server のインスタンスで実行されます。  
  
 SQL Server エージェントを使用してリモート パッケージを実行するには、あらかじめ親パッケージと子パッケージを構成し、子パッケージを制御する SQL Server エージェント ジョブをセットアップしておく必要があります。 次のセクションでは、リモート サーバーで実行するパッケージの作成、構成、実行、および管理方法について説明します。 このプロセスには、いくつかの手順があります。  
  
-   子パッケージを作成してリモート サーバーにインストールします。  
  
-   パッケージを実行するリモート インスタンスで SQL Server エージェント ジョブを作成します。  
  
-   親パッケージを作成します。  
  
-   子パッケージ用のログ記録シナリオを決定します。  
  
 次の表に、このプロセスを説明するトピックへのリンクを示します。  
  
|トピック|説明|  
|-----------|-----------------|  
|[子パッケージの実装](../implementation-of-child-packages.md)|パッケージのインストールおよびパッケージを実行する SQL Server エージェント ジョブの作成について説明します。|  
|[親パッケージの実装](../implementation-of-the-parent-package.md)|SQL Server エージェント ジョブの実行タスクを多数含む親パッケージの作成について説明します。 各タスクが子パッケージの 1 つを実行します。|  
|[リモート サーバー上の負荷分散パッケージのログ記録](../logging-for-load-balanced-packages-on-remote-servers.md)|リモート パッケージ用のログ記録シナリオについて説明します。|  
  
## <a name="related-tasks"></a>Related Tasks  
 [SQL Server エージェントを使用してパッケージのスケジュールを設定する](../schedule-a-package-by-using-sql-server-agent.md)  
  
  
