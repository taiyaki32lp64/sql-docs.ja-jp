---
title: SQL Server エージェント | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, about SQL Server Agent
- automatic administration steps
ms.assetid: 8d1dc600-aabb-416f-b3af-fbc9fccfd0ec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f434c5d323f2203965fd0584dbc1dbc8bd89563
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68188828"
---
# <a name="sql-server-agent"></a>SQL Server エージェント
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、 *の* ジョブ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]と呼ばれる管理タスクをスケジュールに従って実行する Microsoft Windows サービスです。  
  
 **このトピックの内容**  
  
-   [SQL Server エージェントの利点](#Benefits)  
  
-   [SQL Server エージェントのコンポーネント](#Components)  
  
-   [SQL Server エージェントのセキュリティ管理](#Security)  
  
##  <a name="Benefits"></a> SQL Server エージェントの利点  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用してジョブ情報を格納します。 ジョブには 1 つ以上のジョブ ステップが含まれます。 各ジョブ ステップには、データベースをバックアップするなど、独自のタスクがあります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでは、スケジュールに従って、特定のイベントに応答して、または必要に応じてジョブを実行できます。 たとえば、毎平日の業務終了後に会社のすべてのサーバーをバックアップする必要がある場合は、そのタスクを自動化できます。 月曜から金曜までの 22:00 以降にバックアップを実行するスケジュールを設定します。バックアップに問題が発生した場合、イベントが記録され、通知を受け取ることができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされるときに、サービスを自動起動することをユーザーが明示的に選択しない限り、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] エージェント サービスは既定で無効になります。  
  
##  <a name="Components"></a> SQL Server エージェント コンポーネント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでは、次のコンポーネントを使用して、実行するタスク、タスクを実行する時期、タスクの成功/失敗の報告方法を定義します。  
  
### <a name="jobs"></a>ジョブ  
 *ジョブ* とは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで実行される特定の一連の処理のことです。 ジョブを使用して一度管理タスクを定義すると、そのタスクを何度も実行したり、それが正常に終了したかどうかを監視できます。 ジョブは 1 つのローカル サーバーで実行することも、複数のリモート サーバーで実行することもできます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインスタンスでフェールオーバー イベントが発生したときに実行されていた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは、別のフェールオーバー クラスター ノードにフェールオーバーしても再開されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブが Hyper-V ノードの一時停止時に実行されていた場合、一時停止によって別のノードにフェールオーバーしても再開されません。 ジョブの開始後、フェールオーバー イベントが原因でそのジョブが完了しなかった場合は、開始したことがログに記録されますが、完了か失敗かを示すログ エントリは追加されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは終了していないように見えます。  
  
 ジョブは、次のような方法で実行できます。  
  
-   1 つ以上のスケジュールに従って実行する。  
  
-   1 つ以上の警告に応答して実行する。  
  
-   sp_start_job ストアド プロシージャの実行によって実行する。  
  
 ジョブ内の各処理を *ジョブ ステップ*といいます。 たとえば、ジョブ ステップは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージの実行、Analysis Services サーバーへのコマンドの発行などで構成されます。 ジョブ ステップはジョブの一部として管理されます。  
  
 各ジョブ ステップは、特定のセキュリティ コンテキストで実行されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用するジョブ ステップでは、EXECUTE AS ステートメントを使用して、ジョブ ステップにセキュリティ コンテキストを設定します。 その他のジョブ ステップでは、プロキシ アカウントを使用して、ジョブ ステップにセキュリティ コンテキストを設定します。  
  
### <a name="schedules"></a>スケジュール  
 *スケジュール* では、ジョブを実行する時期を指定します。 複数のジョブを同じスケジュールで実行したり、1 つのジョブに複数のスケジュールを割り当てることができます。 スケジュールでは、ジョブを実行する時期について次の条件を定義できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが開始されるたびに、ジョブを実行する。  
  
-   コンピューターの CPU 使用率がアイドルとして定義したレベルになったときに、ジョブを実行する。  
  
-   指定した日時に 1 回だけジョブを実行する。  
  
-   スケジュールに従って定期的にジョブを実行する。  
  
 詳細については、「 [スケジュールの作成とジョブへのアタッチ](create-and-attach-schedules-to-jobs.md)」を参照してください。  
  
### <a name="alerts"></a>警告  
 *警告* とは、特定のイベントに対する自動応答のことです。 たとえば、ジョブが開始されたり、システム リソースが特定のしきい値に達したときなどがイベントと見なされます。 警告では、それが発生する条件を定義します。  
  
 警告は、次のいずれかの条件に対して生成できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベント  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス状態  
  
-   SQL Server エージェントが実行されているコンピューターで発生した Microsoft Windows Management Instrumentation (WMI) イベント  
  
 警告では、次のアクションを実行できます。  
  
-   1 人または複数のオペレーターへの通知  
  
-   ジョブの実行  
  
 詳細については、「 [警告](alerts.md)」を参照してください。  
  
### <a name="operators"></a>オペレーター  
 *オペレーター* は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の 1 つの以上のインスタンスについて、そのメンテナンスを担当する管理責任者の連絡先情報を定義します。 一部の企業では、オペレーターの責任は 1 人に割り当てられます。 サーバーを複数台使用している企業では、多数の担当者がオペレーターの責任を共有します。 オペレーターにはセキュリティ情報を指定せず、セキュリティ プリンシパルを定義しません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からオペレーターに警告を通知できます。  
  
-   電子メール  
  
-   電子メール経由のポケットベル  
  
-   **net send**  
  
> [!NOTE]  
>  **net send**を使用して通知を送信するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが置かれているコンピューターで Windows Messenger サービスを開始する必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のバージョンでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントからポケットベル オプションと **net send** オプションが削除される予定です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  
  
 電子メールまたはポケットベルを使用してオペレーターに通知を送信するには、データベース メールを使用するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを構成する必要があります。 詳細については、「 [Database Mail](../../relational-databases/database-mail/database-mail.md)」を参照してください。  
  
 オペレーターは、個人のグループを表す別名として定義できます。 その場合、その別名のすべてのメンバーが同時に通知を受け取ることになります。 詳細については、「 [オペレーター](operators.md)」を参照してください。  
  
##  <a name="Security"></a> SQL Server エージェントの管理のセキュリティ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して、 **SQLAgentUserRole**、 **SQLAgentReaderRole**、および**SQLAgentOperatorRole**固定データベース ロールで、 **msdb**データベースへのアクセスを制御する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メンバーではないユーザー エージェントの`sysadmin`固定サーバー ロール。 これらの固定データベース ロールに加え、サブシステムとプロキシを使用することで、タスクの実行に最低限必要な権限で各ジョブ ステップを実行できるようになります。  
  
### <a name="roles"></a>ロール  
 メンバー、 **SQLAgentUserRole**、 **SQLAgentReaderRole**、および**SQLAgentOperatorRole**固定データベース ロールで**msdb**とメンバー、`sysadmin`固定サーバー ロールへのアクセスがある[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント。 どのロールのメンバーでもないユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって使用されるロールの詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」を参照してください。  
  
### <a name="subsystems"></a>サブシステム  
 サブシステムは事前に定義されたオブジェクトで、任意のジョブ ステップで使用できる機能を表します。 各プロキシは 1 つ以上のサブシステムにアクセスできます。 サブシステムはプロキシで使用できる機能へのアクセスを制限することによりセキュリティを提供します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップ以外の各ジョブ ステップは、プロキシのコンテキストで実行されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップでは、EXECUTE AS コマンドを使用してセキュリティ コンテキストが設定されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次の表に示すサブシステムを定義しています。  
  
|サブシステム名|説明|  
|--------------------|-----------------|  
|Microsoft ActiveX スクリプト|ActiveX スクリプティング ジョブ ステップを実行します。<br /><br /> **\*\* 重要な \*\*** ActiveX スクリプティング サブシステムはから削除する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の将来のバージョンのエージェント[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。|  
|オペレーティング システム (**CmdExec**)|実行可能なプログラムを実行します。|  
|PowerShell|PowerShell スクリプティング ジョブ ステップを実行します。|  
|レプリケーション ディストリビューター|レプリケーション ディストリビューション エージェントをアクティブにするジョブ ステップを実行します。|  
|レプリケーション マージ|レプリケーション マージ エージェントをアクティブにするジョブ ステップを実行します。|  
|レプリケーション キュー リーダー|レプリケーション キュー リーダー エージェントをアクティブにするジョブ ステップを実行します。|  
|レプリケーション スナップショット|レプリケーション スナップショット エージェントをアクティブにするジョブ ステップを実行します。|  
|レプリケーション トランザクション ログ リーダー|レプリケーション ログ リーダー エージェントをアクティブにするジョブ ステップを実行します。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コマンド|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コマンドを実行します。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Query|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] クエリを実行します。|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ実行|[!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージを実行します。|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップではプロキシを使用しないので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ジョブ ステップ用の [!INCLUDE[tsql](../../includes/tsql-md.md)] エージェント サブシステムはありません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサブシステム制約が強制的に適用されます。 たとえば、sysadmin 固定サーバー ロールのメンバーであるユーザーのプロキシが [!INCLUDE[ssIS](../../includes/ssis-md.md)] サブシステムにアクセスできなければ、そのユーザーが [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージを実行できる場合でも、そのプロキシは [!INCLUDE[ssIS](../../includes/ssis-md.md)] ジョブ ステップを実行できません。  
  
### <a name="proxies"></a>プロキシ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、プロキシを使用してセキュリティ コンテキストを管理します。 プロキシは、複数のジョブ ステップで使用できます。 メンバー、`sysadmin`固定サーバー ロールは、プロキシを作成できます。  
  
 各プロキシには対応するセキュリティ資格情報が 1 つあります。 各プロキシは、一連のサブシステムや一連のログインに関連付けることができます。 プロキシは、そのプロキシに関連付けられているサブシステムを使用するジョブ ステップにのみ使用できます。 特定のプロキシを使用するジョブ ステップを作成するには、ジョブの所有者がそのプロキシに関連付けられているログインを使用しているか、プロキシへ制限なしにアクセスできるロールのメンバーである必要があります。 メンバー、`sysadmin`プロキシに無制限のアクセスに固定サーバー ロール。 **SQLAgentUserRole**、 **SQLAgentReaderRole**、または **SQLAgentOperatorRole** のメンバーは、特定のアクセスが許可されているプロキシしか使用できません。 これらの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの固定データベース ロールのメンバーであるユーザーが特定のプロキシを使用するジョブ ステップを作成するには、ユーザーごとにこれらの特定のプロキシへのアクセスが許可されている必要があります。  
  
## <a name="related-tasks"></a>関連タスク  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理を自動化するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを構成するには、次の手順に従ってください。  
  
1.  定期的に発生する管理タスクまたはサーバー イベントを確定し、それらをプログラムによって管理できるかどうかも確定します。 手順の順序が予測可能で、特定の時刻または特定のイベントに対する応答として行われるタスクは、自動化に適しています。  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) を使用して、ジョブ、スケジュール、警告、およびオペレーターから構成されるセットを定義します。 詳細については、「 [ジョブの作成](create-jobs.md)」を参照してください。  
  
3.  定義した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既定のインスタンスの場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの名前は SQLSERVERAGENT です。 名前付きインスタンスの場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの名前は SQLAgent$*instancename*です。  
  
 複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを実行している場合、すべてのインスタンスに共通なタスクをマルチサーバー管理を使用して自動化できます。 詳細については、「 [エンタープライズ全体の管理の自動化](automated-administration-across-an-enterprise.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントに関連したタスクを次に示します。  
  
|||  
|-|-|  
|**[説明]**|**トピック**|  
|SQL Server エージェントを構成する方法について説明します。|[SQL Server エージェントの構成](configure-sql-server-agent.md)|  
|SQL Server エージェント サービスを開始、停止、および一時停止する方法について説明します。|[SQL Server エージェント サービスの開始、停止、または一時停止](start-stop-or-pause-the-sql-server-agent-service.md)|  
|SQL Server エージェント サービスのアカウントを指定する際の考慮事項について説明します。|[SQL Server エージェント サービスのアカウントの選択](select-an-account-for-the-sql-server-agent-service.md)|  
|SQL Server エージェントのエラー ログを使用する方法について説明します。|[SQL Server エージェント エラー ログ](sql-server-agent-error-log.md)|  
|||  
|パフォーマンス オブジェクトを使用する方法について説明します。|[パフォーマンス オブジェクトの使用](use-performance-objects.md)|  
|メンテナンス プラン ウィザードについて説明します。メンテナンス プラン ウィザードは、SQL Server のインスタンスを自動管理するために、ジョブ、警告、およびオペレーターを作成するのに役立つユーティリティです。|[メンテナンス プラン ウィザードの使用](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|SQL Server エージェントを使用して管理タスクを自動化する方法について説明します。|[管理タスクの自動化 &#40;SQL Server エージェント&#41;](automated-administration-tasks-sql-server-agent.md)|  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)  
  
  
