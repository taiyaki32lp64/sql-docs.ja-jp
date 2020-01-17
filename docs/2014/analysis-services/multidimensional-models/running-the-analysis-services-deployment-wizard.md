---
title: 分析を実行しているサービスの展開ウィザード |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, running
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8fd34a7e614c1c1bb247f84846e090d22ea053e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073038"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>Analysis Services 配置ウィザードの実行
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを配置するときは、ウィザードを次の方法で実行できます。  
  
-   **対話的に実行** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを対話的に実行すると、ユーザーの入力によって対話的に変更された入力ファイルに基づいて、XML 配置スクリプトが生成されます。 ユーザーによる変更は、配置スクリプトのみに適用されます。 入力ファイルが変更されることはありません。 入力ファイルの詳細については、「 [配置スクリプトを作成するための入力ファイルについて](deployment-script-files-input-used-to-create-deployment-script.md)」を参照してください。  
  
-   **コマンド プロンプトから**、コマンド プロンプトで実行すると、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]展開ウィザードには、XML for Analysis (XMLA) 配置スクリプトを使用して、ウィザードを実行するスイッチに基づいてが生成されます。 ウィザードでは、ユーザーの入力を求めてその入力に基づいて入力ファイルを変更するか、入力ファイルをそのまま使用して自動的に配置を実行するか、後で使用可能な配置スクリプトを作成します。  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>Analysis Services 配置ウィザードの対話的な実行  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを対話的に実行すると、入力ファイルから値が読み取られ、その情報が提示されます。 配置先、構成設定、配置オプション、および接続文字列のパスワードとしてこれらの入力値などを変更できるはそのまま使用します。 入力値を変更した場合、ウィザードではこれらの変更値を使用して XMLA 配置スクリプトを生成します。 ただし、入力ファイルの値は変更されません。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードで入力値が変更されるようにするには、コマンド プロンプトでウィザードを応答ファイル モードで実行します。  
  
 入力値を確認し、必要な変更を行うと、ウィザードによって XMLA 配置スクリプトが生成されます。 この配置スクリプトは配置先サーバーで直ちに実行することも、後で使用するために保存することもできます。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>Analysis Services 配置ウィザードを対話的に実行するには  
  
-   **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** 、 **[Analysis Services]** の順にポイントして、 **[配置ウィザード]** をクリックします。  
  
     \- または -  
  
-   **プロジェクト**のフォルダー、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロジェクトで、ダブルクリックして、 *\<プロジェクト名 >* .asdatabase ファイル。  
  
    > [!NOTE]  
    >  見つからない場合、 *\<プロジェクト名 >* .asdatabase ファイルは「*.asdatabase を指定して検索を使用してみてください。  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>コマンド プロンプトでの Analysis Services 配置ウィザードの実行  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードは、コマンド プロンプトで実行することもできます。 コマンド プロンプトを使用する場合は、.asdatabase ファイルへの完全パスを指定し、次のいずれかのモードでウィザードを実行します。  
  
 **応答ファイル モード**  
 応答ファイル モードでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトが [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でビルドされたときに生成された入力ファイルを対話的に変更できます。 これらの変更された入力ファイルは XMLA 配置スクリプトの生成前に保存されます。 変更された入力ファイルは、次にウィザードを実行したときの開始点として使用されます。  
  
 応答ファイル モードでウィザードを実行するには使用、 **/a**スイッチします。  
  
 **サイレント モード**  
 サイレント モードでは、ウィザードは入力ファイルに含まれている情報に基づいて、自動的に配置を実行します。  
  
 サイレント モードでウィザードを実行するには使用、 **/s**スイッチします。 サイレント モードでウィザードを実行した場合、メッセージはコンソールに出力されます。ログ ファイルを指定した場合はログ ファイルに出力されます。  
  
 **出力モード**  
 出力モードでは、ウィザードは入力ファイルに基づいて、後で実行するための XMLA 配置スクリプトを生成します。  
  
 出力モードでウィザードを実行するには使用、 **/o**切り替えるし、出力ファイル名を指定します。  
  
 これらのコマンド ライン スイッチの詳細については、「 [配置ユーティリティを使用したモデル ソリューションの配置](deploy-model-solutions-with-the-deployment-utility.md)」を参照してください。  
  
 次の手順では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードをコマンド プロンプトで実行する方法について説明します。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Analysis Services 配置ウィザードをコマンド プロンプトで実行するには  
  
1.  コマンド プロンプトを開き、C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE フォルダーに移動します。  
  
2.  「 **Microsoft.AnalysisServices.Deployment.exe** 」の後に、ウィザードを実行するモードに対応するスイッチを入力します。  
  
## <a name="see-also"></a>参照  
 [Analysis Services 配置スクリプトについて](understanding-the-analysis-services-deployment-script.md)   
 [Deploy Model Solutions Using the Deployment Wizard](deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
