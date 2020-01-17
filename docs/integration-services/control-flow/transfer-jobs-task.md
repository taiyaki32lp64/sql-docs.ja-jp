---
title: ジョブ転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eb4812b48c9465659ca8c0739f0411a9e65660bf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293868"
---
# <a name="transfer-jobs-task"></a>ジョブ転送タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ジョブ転送タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス間で 1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブを転送します。  
  
 ジョブ転送タスクは、すべてのジョブまたは指定したジョブのみを転送するように構成できます。 また、転送先で転送したジョブを有効にするかどうかも指定できます。  
  
 転送しようとするジョブが既に転送先に存在している場合もあります。 ジョブ転送タスクでは、既存のジョブの処理を次のように構成できます。  
  
-   既存のジョブを上書きします。  
  
-   重複するジョブが存在する場合、タスクを失敗させます。  
  
-   重複するジョブをスキップします。  
  
 実行時に、ジョブ転送タスクは 1 つまたは 2 つの SMO 接続マネージャーを使用して、転送元および転送先サーバーに接続します。 SMO 接続マネージャーはジョブ転送タスクとは別に構成され、ジョブ転送タスクで参照されます。 SMO 接続マネージャーは、サーバーと、このサーバーにアクセスするときに使用する認証モードを指定します。 詳細については、「 [SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)」を参照してください。  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>SQL Server のインスタンス間でのジョブの転送  
 ジョブ転送タスクは、転送元または転送先として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をサポートします。 転送元または転送先として使用するバージョンに関する制限はありません。  
  
## <a name="events"></a>イベント  
 ジョブ転送タスクでは、転送されたジョブの数を報告する情報イベントと、ジョブが上書きされた場合の警告イベントが発生します。 ジョブの転送の進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 タスクの **ExecutionValue** プロパティで定義される実行値は、転送されたジョブの数を返します。 ジョブ転送タスクの **ExecValueVariable** プロパティにユーザー定義変数を割り当てると、パッケージの他のオブジェクトからジョブの転送に関する情報を使用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」をご覧ください。  
  
## <a name="log-entries"></a>ログ エントリ  
 ジョブ転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferJobsTaskStarTransferringObjects   転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferJobsTaskFinishedTransferringObjects    転送が終了したことを報告するログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、 **OnInformation** イベントのログ エントリは転送されたジョブの数を報告し、 **OnWarning** イベントのログ エントリは転送先でジョブが上書きされると書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 ジョブを転送するユーザーは、sysadmin 固定サーバー ロールのメンバー、または転送元および転送先の両方の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの msdb データベースで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント固定データベース ロールのメンバーである必要があります。  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>ジョブ転送タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>[ジョブ転送タスク エディター] ([全般] ページ)
  **[ジョブ転送タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、ジョブ転送タスクの名前と説明を入力できます。  
  
> [!NOTE]  
>  転送先サーバー上の **sysadmin** 固定サーバー ロールのメンバー、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールのうち 1 つのロールのメンバーだけが、転送先にジョブを正常に作成できます。 転送元サーバー上のジョブにアクセスするには、ユーザーは少なくとも転送元サーバー上で **SQLAgentUserRole** 固定データベース ロールのメンバーである必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールおよびその権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 ジョブ転送タスクの一意な名前を入力します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 ジョブ転送タスクの説明を入力します。  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>[ジョブ転送タスク エディター] ([ジョブ] ページ)
  **[ジョブ転送タスク エディター]** ダイアログ ボックスの **[ジョブ]** ページを使用すると、1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのインスタンスから別のインスタンスにコピーするためのプロパティを指定できます。  
  
> [!NOTE]  
>  コピー元サーバーのジョブにアクセスするには、少なくともサーバーの **SQLAgentUserRole** 固定データベース ロールのメンバーであることが必要です。 コピー先サーバーでジョブを正常に作成するには、 **sysadmin** 固定サーバー ロールのメンバーであるか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールの 1 つであることが必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールおよびその権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」をご覧ください。  
  
### <a name="options"></a>オプション  
 **SourceConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー元のサーバーへの新しい接続を作成します。  
  
 **DestinationConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー先のサーバーへの新しい接続を作成します。  
  
 **[TransferAllJobs]**  
 コピー元サーバーからコピー先サーバーにすべてコピーするか、指定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのみをコピーするかを選択します。  
  
 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|Description|  
|-----------|-----------------|  
|**True**|すべてのジョブをコピーします。|  
|**False**|指定のジョブのみをコピーします。|  
  
 **[JobsList]**  
 **[...]** ボタンをクリックして、コピーするジョブを選択します。 少なくとも 1 つのジョブを選択する必要があります。  
  
> [!NOTE]  
>  コピーするジョブを選択する前に **[SourceConnection]** を指定します。  
  
 **[JobsList]** オプションは、 **[TransferAllJobs]** が **[True]** に設定されている場合は使用できません。  
  
 **[IfObjectExists]**  
 コピー先サーバーに既に存在する名前と同じ名前のジョブをどのように処理するかを選択します。  
  
 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[FailTask]**|ジョブの名前がコピー先サーバーに既に存在する名前と同じである場合、タスクは失敗します。|  
|**Overwrite**|コピー先サーバーの同じ名前のジョブを上書きします。|  
|**Skip**|コピー先サーバーの同じ名前のジョブをスキップします。|  
  
 **[EnableJobsAtDestination]**  
 コピー先サーバーにコピーされたジョブを有効にするかどうかを選択します。  
  
 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|Description|  
|-----------|-----------------|  
|**True**|コピー先サーバーのジョブを有効にします。|  
|**False**|コピー先サーバーのジョブを無効にします。|  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
