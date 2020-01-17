---
title: インストール先の指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- installation targets [Analysis Services]
- Analysis Services deployments, installation targets
- Analysis Services Deployment Wizard, installation targets
- deploying [Analysis Services], installation targets
- modifying installation targets
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5a46dc4c6130bb49d973ffc0025388c563c080f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075219"
---
# <a name="specifying-the-installation-target"></a>インストール先の指定
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]展開ウィザードからインストール先の情報を読み取り、 \<*プロジェクト名*> >.deploymenttargets ファイル。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの作成時にこのファイルを作成します。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] データベースとで指定したサーバーを使用して、**展開**のページ、 *\<プロジェクト名 >* **プロパティ ページ**を作成するダイアログボックス\<*プロジェクト名*> .targets ファイル。  
  
## <a name="modifying-the-installation-target-for-deployment"></a>配置に関するインストール先の変更  
 場合によっては、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [配置] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ページで指定されたものとは別のデータベースまたは **インスタンスに** プロジェクトを配置する必要が生じることがあります。 たとえば、配置前のテストを行うためにプロジェクトをサーバーに配置し、テストの完了後にそのプロジェクトを実稼働サーバーに配置する必要が生じることがあります。 また、完成したテスト済みのプロジェクトをネットワーク負荷分散クラスター内の複数の実稼働サーバーに配置するか、ステージング サーバーおよび実稼働サーバーに配置する必要が生じることもあります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを別のデータベースまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに配置するには、次の手順で説明するいずれかの方法に従って、入力ファイル内のインストール先を変更します。  
  
#### <a name="to-change-the-installation-target-after-the-input-files-have-been-generated"></a>入力ファイルの生成後にインストール先を変更するには  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを対話形式で実行します。 **[インストールの対象]** ページで、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスとデータベースの新しいインストール先を指定します。  
  
     \- または -  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードをコマンド プロンプトで実行し、ウィザードを応答ファイル モードで実行するように設定します。 応答ファイル モードの詳細については、「 [Analysis Services 配置ウィザードの実行](running-the-analysis-services-deployment-wizard.md)」を参照してください。  
  
     \- または -  
  
-   変更、 \<*プロジェクト名*> 任意のテキスト エディターを使用して、>.deploymenttargets ファイル。  
  
## <a name="see-also"></a>関連項目  
 [パーティションおよびロールの配置オプションの指定](deployment-script-files-partition-and-role-deployment-options.md)   
 [ソリューションの配置に関する構成設定の指定](deployment-script-files-solution-deployment-config-settings.md)   
 [処理オプションの指定](deployment-script-files-specifying-processing-options.md)  
  
  
