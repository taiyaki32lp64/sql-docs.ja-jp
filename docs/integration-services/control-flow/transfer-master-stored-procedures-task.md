---
title: Master ストアド プロシージャ転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
- sql13.dts.designer.transferstoredprocedurestask.general.f1
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cee2dfed374c3f479e32b8d81602eff924287356
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293847"
---
# <a name="transfer-master-stored-procedures-task"></a>Master ストアド プロシージャ転送タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Master ストアド プロシージャ転送タスクは、 **のインスタンス上の** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース間で、1 つ以上のユーザー定義ストアド プロシージャを転送します。 **master** データベースからストアド プロシージャを転送するには、プロシージャの所有者が dbo である必要があります。  
  
 Master ストアド プロシージャ転送タスクは、すべてのストアド プロシージャまたは指定したストアド プロシージャのみを転送するように設定できます。 このタスクでは、システム ストアド プロシージャはコピーされません。  
  
 転送する master ストアド プロシージャが既に転送先に存在している場合もあります。 Master ストアド プロシージャ転送タスクでは、既存のストアド プロシージャの処理を次のように設定できます。  
  
-   既存のストアド プロシージャを上書きします。  
  
-   重複するストアド プロシージャが存在する場合、タスクを失敗とします。  
  
-   重複するストアド プロシージャをスキップします。  
  
 Master ストアド プロシージャ転送タスクは実行時に、2 つの SMO 接続マネージャーを使用して、転送元および転送先サーバーに接続します。 SMO 接続マネージャーの構成は Master ストアド プロシージャ転送タスクとは別に行い、Master ストアド プロシージャ転送タスクは SMO 接続マネージャーを参照します。 SMO 接続マネージャーは、サーバーと、サーバーに接続する際に使用する認証モードを指定します。 詳細については、「 [SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)」を参照してください。  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>SQL Server のインスタンス間でのストアド プロシージャの転送  
 Master ストアド プロシージャ転送タスクでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 転送元と転送先をサポートします。  
  
## <a name="events"></a>イベント  
 Master ストアド プロシージャ転送タスクでは、転送されたストアド プロシージャの数を報告する情報イベントと、ストアド プロシージャが上書きされた場合の警告イベントが発生します。  
  
 Master ストアド プロシージャ転送タスクでは、増分中のログイン転送タスクの進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 タスクの **ExecutionValue** プロパティで定義する実行値は、転送されたストアド プロシージャの数を返します。 Master ストアド プロシージャ転送タスクの **ExecValueVariable** プロパティにユーザー定義変数を割り当てると、パッケージの他のオブジェクトからストアド プロシージャの転送に関する情報を使用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」および「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」を参照してください。  
  
## <a name="log-entries"></a>ログ エントリ  
 Master ストアド プロシージャ転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferStoredProceduresTaskStartTransferringObjects  転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  転送が終了したことを報告するログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、 **OnInformation** イベントのログ エントリは転送されたストアド プロシージャの数を報告し、 **OnWarning** イベントのログ エントリは転送先でストアド プロシージャが上書きされると書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 ソースの **master** データベースでストアド プロシージャの一覧を表示する権限が必要です。また、転送先サーバーの sysadmin サーバー ロールのメンバーであるか、転送先サーバーの **master** データベースでストアド プロシージャを作成する権限を持つユーザーである必要があります。  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Master ストアド プロシージャ転送タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>プログラムによる Master ストアド プロシージャ転送タスクの構成  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-master-stored-procedures-task-editor-general-page"></a>[Master ストアド プロシージャ転送タスク エディター] ([全般] ページ)
  **[Master ストアド プロシージャ転送タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、Master ストアド プロシージャ転送タスクの名前と説明を入力できます。  
  
> [!NOTE]  
>  このタスクは、コピー元のサーバーの **master** データベースからコピー先のサーバーの **master** データベースに、 **dbo** が所有しているユーザー定義のストアド プロシージャのみを転送します。 コピー先のサーバーでストアド プロシージャを作成するには、そのサーバーの **master** データベースの CREATE PROCEDURE 権限を取得するか、そのサーバーの **sysadmin** 固定サーバー ロールのメンバーである必要があります。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 Master ストアド プロシージャ転送タスクの一意な名前を入力します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 Master ストアド プロシージャ転送タスクの説明を入力します。  
  
## <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>[Master ストアド プロシージャ転送タスク エディター] ([ストアド プロシージャ] ページ)
  **[Master ストアド プロシージャ転送タスク エディター]** ダイアログ ボックスの **[ストアド プロシージャ]** ページを使用すると、 **の 1 つのインスタンスの** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースから **の別のインスタンスの** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースに、1 つ以上のユーザー定義ストアド プロシージャをコピーする場合のプロパティを指定できます。  
  
> [!NOTE]  
>  このタスクは、コピー元のサーバーの **master** データベースからコピー先のサーバーの **master** データベースに、 **dbo** が所有しているユーザー定義のストアド プロシージャのみを転送します。 コピー先のサーバーでストアド プロシージャを作成するには、そのサーバーの **master** データベースの CREATE PROCEDURE 権限を取得するか、そのサーバーの **sysadmin** 固定サーバー ロールのメンバーである必要があります。  
  
### <a name="options"></a>オプション  
 **SourceConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー元のサーバーへの新しい接続を作成します。  
  
 **DestinationConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー先のサーバーへの新しい接続を作成します。  
  
 **[IfObjectExists]**  
 コピー先のサーバーの **master** データベースに存在する名前と同じ名前を持つ、ユーザー定義ストアド プロシージャの処理方法を選択します。  
  
 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[FailTask]**|ストアド プロシージャがコピー先のサーバーの **master** データベースに既に存在する名前と同じ名前を持つ場合、タスクは失敗します。|  
|**Overwrite**|コピー先のサーバーの **master** データベースにある同じ名前のストアド プロシージャを上書きします。|  
|**Skip**|コピー先のサーバーの **master** データベースにある同じ名前のストアド プロシージャをスキップします。|  
  
 **[TransferAllStoredProcedures]**  
 コピー元のサーバーの **master** データベースのすべてのユーザー定義ストアド プロシージャをコピー先のサーバーにコピーするかどうかを選択します。  
  
|[値]|Description|  
|-----------|-----------------|  
|**True**|**master** データベースのユーザー定義ストアド プロシージャをすべてコピーします。|  
|**False**|指定したストアド プロシージャのみをコピーします。|  
  
 **[StoredProceduresList]**  
 コピー先の **master** データベースにコピーする、コピー元サーバーの **master** データベースのユーザー定義ストアド プロシージャを選択します。 このオプションは、 **[TransferAllStoredProcedures]** を **[False]** に設定した場合のみ使用できます。  
  
## <a name="see-also"></a>参照  
 [SQL Server オブジェクトの転送タスク](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
