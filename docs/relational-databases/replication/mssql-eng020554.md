---
title: MSSQL_ENG020554 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020554 error
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7a9ad1938f94c090bd0f7e3746d565d2f0fce25d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770461"
---
# <a name="mssqleng020554"></a>MSSQL_ENG020554
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|20554|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|レプリケーション エージェントでは、進捗状況メッセージが %ld 分間ログに記録されていません。 この現象は、エージェントの応答が止まったか、システムの使用率が高いことを示している場合があります。 レコードがレプリケーション先にレプリケートされていること、およびサブスクライバー、パブリッシャー、ディストリビューターへの接続がアクティブなままであることを確認してください。|  
  
## <a name="explanation"></a>説明  
 **レプリケーション エージェントの検査** ジョブは、指定された間隔 (既定では 10 分) で実行され、各レプリケーション エージェントの状態を確認します。 エージェントが、最後の検査ジョブを実行してからまったく進捗状況メッセージを記録していない場合は、MSSQL_ENG020554 エラーが発生する可能性があります。 他のレプリケーション処理が実行されていない場合でも、エージェントは少なくとも履歴メッセージだけは記録する必要があります。 レプリケーション エージェントは、予想どおり応答していない場合でも、停止したり障害が発生するとは限りません (エージェントで障害が発生すると、エラー MSSQL_ENG020536 が発生します)。  
  
 MSSQL_ENG020554 は、次のような問題が原因で発生する可能性があります。  
  
-   エージェントがビジーである場合  
  
     エージェントの検査ジョブでポーリングが実行されているときにエージェントがビジーで応答できない場合、エージェントの検査ジョブは、レプリケーション エージェントが正しく機能しているかどうかについて報告できません。 レプリケーション エージェントがビジーになるのは、レプリケートされているデータの量が多すぎたり、アプリケーションの設計または構成の問題が原因でプロセスが長時間実行されるなど、さまざまな原因があります。  
  
-   エージェントがトポロジ内のコンピューターのいずれにもログインできない場合  
  
     すべてのエージェントには **-LoginTimeOut** パラメーター (既定では 15 秒に設定) が指定されています。このパラメーターによって、エージェントがレプリケーション ノードにログインする (マージ エージェントがパブリッシャーにログインするなど) 時間が決まります。 **-LoginTimeOut** の値を、レプリケーション エージェントの検査ジョブを実行する間隔よりも高く設定すると、ログインの問題がエラーの根本原因になる場合があります。エージェントで他の具体的なエラーが発生する前にエラー MSSQL_ENG020554 が発生します。  
  
## <a name="user-action"></a>ユーザーの操作  
 必要な操作は、エラーが発生した原因によって異なります。  
  
-   このエラーが発生するすべてのケースで、次のアクションを実行します。  
  
     レプリケーション モニターでエラーの詳細を確認してから、エージェントが停止している場合は再起動します。 エラーの詳細には、エージェントが正しく実行されなかった原因について追加の情報が示されている場合があります。 エージェントが実行中の場合は、エージェントを停止および再起動しないでください。停止および再起動すると、問題がさらに悪化する可能性があります。 レプリケーション モニターでのエージェントの状態やエラーの詳細の表示について詳しくは、[レプリケーション モニターを使用した情報の表示とタスクの実行](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)に関するページを参照してください。    
  
-   エージェントがビジーであるためにこのエラーが頻繁に発生する場合は、次の操作を実行します。  
  
     場合によっては、エージェントの処理時間が短くなるように、アプリケーションを再設計する必要があります。  
  
     **[ジョブのプロパティ]** ダイアログ ボックスを使用してエージェントの状態を確認する間隔を長くすることができます。 レプリケーション ジョブの場合のこのダイアログ ボックスへのアクセスの詳細については、[レプリケーション モニターを使用した情報の表示とタスクの実行](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)に関するページを参照してください。  
  
-   エージェントがトポロジ内のコンピューターのいずれにもログインできない場合には、次の操作を実行します。  
  
     **-LoginTimeOut** の値を、レプリケーション エージェントの検査ジョブを実行する間隔よりも低い値に設定することをお勧めします。 ネットワークの問題により、 **-LoginTimeOut** が高く設定され、その結果ログインがタイムアウトになる場合があります。 **-LoginTimeOut** の値を低く設定すると、レプリケーションから他の具体的なエラーが報告されるので、ログインの問題の原因 (権限、ネットワーク障害、その他の問題など) を特定してトラブルシューティングできます。 エージェント パラメーターは、エージェント プロファイルおよびコマンド ラインで指定できます。 詳細については、以下をご覧ください。  
  
    -   [レプリケーション エージェント プロファイルの操作](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)に割り当てるメモリの最大容量と最小容量を設定する。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [レプリケーション ディストリビューション エージェント](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [レプリケーション ログ リーダー エージェント](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [レプリケーション マージ エージェント](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [レプリケーション キュー リーダー エージェント](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [レプリケーション スナップショット エージェント](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
