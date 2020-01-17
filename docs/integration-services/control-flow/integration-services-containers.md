---
title: Integration Services コンテナー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS containers
- containers [Integration Services]
- containers [Integration Services], about containers
- control flow [Integration Services], containers
- SQL Server Integration Services containers
ms.assetid: 1b725922-ec59-4a47-9d55-e079463058f3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b05b7ffa40bb5b44c9dd3a5fa0d320cfadba0a43
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294059"
---
# <a name="integration-services-containers"></a>Integration Services コンテナー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  コンテナーとは、パッケージに構造を提供し、タスクにサービスを提供する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクトのことです。 コンテナーは、パッケージ内の制御フローの反復をサポートし、タスクおよびコンテナーを意味のある作業単位にグループ化します。 コンテナーには、タスクの他に別のコンテナーを含めることができます。  
  
 パッケージには、次の目的でコンテナーが使用されます。  
  
-   フォルダー内のファイル、スキーマ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) オブジェクトなど、コレクション内の各要素に対してタスクを繰り返します。 たとえば、複数ファイル内に含まれる Transact-SQL ステートメントをパッケージで実行できます。  
  
-   指定された式が **false**に評価されるまで、タスクを繰り返します。 たとえば、パッケージは各種電子メール メッセージを各曜日に 1 回、週に合計 7 回送信できます。  
  
-   ある単位として処理の成否を評価する必要のあるタスクおよびコンテナーをグループ化します。 たとえば、パッケージはデータベース テーブルの行を削除および追加するタスクをグループ化し、1 つのタスクが失敗したときにタスク全体をコミットまたはロールバックできます。  
  
## <a name="container-types"></a>コンテナーの種類  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、パッケージを構築するために 4 種類のコンテナーが用意されています。 次の表に、使用できるコンテナーの種類の一覧を示します。  
  
|コンテナー|[説明]|  
|---------------|-----------------|  
|[Foreach ループ コンテナー](../../integration-services/control-flow/foreach-loop-container.md)|列挙子を使用して、制御フローを繰り返し実行します。|  
|[For ループ コンテナー](../../integration-services/control-flow/for-loop-container.md)|条件をテストして、制御フローを繰り返し実行します。|  
|[シーケンス コンテナー](../../integration-services/control-flow/sequence-container.md)|タスクおよびコンテナーをグループ化して、パッケージ制御フローのサブセットである制御フローにします。|  
|[タスク ホスト コンテナー](../../integration-services/control-flow/task-host-container.md)|単一のタスクにサービスを提供します。|  
  
 パッケージおよびイベント ハンドラーも、コンテナーの種類に含まれます。 詳細については、「[Integration Services (SSIS) のパッケージ](../../integration-services/integration-services-ssis-packages.md)」および「[Integration Services (SSIS) のイベント ハンドラー](../../integration-services/integration-services-ssis-event-handlers.md)」を参照してください。  
  
### <a name="summary-of-container-properties"></a>コンテナー プロパティのまとめ  
 すべての種類のコンテナーには、一連の共通のプロパティがあります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に用意されているグラフィック ツールを使用してパッケージを作成すると、Foreach ループ、For ループ、およびシーケンスの各コンテナーに対して、次のプロパティが [プロパティ] ウィンドウに一覧表示されます。 タスク ホスト コンテナーのプロパティは、タスク ホストがカプセル化しているタスクの構成の一環として、 タスクを構成するときに設定します。  
  
|プロパティ|[説明]|  
|--------------|-----------------|  
|**DelayValidation**|コンテナーの検証を実行時まで遅らせるかどうかを示すブール値です。 このプロパティの既定値は、 **False**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.DelayValidation%2A>に評価されるまで、タスクを繰り返します。|  
|**[説明]**|コンテナーの説明です。 このプロパティに格納されるのは文字列で、空白にすることもできます。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Description%2A>に評価されるまで、タスクを繰り返します。|  
|**Disable**|コンテナーを実行するかどうかを示すブール値です。 このプロパティの既定値は、 **False**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Disable%2A>に評価されるまで、タスクを繰り返します。|  
|**DisableEventHandlers**|コンテナーに関連付けられているイベント ハンドラーを実行するかどうかを示すブール値です。 このプロパティの既定値は、 **False**です。|  
|**FailPackageOnFailure**|コンテナーでエラーが発生した場合、パッケージが失敗するかどうかを示すブール値です。 このプロパティの既定値は、 **False**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailPackageOnFailure%2A>に評価されるまで、タスクを繰り返します。|  
|**FailParentOnFailure**|コンテナーでエラーが発生した場合、親コンテナーが失敗するかどうかを示すブール値です。 このプロパティの既定値は、 **False**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailParentOnFailure%2A>に評価されるまで、タスクを繰り返します。|  
|**ForcedExecutionValue**|**ForcedExecutionValue** が **True**に設定されている場合は、コンテナーのオプションの実行値を含むオブジェクトです。 このプロパティの既定値は **0**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForcedExecutionValue%2A>に評価されるまで、タスクを繰り返します。|  
|**ForcedExecutionValueType**|**ForcedExecutionValue**のデータ型。 このプロパティの既定値は **Int32**です。|  
|**ForceExecutionResult**|パッケージまたはコンテナーの強制実行結果を示す値です。 有効値は、 **None**、 **Success**、 **Failure**、および **Completion**です。 このプロパティの既定値は、 **None**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionResult%2A>に評価されるまで、タスクを繰り返します。|  
|**ForcedExecutionValue**|コンテナーのオプションの実行値に特定の値を適用する必要があるかどうかを示すブール値です。 このプロパティの既定値は **False**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionValue%2A>に評価されるまで、タスクを繰り返します。|  
|**ID**|コンテナー GUID です。パッケージの作成時に割り当てられます。 このプロパティは読み取り専用です。<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A>に評価されるまで、タスクを繰り返します。|  
|**IsolationLevel**|コンテナー トランザクションの分離レベルです。 値は、 **Unspecified**、 **Chaos**、 **ReadUncommitted**、 **ReadCommitted**、 **RepeatableRead**、 **Serializable**、および **Snapshot**です。 このプロパティの既定値は **Serializable**です。 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>に評価されるまで、タスクを繰り返します。|  
|**LocaleID**|Microsoft Win32 ロケールです。 このプロパティの既定値は、ローカル コンピューター上のオペレーティング システムのロケールです。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LocaleID%2A>に評価されるまで、タスクを繰り返します。|  
|**LoggingMode**|コンテナーのログ記録の動作を指定する値です。 値は、 **Disabled**、 **Enabled**、および **UseParentSetting**です。 このプロパティの既定値は **UseParentSetting**です。 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>に評価されるまで、タスクを繰り返します。|  
|**MaximumErrorCount**|コンテナーが実行を停止するまでに発生が許可される、最大エラー数を示します。 このプロパティの既定値は **1**です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.MaximumErrorCount%2A>に評価されるまで、タスクを繰り返します。|  
|**[名前]**|コンテナーの名前です。<br /><br /> 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Name%2A>に評価されるまで、タスクを繰り返します。|  
|**TransactionOption**|コンテナーに対するトランザクションの関与を示します。 値は、 **NotSupported**、 **Supported**、および **Required**です。 このプロパティの既定値は **Supported**です。 詳細については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>に評価されるまで、タスクを繰り返します。|  
  
 Foreach ループ、For ループ、シーケンス、およびタスク ホストの各コンテナーをプログラムで構成する際に使用できるすべてのプロパティの詳細については、以下の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] API のトピックを参照してください。  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForEachLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.Sequence  
  
-   T:Microsoft.SqlServer.Dts.Runtime.TaskHost  
  
## <a name="objects-that-extend-container-functionality"></a>コンテナーの機能を拡張するオブジェクト  
 コンテナーには実行可能ファイルおよび優先順位制約で構成される制御フローが含まれ、場合によってはイベント ハンドラーおよび変数が使用されています。 ただし、タスク ホスト コンテナーは単一タスクをカプセル化し、優先順位制約を使用しない、例外的なコンテナーです。  
  
### <a name="executables"></a>実行可能ファイル  
 実行可能ファイルは、コンテナー レベルのタスクおよびコンテナー内の任意のコンテナーを参照します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が提供するタスクおよびコンテナーのいずれか、またはカスタム タスクを実行ファイルとすることができます。 詳細については、「 [Integration Services のタスク](../../integration-services/control-flow/integration-services-tasks.md)」を参照してください。  
  
### <a name="precedence-constraints"></a>優先順位制約  
 優先順位制約は、同じ親コンテナー内のコンテナーとタスクを連結して、順序付けられた制御フローを作成します。 詳細については、「 [優先順位制約](../../integration-services/control-flow/precedence-constraints.md)」を参照してください。  
  
### <a name="event-handlers"></a>イベント ハンドラー  
 コンテナー レベルのイベント ハンドラーは、コンテナーまたはそれに含まれるオブジェクトにより発生したイベントに応答します。 詳細については、「[Integration Services (SSIS) のイベント ハンドラー](../../integration-services/integration-services-ssis-event-handlers.md)」を参照してください。  
  
### <a name="variables"></a>変数:  
 コンテナーで使用される変数には、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が提供するコンテナー レベルのシステム変数、およびコンテナーが使用するユーザー定義の変数が含まれます。 詳細については、「 [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="break-points"></a>ブレークポイント  
 コンテナーにブレークポイントを設定していて、ブレークの条件が **[コンテナーに OnVariableValueChanged イベントが渡されたときに停止します]** である場合は、変数をコンテナーのスコープ内で定義します。  
  
## <a name="see-also"></a>参照  
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
