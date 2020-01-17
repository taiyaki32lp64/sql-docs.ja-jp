---
title: レプリケーション エージェント実行可能ファイルの概念 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: d2df5c3df512c60c38caeb2f2d0240a3cf2daa6e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768723"
---
# <a name="replication-agent-executables-concepts"></a>レプリケーション エージェント実行可能ファイルの概念
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  レプリケーション エージェントは、次のような方法でプログラムから制御できます。  
  
-   <xref:Microsoft.SqlServer.Replication> 名前空間のマネージド エージェント プログラミング インターフェイスを使用する。  
  
-   エージェントの実行可能ファイルを一連のパラメーターを指定してコマンド プロンプトから呼び出す。  
  
 レプリケーション エージェントはコマンド プロンプトから直接呼び出すことができるため、コマンド ライン スクリプトをバッチ ファイル化することで、プログラムからエージェントにアクセスできます。 エージェントをコマンド プロンプトから呼び出した場合、そのエージェントは、エージェントを呼び出したユーザーまたはバッチ ファイルを実行したユーザーの [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows セキュリティ アカウント下で実行されます。  
  
 次のレプリケーション エージェントのインスタンスは、実行可能ファイルを使用して実行できます。  
  
-   [レプリケーション ディストリビューション エージェント](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [レプリケーション ログ リーダー エージェント](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [レプリケーション キュー リーダー エージェント](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
-   [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
 レプリケーション エージェントを呼び出す際、パフォーマンス プロファイルを使用することで、あらかじめ定義された一連のパラメーターを自動的にエージェント実行可能ファイルに渡すことができます。 詳しくは、「 [レプリケーション エージェント プロファイル](../../../relational-databases/replication/agents/replication-agent-profiles.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
 次の例は、レプリケーション エージェントをコマンド プロンプトから呼び出す方法を示しています。 レプリケーション エージェントは、レプリケーション管理オブジェクト (RMO) を使用して呼び出すこともできます。 詳細については、「[サブスクリプションの同期 &#40;レプリケーション&#41;](../../../relational-databases/replication/synchronize-data.md)」を参照してください。  
  
> [!NOTE]  
>  これらの例では、読みやすくするために、改行が追加されています。 バッチ ファイルの場合、コマンドは 1 行で入力する必要があります。  
  
### <a name="running-the-snapshot-agent"></a>スナップショット エージェントの実行  
 次の例では、バッチ ファイルを使って、スナップショット エージェントをコマンド プロンプトから呼び出し、**AdvWorksSalesOrdersMerge** パブリケーションのスナップショットを生成しています。 (以下のスクリプトでは、[!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] ファイル (バージョン 130) へのパスを使用しています)。 スクリプトを調整し、使用しているバージョンの [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] のファイルを指すようにする必要があります。)  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\130\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>ディストリビューション エージェントの実行  
 この例では、バッチ ファイルを使って、ディストリビューション エージェントをコマンド プロンプトから呼び出し、**AdvWorksProductTran** パブリケーションからの変更を、プッシュ サブスクライバーに連続してレプリケートしています。  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>マージ エージェントの実行  
 この例では、バッチ ファイルを使って、マージ エージェントをコマンド プロンプトから呼び出し、**AdvWorksSalesOrdersMerge** パブリケーションにプル サブスクリプションを同期しています。  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  
