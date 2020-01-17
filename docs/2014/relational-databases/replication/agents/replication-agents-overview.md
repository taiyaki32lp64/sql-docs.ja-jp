---
title: レプリケーション エージェントの概要 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent
- agents [SQL Server replication]
- Queue Reader Agent, about Queue Reader Agent
- Queue Reader Agent
- Merge Agent, about Merge Agent
- Log Reader Agent, about Log Reader Agent
- replication [SQL Server], agents and profiles
- Log Reader Agent
- Distribution Agent, about Distribution Agent
- agents [SQL Server replication], about agents
- Merge Agent
- Snapshot Agent, about Snapshot Agent
- Snapshot Agent
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41775a529d34aa5ca457f92c9d26e327b74705ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721914"
---
# <a name="replication-agents-overview"></a>レプリケーション エージェントの概要
  レプリケーションでは、エージェントと呼ばれる多数のスタンドアロン プログラムを使用して、変更の監視やデータの配信に関連するタスクを実行します。 既定では、レプリケーション エージェントは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントでスケジュールされたジョブとして実行されるため、ジョブを実行するためには [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントが実行中であることが必要です。 レプリケーション エージェントはコマンド ラインから実行することも、レプリケーション管理オブジェクト (RMO) を使用するアプリケーションから実行することもできます。 レプリケーション エージェントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション モニターおよび [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]から管理できます。  
  
## <a name="sql-server-agent"></a>SQL Server エージェント  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントでは、レプリケーションで使用するエージェントをホストし、スケジュールを設定することによって、レプリケーション エージェントを簡単に実行できるようになっています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントは、レプリケーション以外の操作も管理および監視します。 詳細については、「 [Configure SQL Server Agent](../../../ssms/agent/sql-server-agent.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール時に、サービスがインストール中に自動開始されるように明示的に選択しない限り、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスは既定で無効になります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスを開始する方法の詳細については、「[SQL Server エージェント サービスの開始、停止、または一時停止](../../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)」を参照してください。  
  
## <a name="snapshot-agent"></a>スナップショット エージェント  
 スナップショット エージェントは、一般的にすべての種類のレプリケーションで使用されます。 スナップショット エージェントは、パブリッシュされたテーブルやその他のオブジェクトのスキーマと初期データ ファイルを作成し、スナップショット ファイルを格納して、同期に関する情報をディストリビューション データベースに記録します。 スナップショット エージェントはディストリビューター側で実行されます。 詳細については、「 [Replication Snapshot Agent](replication-snapshot-agent.md)」を参照してください。  
  
## <a name="log-reader-agent"></a>ログ リーダー エージェント (Log Reader Agent)  
 ログ リーダー エージェントは、トランザクション レプリケーションで使用されます。 レプリケーションとしてマークが付けられたトランザクションを、パブリッシャーのトランザクション ログから、ディストリビューション データベースに移動します。 トランザクション レプリケーションを使用してパブリッシュされた各データベースには、ディストリビューター上で実行され、パブリッシャーに接続する独自のログ リーダー エージェントがあります (ディストリビューターはパブリッシャーと同じコンピューター上に存在していてもかまいません)。 詳細については、「 [Replication Log Reader Agent](replication-log-reader-agent.md)」を参照してください。  
  
## <a name="distribution-agent"></a>ディストリビューション エージェント  
 ディストリビューション エージェントは、スナップショット レプリケーション、およびトランザクション レプリケーションで使用されます。 ディストリビューション エージェントは初期スナップショットをサブスクライバーに適用し、ディストリビューション データベースに保持されているトランザクションをサブスクライバーに移動します。 ディストリビューション エージェントは、プッシュ サブスクリプションの場合はディストリビューターで実行され、プル サブスクリプションの場合はサブスクライバーで実行されます。 詳細については、「 [Replication Distribution Agent](replication-distribution-agent.md)」を参照してください。  
  
## <a name="merge-agent"></a>[マージ エージェント]  
 マージ エージェントは、マージ レプリケーションで使用されます。 マージ エージェントは、初期スナップショットをサブスクライバーに適用し、データの増分変更を移動および調整します。 マージ サブスクリプションごとにマージ エージェントがあり、パブリッシャーとサブスクライバーの両方に接続し、両方を更新します。 マージ エージェントは、プッシュ サブスクリプションの場合はディストリビューターで実行され、プル サブスクリプションの場合はサブスクライバーで実行されます。 既定では、マージ エージェントはサブスクライバーからパブリッシャーに変更をアップロードし、パブリッシャーからサブスクライバーに変更をダウンロードします。 詳細については、「 [Replication Merge Agent](replication-merge-agent.md)」を参照してください。  
  
## <a name="queue-reader-agent"></a>キュー リーダー エージェント (Queue Reader Agent)  
 キュー リーダー エージェントは、キュー更新オプションによるトランザクション レプリケーションで使用されます。 このエージェントはディストリビューターで実行され、サブスクライバーで行われた変更をパブリッシャーに戻します。 ディストリビューション エージェントやマージ エージェントとは異なり、キュー リーダー エージェントは 1 つのインスタンスだけで、ディストリビューション データベースのすべてのパブリッシャーおよびパブリケーションに対応します。 キュー リーダー エージェントの詳細については、「 [Replication Queue Reader Agent](replication-queue-reader-agent.md)」を参照してください。 更新可能なサブスクリプションの詳細については、「 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)」を参照してください。  
  
## <a name="replication-maintenance-jobs"></a>レプリケーション メンテナンス ジョブ  
 レプリケーションには、定期的なメンテナンスや要求時メンテナンスを実行する多数のメンテナンス ジョブがあります。 詳細については、「[Replication Agent Administration](replication-agent-administration.md)」 (レプリケーション エージェントの管理) を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [レプリケーション メンテナンス ジョブの実行 &#40;SQL Server Management Studio&#41;](../administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)   
 [レプリケーション エージェントの管理](replication-agent-administration.md)  
  
  
