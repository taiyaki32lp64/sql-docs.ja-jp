---
title: ジョブ転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03913242246fcdaf11e9272e827cd8e06951a108
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829898"
---
# <a name="transfer-jobs-task"></a>ジョブ転送タスク
  ジョブ転送タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス間で 1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブを転送します。  
  
 ジョブ転送タスクは、すべてのジョブまたは指定したジョブのみを転送するように構成できます。 また、転送先で転送したジョブを有効にするかどうかも指定できます。  
  
 転送しようとするジョブが既に転送先に存在している場合もあります。 ジョブ転送タスクでは、既存のジョブの処理を次のように構成できます。  
  
-   既存のジョブを上書きします。  
  
-   重複するジョブが存在する場合、タスクを失敗させます。  
  
-   重複するジョブをスキップします。  
  
 実行時に、ジョブ転送タスクは 1 つまたは 2 つの SMO 接続マネージャーを使用して、転送元および転送先サーバーに接続します。 SMO 接続マネージャーはジョブ転送タスクとは別に構成され、ジョブ転送タスクで参照されます。 SMO 接続マネージャーは、サーバーと、このサーバーにアクセスするときに使用する認証モードを指定します。 詳細については、「 [SMO 接続マネージャー](../connection-manager/smo-connection-manager.md)」を参照してください。  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>SQL Server のインスタンス間でのジョブの転送  
 ジョブ転送タスクは、転送元または転送先として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をサポートします。 転送元または転送先として使用するバージョンに関する制限はありません。  
  
## <a name="events"></a>イベント  
 ジョブ転送タスクでは、転送されたジョブの数を報告する情報イベントと、ジョブが上書きされた場合の警告イベントが発生します。 ジョブの転送の進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 タスクの `ExecutionValue` プロパティで定義される実行値は、転送されたジョブの数を返します。 ジョブ転送タスクの `ExecValueVariable` プロパティにユーザー定義変数を割り当てると、パッケージの他のオブジェクトからジョブの転送に関する情報を使用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](../use-variables-in-packages.md)」をご覧ください。  
  
## <a name="log-entries"></a>ログ エントリ  
 ジョブ転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferJobsTaskStarTransferringObjects   転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferJobsTaskFinishedTransferringObjects    転送が終了したことを報告するログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、`OnInformation` イベントのログ エントリは転送されたジョブの数を報告し、`OnWarning` イベントのログ エントリは転送先でジョブが上書きされると書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 ジョブを転送するユーザーは、sysadmin 固定サーバー ロールのメンバー、または転送元および転送先の両方の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの msdb データベースで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント固定データベース ロールのメンバーである必要があります。  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>ジョブ転送タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[ジョブ転送タスク エディター] ([全般] ページ)](../general-page-of-integration-services-designers-options.md)  
  
-   [[ジョブ転送タスク エディター] ([ジョブ] ページ)](../transfer-jobs-task-editor-jobs-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
