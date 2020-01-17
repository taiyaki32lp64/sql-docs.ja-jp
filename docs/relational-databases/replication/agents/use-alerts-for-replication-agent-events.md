---
title: レプリケーション エージェント イベントに対する警告の使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing alerts
- Queue Reader Agent, alerts
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
- Log Reader Agent, alerts
- Distribution Agent, alerts
- Merge Agent, alerts
- agents [SQL Server replication], alerts
- displaying alerts
- Snapshot Agent, alerts
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: f0aa79ac22011a480ae60fe3002e0ac5bf896525
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768236"
---
# <a name="use-alerts-for-replication-agent-events"></a>レプリケーション エージェント イベントに対する警告の使用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] および [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントでは、レプリケーション エージェント イベントなどのイベントを、警告を使用して監視する方法が用意されています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントでは、警告に関連するイベントに対し、Windows アプリケーション ログを監視します。 このようなイベントが発生すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントは、定義されたタスクを実行したり、電子メールまたはポケットベルのメッセージを指定したオペレーターに送信することにより、自動的に応答します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、タスクを実行したりオペレーターに通知するように設定できる、レプリケーション エージェントに対する一連の定義済みの警告が含まれます。 実行するタスクの定義の詳細については、このトピックの「警告への応答の自動化」を参照してください。  
  
 次の警告は、コンピューターをディストリビューターとして構成したときにインストールされます。  
  
|メッセージ ID|定義済みの警告|警告を表示する原因となった条件|msdb..sysreplicationalerts への追加情報の入力|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**レプリケーション: エージェントが成功しました**|エージェントが正常にシャットダウンされました。|はい|  
|14151|**レプリケーション: エージェントが失敗しました**|エージェントがエラーでシャットダウンされました。|はい|  
|14152|**レプリケーション: エージェントを再試行します**|操作の再試行が成功せず、エージェントはシャットダウンされました (エージェントが、サーバーの利用不能、デッドロック、接続の失敗、タイムアウト障害などのエラーを検出しました)。|はい|  
|14157|**レプリケーション: 有効期限の切れたサブスクリプションを削除しました**|有効期限の切れたサブスクリプションが削除されました。|いいえ|  
|20572|**レプリケーション:データ検証で問題が見つかった後、サブスクリプションが再初期化されました**|応答ジョブ "データ検証で問題が見つかったサブスクリプションの再初期化" でサブスクリプションが正常に再初期化されました。|いいえ|  
|20574|**レプリケーション:サブスクライバーでデータ検証の問題が見つかりました**|ディストリビューション エージェントまたはマージ エージェントはデータの検証で問題が見つかりました。|はい|  
|20575|**レプリケーション:サブスクライバーでデータ検証を正常に終了しました**|ディストリビューション エージェントまたはマージ エージェントはデータの検証を正常に終了しました。|はい|  
|20578|**レプリケーション: エージェントのカスタム シャットダウン**|||  
|22815|**ピア ツー ピア競合検出の警告**|ピア ツー ピア ノードで変更を適用しようとしたときにディストリビューション エージェントで競合が検出されました。|はい|  
  
 これらの警告に加え、レプリケーション モニターでは、ステータスおよびパフォーマンスに関連する一連の警告を使用できます。 詳細については、「 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 警告システムを使用して、他のレプリケーション イベントの警告を定義することもできます。 詳細については、「[ユーザー定義イベントの作成](https://msdn.microsoft.com/library/03d71a35-97fa-4bba-aa9a-23ac9c9cf879)」を参照してください。  
  
 **定義済みのレプリケーションの警告を構成するには**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [定義済みのレプリケーションの警告の構成 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## <a name="viewing-the-application-log-directly"></a>アプリケーション ログの直接表示  
 Windows アプリケーション ログを表示するには、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows イベント ビューアーを使用します。 アプリケーション ログには [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエラー メッセージだけでなく、コンピューターのその他多くの利用状況に関するメッセージが含まれます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エラー ログとは異なり、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を起動するたびに新しいアプリケーション ログが作成されることはありません (各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セッションでは、既存のアプリケーション ログに新しいイベントを書き込みます)。ただし、ログに記録されたイベントを保有する期間を指定できます。 Windows アプリケーション ログを表示するときに、特定のイベントのログをフィルター選択できます。 詳細については、Windows のマニュアルを参照してください。  
  
## <a name="automating-a-response-to-an-alert"></a>警告への応答の自動化  
 レプリケーションでは、データ検証に失敗するサブスクリプションに対する応答ジョブ、および自動化された警告への応答を追加作成するためのフレームワークが用意されています。 応答ジョブは、" **データ検証で問題が見つかったサブスクリプションの再初期化** " というタイトルが付けられ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にある **エージェントの** [ジョブ] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]フォルダーに保存されます。 この応答ジョブを有効にする方法については、「[Configure Predefined Replication Alerts &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)」 (定義済みのレプリケーションの警告の構成 &#40;SQL Server Management Studio&#41;) を参照してください。 トランザクション パブリケーション内のアーティクルが検証に失敗すると、応答ジョブは、その失敗したアーティクルのみを再初期化します。 マージ パブリケーション内のアーティクルが検証に失敗すると、応答ジョブは、パブリケーション内のすべてのアーティクルを再初期化します。  
  
### <a name="framework-for-automating-responses"></a>応答の自動化のためのフレームワーク  
 通常では、警告が表示された場合、警告の原因と実行する適切な操作を知るのに役立つ唯一の情報は、警告自体に含まれています。 この情報の解析は間違いやすく、時間がかかります。 レプリケーションでは、 **sysreplicationalerts** システム テーブルで警告についての追加情報が提供され、応答の自動化を容易にしています。提供される情報は、既に解析済みで、カスタマイズしたプログラムで簡単に使用できます。  
  
 たとえば、サブスクライバー A の **Sales.SalesOrderHeader** テーブルのデータが検証に失敗した場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、その失敗を通知するメッセージ 20574 を表示します。 受信するメッセージは、"パブリケーション 'MyPublication' のアーティクル 'SalesOrderHeader' に対するサブスクライバー 'A' のサブスクリプションで、データ検証に失敗しました" という内容になります。  
  
 このメッセージに基づいた応答を作成する場合は、サブスクライバー名、アーティクル名、パブリケーション名、およびエラーをメッセージから手動で解析する必要があります。 しかし、ディストリビューション エージェントおよびマージ エージェントは **sysreplicationalerts** にそれらの情報 (およびエージェントの種類、警告の時刻、パブリケーション データベース、サブスクライバー データベース、パブリケーションの種類などの詳細) を書き込みます。このため、応答ジョブではテーブルから関連情報を直接クエリできます。 正確な行を警告の特定のインスタンスへ関連付けることはできませんが、このテーブルにある **status** 列を使用して、対象となるエントリを追跡できます。 このテーブルのエントリは、履歴の保有期間の間、維持されます。  
  
 たとえば、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] で警告メッセージ 20574 を対象とする応答を作成する場合、次のロジックを使用します。  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [監視 &#40;レプリケーション&#41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
