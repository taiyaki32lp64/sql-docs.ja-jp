---
title: Integration Services サーバーへのプロジェクトの配置 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6e9402f4-4d50-49ff-820d-65a77829c4a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4e260825532f66205e301628f60d68d93f8e7c04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059577"
---
# <a name="deploy-projects-to-integration-services-server"></a>Integration Services サーバーへのプロジェクトの配置
  現在のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーにプロジェクトを配置できます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーを使用すると、さまざまな環境を利用して、パッケージの管理、パッケージの実行、およびパッケージに合わせたランタイム値の構成を行うことができます。  
  
 環境の詳細については、「 [サーバー環境の作成とマップ](../../2014/integration-services/create-and-map-a-server-environment.md)」を参照してください。  
  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]と同様に、現在のリリースでも、パッケージを SQL Server のインスタンスに配置し、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを使用してパッケージを実行および管理できます。 パッケージ配置モデルを使用できます。 詳細については、次を参照してください。[パッケージの配置&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)します。  
  
 プロジェクトを [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに配置するには、次の作業を実行します。  
  
1.  SSISDB カタログをまだ作成していない場合は、作成します。 詳細については、「 [SSIS カタログの作成](catalog/ssis-catalog.md)」を参照してください。  
  
2.  **Integration Services プロジェクト変換ウィザード** を実行して、プロジェクトをプロジェクト配置モデルに変換します。 詳細については、後の手順を参照してください。[プロジェクトをプロジェクトの配置モデルに変換するには](#convert)  
  
    -   [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)]でプロジェクトを作成した場合、既定では、プロジェクトでプロジェクト配置モデルが使用されます。  
  
    -   以前のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]でプロジェクトを作成した場合、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でプロジェクト ファイルを開いた後に、プロジェクトをプロジェクト配置モデルに変換します。  
  
        > [!NOTE]  
        >  プロジェクトに含まれている 1 つ以上のデータ ソースは、プロジェクトの変換が完了すると削除されます。 プロジェクト内のパッケージで共有できるデータ ソースへの接続を作成するには、プロジェクト レベルで接続マネージャーを追加します。 詳細については、「 [パッケージでの接続マネージャーの追加、削除、または共有](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)」 を参照してください。  
  
         **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] または [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のいずれから実行するかによって、ウィザードが実行する変換タスクは異なります。  
  
        -   ウィザードを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]から実行した場合、プロジェクトに含まれるパッケージは [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 2005、2008、または 2008 R2 から現在のバージョンの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]で使用されている形式に変換されます。 元のプロジェクト (.dtproj) ファイルおよびパッケージ (.dtsx) ファイルはアップグレードされます。  
  
        -   ウィザードを [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]から実行した場合、プロジェクトに含まれるパッケージおよび構成からプロジェクト配置ファイル (.ispac) が生成されます。 元のパッケージ (.dtsx) ファイルはアップグレードされません。  
  
             ウィザードの **[変換先の選択]** ページで、既存のファイルを選択するか、新規ファイルを作成することができます。  
  
             プロジェクトの変換時にパッケージ ファイルをアップグレードするには、 **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]から実行します。 プロジェクトの変換とは別にパッケージ ファイルをアップグレードするには、 **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] から実行してから、 **SSIS パッケージ アップグレード ウィザード**を実行します。 パッケージ ファイルを個別にアップグレードする場合は、必ず変更を保存します。 保存しないと、プロジェクトをプロジェクトの配置モデルに変換するときに、パッケージに対する未保存の変更が変換されません。  
  
     パッケージのアップグレードの詳細については、「 [Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages.md) 」および「 [SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)」を参照してください。  
  
3.  プロジェクトを [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに配置します。 詳細については、後の手順を参照してください。[Integration Services サーバーにプロジェクトを配置するには](#deploy)。  
  
4.  (省略可能) 配置されたプロジェクト用の環境を作成します。 詳細については、「 [サーバー環境の作成とマップ](../../2014/integration-services/create-and-map-a-server-environment.md)」を参照してください。  
  
##  <a name="convert"></a> プロジェクトをプロジェクトの配置モデルに変換するには  
  
1.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でプロジェクトを開き、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロジェクト配置モデルに変換]** をクリックします。  
  
     \- または -  
  
     オブジェクト エクスプローラーの [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]で、 **[プロジェクト]** ノードを右クリックし、 **[パッケージのインポート]** を選択します。  
  
2.  ウィザードを完了します。 詳細については、「 [Integration Services プロジェクトの変換ウィザード](../../2014/integration-services/integration-services-project-conversion-wizard.md)」を参照してください。  
  
##  <a name="deploy"></a> Integration Services サーバーにプロジェクトを配置するには  
  
1.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でプロジェクトを開き、 **[プロジェクト]** メニューの **[配置]** を選択して、 **Integration Services 配置ウィザード**を起動します。  
  
     -または-  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーで、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] > **SSISDB** ノードの順に展開し、配置するプロジェクトの [プロジェクト] フォルダーを探します。 **[プロジェクト]** フォルダーを右クリックして **[プロジェクトの配置]** をクリックします。  
  
     \- または -  
  
     コマンド プロンプトで、 **%ProgramFiles%\Microsoft SQL Server\110\DTS\Binn** にある **isdeploymentwizard.exe**を実行します。 64 ビット コンピューターの場合、 **%ProgramFiles(x86)%\Microsoft SQL Server\100\DTS\Binn**に 32 ビット バージョンのツールもあります。  
  
2.  **[ソースの選択]** ページで、 **[プロジェクト配置ファイル]** をクリックして、プロジェクトの配置ファイルを選択します。  
  
     -または-  
  
     **[Integration Services カタログ]** をクリックし、SSISDB カタログに既に配置されているプロジェクトを選択します。  
  
3.  ウィザードを完了します。 詳細については、「 [Integration Services 配置ウィザード](../../2014/integration-services/integration-services-deployment-wizard.md)」を参照してください。  
  
  
