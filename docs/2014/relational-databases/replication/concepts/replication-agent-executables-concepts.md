---
title: レプリケーション エージェント実行可能ファイルの概念 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 451b7ca4cc06269f116c62be2ef7f01f0e33abd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721892"
---
# <a name="replication-agent-executables-concepts"></a>レプリケーション エージェント実行可能ファイルの概念
  レプリケーション エージェントは、次のような方法でプログラムから制御できます。  
  
-   <xref:Microsoft.SqlServer.Replication> 名前空間のマネージド エージェント プログラミング インターフェイスを使用する。  
  
-   エージェントの実行可能ファイルを一連のパラメーターを指定してコマンド プロンプトから呼び出す。  
  
 レプリケーション エージェントはコマンド プロンプトから直接呼び出すことができるため、コマンド ライン スクリプトをバッチ ファイル化することで、プログラムからエージェントにアクセスできます。 エージェントをコマンド プロンプトから呼び出した場合、そのエージェントは、エージェントを呼び出したユーザーまたはバッチ ファイルを実行したユーザーの [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows セキュリティ アカウント下で実行されます。  
  
 次のレプリケーション エージェントのインスタンスは、実行可能ファイルを使用して実行できます。  
  
-   [レプリケーション ディストリビューション エージェント](../agents/replication-distribution-agent.md)  
  
-   [レプリケーション ログ リーダー エージェント](../agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../agents/replication-merge-agent.md)  
  
-   [レプリケーション キュー リーダー エージェント](../agents/replication-queue-reader-agent.md)  
  
-   [レプリケーション スナップショット エージェント](../agents/replication-snapshot-agent.md)  
  
 レプリケーション エージェントを呼び出す際、パフォーマンス プロファイルを使用することで、あらかじめ定義された一連のパラメーターを自動的にエージェント実行可能ファイルに渡すことができます。 詳しくは、「 [Replication Agent Profiles](../agents/replication-agent-profiles.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
 次の例は、レプリケーション エージェントをコマンド プロンプトから呼び出す方法を示しています。 レプリケーション エージェントは、レプリケーション管理オブジェクト (RMO) を使用して呼び出すこともできます。 詳細については、「[サブスクリプションの同期 &#40;レプリケーション&#41;](../synchronize-data.md)」を参照してください。  
  
> [!NOTE]  
>  これらの例では、読みやすくするために、改行が追加されています。 バッチ ファイルの場合、コマンドは 1 行で入力する必要があります。  
  
### <a name="running-the-snapshot-agent"></a>スナップショット エージェントの実行  
 次の例では、バッチ ファイルを使って、スナップショット エージェントをコマンド プロンプトから呼び出し、**AdvWorksSalesOrdersMerge** パブリケーションのスナップショットを生成しています。  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
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
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
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
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  
