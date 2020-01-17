---
title: Master ストアド プロシージャ転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfermasterspstask.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b7cef1e64ab9c499c52ac3bbc0364a05bfcc812
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829483"
---
# <a name="transfer-master-stored-procedures-task"></a>Master ストアド プロシージャ転送タスク
  Master ストアド プロシージャ転送タスクは、 **のインスタンス上の** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース間で、1 つ以上のユーザー定義ストアド プロシージャを転送します。 **master** データベースからストアド プロシージャを転送するには、プロシージャの所有者が dbo である必要があります。  
  
 Master ストアド プロシージャ転送タスクは、すべてのストアド プロシージャまたは指定したストアド プロシージャのみを転送するように設定できます。 このタスクでは、システム ストアド プロシージャはコピーされません。  
  
 転送する master ストアド プロシージャが既に転送先に存在している場合もあります。 Master ストアド プロシージャ転送タスクでは、既存のストアド プロシージャの処理を次のように設定できます。  
  
-   既存のストアド プロシージャを上書きします。  
  
-   重複するストアド プロシージャが存在する場合、タスクを失敗とします。  
  
-   重複するストアド プロシージャをスキップします。  
  
 Master ストアド プロシージャ転送タスクは実行時に、2 つの SMO 接続マネージャーを使用して、転送元および転送先サーバーに接続します。 SMO 接続マネージャーの構成は Master ストアド プロシージャ転送タスクとは別に行い、Master ストアド プロシージャ転送タスクは SMO 接続マネージャーを参照します。 SMO 接続マネージャーは、サーバーと、サーバーに接続する際に使用する認証モードを指定します。 詳細については、「 [SMO 接続マネージャー](../connection-manager/smo-connection-manager.md)」を参照してください。  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>SQL Server のインスタンス間でのストアド プロシージャの転送  
 Master ストアド プロシージャ転送タスクでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 転送元と転送先をサポートします。  
  
## <a name="events"></a>イベント  
 Master ストアド プロシージャ転送タスクでは、転送されたストアド プロシージャの数を報告する情報イベントと、ストアド プロシージャが上書きされた場合の警告イベントが発生します。  
  
 Master ストアド プロシージャ転送タスクでは、増分中のログイン転送タスクの進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 タスクの `ExecutionValue` プロパティで定義する実行値は、転送されたストアド プロシージャの数を返します。 Master ストアド プロシージャ転送タスクの `ExecValueVariable` プロパティにユーザー定義変数を割り当てると、パッケージの他のオブジェクトからストアド プロシージャの転送に関する情報を使用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](../use-variables-in-packages.md)」をご覧ください。  
  
## <a name="log-entries"></a>ログ エントリ  
 Master ストアド プロシージャ転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferStoredProceduresTaskStartTransferringObjects  転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  転送が終了したことを報告するログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、`OnInformation` イベントのログ エントリは転送されたストアド プロシージャの数を報告し、`OnWarning` イベントのログ エントリは転送先でストアド プロシージャが上書きされると書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 ソースの **master** データベースでストアド プロシージャの一覧を表示する権限が必要です。また、転送先サーバーの sysadmin サーバー ロールのメンバーであるか、転送先サーバーの **master** データベースでストアド プロシージャを作成する権限を持つユーザーである必要があります。  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Master ストアド プロシージャ転送タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[Master ストアド プロシージャ転送タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[Master ストアド プロシージャ転送タスク エディター] &#40;[ストアド プロシージャ] ページ&#41;](../transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>プログラムによる Master ストアド プロシージャ転送タスクの構成  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server オブジェクトの転送タスク](transfer-sql-server-objects-task.md)   
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
