---
title: プロジェクトとパッケージの実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5a3ecbe615d60a703b66dff78cd77ddfde0a20d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767086"
---
# <a name="execution-of-projects-and-packages"></a>プロジェクトとパッケージの実行
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを実行するには、それらのパッケージの格納場所に応じていくつかのツールのうちの 1 つを使用できます。 次の表にツールを示します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーにパッケージを格納するには、プロジェクト配置モデルを使用してプロジェクトをサーバーに配置します。 詳細については、「 [Integration Services サーバーへのプロジェクトの配置](../deploy-projects-to-integration-services-server.md)」を参照してください。  
  
 SSIS パッケージ ストア、msdb データベース、またはファイル システムにパッケージを格納するには、パッケージ配置モデルを使用します。 詳細については、次を参照してください。[パッケージの配置&#40;SSIS&#41;](legacy-package-deployment-ssis.md)します。  
  
|ツール|Integration Services サーバーに格納されているパッケージ|SSIS パッケージ ストアまたは msdb データベースに格納されているパッケージ|ファイル システムに格納されているパッケージ (SSIS パッケージ ストアに含まれる場所の範囲外)|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|いいえ|いいえ<br /><br /> ただし、msdb データベースを含む [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアからプロジェクトに既存のパッケージを追加できます。 この方法でプロジェクトに既存のパッケージを追加すると、ファイル システム内にパッケージのローカル コピーが作成されます。|はい|  
|**SQL Server Management Studio (Integration Services サーバーをホストするデータベース エンジンのインスタンスに接続している場合)**<br /><br /> 詳細については、「 [[パッケージの実行] ダイアログ ボックス](../execute-package-dialog-box.md)」を参照してください。|はい|いいえ<br /><br /> ただし、これらの場所からサーバーにパッケージをインポートできます。|いいえ<br /><br /> ただし、ファイル システムからサーバーにパッケージをインポートできます。|  
|**SQL Server Management Studio (SSIS パッケージ ストアを管理する Integration Services サービスに接続している場合)**|いいえ|はい|いいえ<br /><br /> ただし、ファイル システムから [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアにパッケージをインポートできます。|  
|**dtexec**<br /><br /> 詳しくは、「 [dtexec Utility](dtexec-utility.md)」をご覧ください。|はい|[はい]|はい|  
|**dtexecui**<br /><br /> 詳細については、「[パッケージ実行ユーティリティ &#40;DtExecUI&#41; の UI リファレンス](execute-package-utility-dtexecui-ui-reference.md)」を参照してください。|いいえ|はい|はい|  
|**SQL Server エージェント**<br /><br /> パッケージのスケジュールを設定するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを使用します。<br /><br /> 詳細については、「 [パッケージに対する SQL Server エージェント ジョブ](sql-server-agent-jobs-for-packages.md)」を参照してください。|はい|[はい]|はい|  
|**組み込みのストアド プロシージャ**<br /><br /> 詳細については、「[catalog.start_execution &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)」を参照してください。|はい|いいえ|いいえ|  
|**API (**<xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間の型およびメンバーを使用)|はい|いいえ|いいえ|  
|**API (**<xref:Microsoft.SqlServer.Dts.Runtime> 名前空間の型およびメンバーを使用)|現時点ではいいえ|はい|はい|  
  
## <a name="execution-and-logging"></a>実行とログ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージではログ記録を有効にできるので、実行時情報をログ ファイルに保存できます。 詳細については、「[Integration Services (SSIS) のログ記録](../performance/integration-services-ssis-logging.md)」をご覧ください。  
  
 操作レポートを使用して、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置され、実行されている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを監視できます。 レポートは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で利用できます。 詳細については、「 [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [SQL Server エージェントを使用してパッケージのスケジュールを設定する](../schedule-a-package-by-using-sql-server-agent.md)  
  
-   [SQL Server Data Tools でのパッケージの実行](../run-a-package-in-sql-server-data-tools.md)  
  
-   [SQL Server Management Studio を使用した SSIS サーバーでのパッケージの実行](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>参照  
 [dtexec ユーティリティ](dtexec-utility.md)   
 [SQL Server インポートおよびエクスポート ウィザード](../import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)  
  
  
