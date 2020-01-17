---
title: レプリケーション エージェントの概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 050197c7ce5a6098397b6ad3db13a933983270d6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770740"
---
# <a name="replication-agents-overview"></a>レプリケーション エージェントの概要
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーションでは、エージェントと呼ばれる多数のスタンドアロン プログラムを使用して、変更の監視やデータの配信に関連するタスクを実行します。 既定では、レプリケーション エージェントは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントでスケジュールされたジョブとして実行されるため、ジョブを実行するためには [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントが実行中であることが必要です。 レプリケーション エージェントはコマンド ラインから実行することも、レプリケーション管理オブジェクト (RMO) を使用するアプリケーションから実行することもできます。 レプリケーション エージェントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション モニターおよび [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]から管理できます。  
  
## <a name="sql-server-agent"></a>SQL Server エージェント  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントでは、レプリケーションで使用するエージェントをホストし、スケジュールを設定することによって、レプリケーション エージェントを簡単に実行できるようになっています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントは、レプリケーション以外の操作も管理および監視します。 詳細については、「 [Configure SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール時に、サービスがインストール中に自動開始されるように明示的に選択しない限り、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスは既定で無効になります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスを開始する方法の詳細については、「[SQL Server エージェント サービスの開始、停止、または一時停止](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)」を参照してください。  
  
## <a name="snapshot-agent"></a>スナップショット エージェント  
 スナップショット エージェントは、一般的にすべての種類のレプリケーションで使用されます。 スナップショット エージェントは、パブリッシュされたテーブルやその他のオブジェクトのスキーマと初期データ ファイルを作成し、スナップショット ファイルを格納して、同期に関する情報をディストリビューション データベースに記録します。 スナップショット エージェントはディストリビューター側で実行されます。 詳細については、「 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)」を参照してください。  
  
## <a name="log-reader-agent"></a>ログ リーダー エージェント (Log Reader Agent)  
 ログ リーダー エージェントは、トランザクション レプリケーションで使用されます。 レプリケーションとしてマークが付けられたトランザクションを、パブリッシャーのトランザクション ログから、ディストリビューション データベースに移動します。 トランザクション レプリケーションを使用してパブリッシュされた各データベースには、ディストリビューター上で実行され、パブリッシャーに接続する独自のログ リーダー エージェントがあります (ディストリビューターはパブリッシャーと同じコンピューター上に存在していてもかまいません)。 詳細については、「 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)」を参照してください。  
  
## <a name="distribution-agent"></a>ディストリビューション エージェント  
 ディストリビューション エージェントは、スナップショット レプリケーション、およびトランザクション レプリケーションで使用されます。 ディストリビューション エージェントは初期スナップショットをサブスクライバーに適用し、ディストリビューション データベースに保持されているトランザクションをサブスクライバーに移動します。 ディストリビューション エージェントは、プッシュ サブスクリプションの場合はディストリビューターで実行され、プル サブスクリプションの場合はサブスクライバーで実行されます。 詳細については、「 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)」を参照してください。  
  
## <a name="merge-agent"></a>[マージ エージェント]  
 マージ エージェントは、マージ レプリケーションで使用されます。 マージ エージェントは、初期スナップショットをサブスクライバーに適用し、データの増分変更を移動および調整します。 マージ サブスクリプションごとにマージ エージェントがあり、パブリッシャーとサブスクライバーの両方に接続し、両方を更新します。 マージ エージェントは、プッシュ サブスクリプションの場合はディストリビューターで実行され、プル サブスクリプションの場合はサブスクライバーで実行されます。 既定では、マージ エージェントはサブスクライバーからパブリッシャーに変更をアップロードし、パブリッシャーからサブスクライバーに変更をダウンロードします。 詳細については、「 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)」を参照してください。  
  
## <a name="queue-reader-agent"></a>キュー リーダー エージェント (Queue Reader Agent)  
 キュー リーダー エージェントは、キュー更新オプションによるトランザクション レプリケーションで使用されます。 このエージェントはディストリビューターで実行され、サブスクライバーで行われた変更をパブリッシャーに戻します。 ディストリビューション エージェントやマージ エージェントとは異なり、キュー リーダー エージェントは 1 つのインスタンスだけで、ディストリビューション データベースのすべてのパブリッシャーおよびパブリケーションに対応します。 キュー リーダー エージェントの詳細については、「 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)」を参照してください。 更新可能なサブスクリプションの詳細については、「 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)」を参照してください。  
  
## <a name="replication-maintenance-jobs"></a>レプリケーション メンテナンス ジョブ  
 レプリケーションには、定期的なメンテナンスや要求時メンテナンスを実行する多数のメンテナンス ジョブがあります。 詳細については、「[Replication Agent Administration](../../../relational-databases/replication/agents/replication-agent-administration.md)」 (レプリケーション エージェントの管理) を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [レプリケーション メンテナンス ジョブの実行 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [レプリケーション エージェント実行可能ファイルの概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [レプリケーション エージェントの管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
