---
title: 親パッケージの実装 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parent packages [Integration Services]
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cec1f30ba728f1cf3b808acb2fb362e21d259a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058156"
---
# <a name="implementation-of-the-parent-package"></a>親パッケージの実装
  さまざまなサーバー間で SSIS パッケージの負荷を分散する場合、子パッケージの作成と配置を行い、その子パッケージを実行するためのリモート SQL Server エージェント ジョブを作成したら、次のステップは親パッケージを作成することです。 親パッケージには、SQL Server エージェント ジョブの実行タスクが多数含まれます。各タスクは、子パッケージの 1 つを実行する個別の SQL Server エージェント ジョブを呼び出します。 親パッケージ内にある SQL Server エージェント ジョブの実行タスクは、各種の SQL Server エージェント ジョブを次々に実行します。 親パッケージ内の各タスクには、リモート サーバーへの接続方法やそのサーバーで実行するジョブなどの情報が含まれています。 詳しくは、「 [Execute SQL Server Agent Job Task](control-flow/execute-sql-server-agent-job-task.md)」をご覧ください。  
  
 子パッケージを実行する親パッケージを識別するには、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] のソリューション エクスプローラーでパッケージを右クリックし、 **[エントリ ポイント パッケージ]** をクリックします。  
  
## <a name="listing-child-packages"></a>子パッケージの一覧表示  
 親パッケージと子パッケージを含むプロジェクトを [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに配置した場合、親パッケージにより実行される子パッケージの一覧を表示することができます。 親パッケージを実行すると、 **に親パッケージの** [概要] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]レポートが自動的に生成されます。 次の図のように、レポートには、親パッケージに含まれるパッケージ実行タスクによって実行された子パッケージが一覧表示されます。  
  
 ![子パッケージの一覧を含む概要レポート](media/overviewreport-childpackagelisting.png "子パッケージの一覧を含む概要レポート")  
  
 **[概要]** レポートのアクセスについては、「 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)」を参照してください。  
  
## <a name="precedence-constraints-in-the-parent-package"></a>親パッケージの優先順位制約  
 親パッケージ内の複数の SQL Server エージェント ジョブの実行タスク間で優先順位制約を作成する場合、これらの優先順位制約で制御されるのは、リモート サーバー上の SQL Server エージェント ジョブの開始時刻のみです。 優先順位制約では、SQL Server エージェント ジョブのステップで実行される子パッケージが、成功したか失敗したかに関する情報を受け取ることができません。  
  
 つまり、子パッケージの成功または失敗は親に伝達されません。これは、親パッケージ内の SQL Server エージェント ジョブの実行タスクには、SQL Server エージェント ジョブに子パッケージを実行することを要求する機能しかないためです。 SQL Server エージェント ジョブが正しく呼び出されると、親パッケージは、<xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> という結果を受け取ります。  
  
 このシナリオでの失敗とは、リモート SQL Server エージェント ジョブ タスクの呼び出しに失敗した場合しかありません。 このような失敗は、リモート サーバーが停止している場合、およびエージェントが応答しない場合に発生することがあります。 ただし、エージェントが起動している限り、親パッケージはそのタスクを正常に完了したことになります。  
  
> [!NOTE]  
>  **sp_start_job N'package_name'** の Transact-SQL ステートメントを含む SQL 実行タスクを使用できます。 詳細については、「[sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)」をご覧ください。  
  
## <a name="debugging-environment"></a>デバッグ環境  
 親パッケージをテストする場合は、[デバッグ] メニューの [デバッグの開始] をクリックして (または F5 キーを押して) そのパッケージを実行し、デザイナーのデバッグ環境を使用します。 または、コマンド プロンプト ユーティリティ **dtexec**を使用できます。 詳しくは、「 [dtexec Utility](packages/dtexec-utility.md)」をご覧ください。  
  
  
