---
title: Integration Services (SSIS) プロジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26ab429a5f2abeda9a811e85dc5113121380e999
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892494"
---
# <a name="integration-services-ssis-projects"></a>Integration Services (SSIS) プロジェクト
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] パッケージを開発するための [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] が用意されています。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースまたは [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアにパッケージを配置する場合は、パッケージの管理に [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを使用します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]でのみ使用できます。 サービスの詳細については、「[Integration Services サービス (SSIS サービス)](service/integration-services-service-ssis-service.md)」を参照してください。 パッケージの配置の詳細については、次を参照してください。[パッケージの配置&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)します。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを配置する場合は、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で Transact-SQL のビューおよびストアド プロシージャを使用してプロジェクトを管理します。 プロジェクト配置の詳細については、「 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーの詳細については、「[Integration Services (SSIS) Server](catalog/integration-services-ssis-server-and-catalog.md)」を参照してください。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] と [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の概要については、「[Integration Services (SSIS) and Studio Environments](integration-services-ssis-development-and-management-tools.md)」(Integration Services (SSIS) と Studio 環境) を参照してください。  
  
## <a name="understanding-integration-services-projects"></a>Integration Services プロジェクトについて  
 プロジェクトとは [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開発するコンテナーのことです。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトにはパッケージに関連するファイルが格納され、グループ化されます。 たとえば、プロジェクトには、特定の抽出、変換、および読み込み (ETL) ソリューションの作成に必要なファイルが含まれます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成する前に、この種のプロジェクトの基本的な内容を理解しておく必要があります。 プロジェクトの内容を理解すれば、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの作成および作業を開始することができます。  
  
### <a name="folders-in-integration-services-projects"></a>Integration Services プロジェクトのフォルダー  
 次の図は、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] での [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクト内のフォルダーを示しています。  
  
 ![Integration Services プロジェクトのフォルダー](media/solutionexplorer.gif "Integration Services プロジェクトのフォルダー")  
  
 次の表では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに表示されるフォルダーについて説明します。  
  
|フォルダー|説明|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ|パッケージが含まれます。 詳細については、「[Integration Services &#40;SSIS&#41; Packages](../../2014/integration-services/integration-services-ssis-packages.md)」を参照してください。|  
|その他|パッケージ ファイル以外のファイルが含まれます。|  
  
### <a name="files-in-integration-services-projects"></a>Integration Services プロジェクトのファイル  
 新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトまたは既存のプロジェクトをソリューションに追加すると、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] により、.dtproj、.dtproj.user、および .database 拡張子を持つプロジェクト ファイルが作成されます。  
  
-   *.dtproj ファイルには、プロジェクトの構成と、パッケージなどのアイテムに関する情報が含まれます。  
  
-   *.dtproj.user ファイルには、プロジェクト処理の設定に関する情報が含まれます。  
  
-   *.database ファイルには、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開くために必要な情報が含まれます。  
  
## <a name="understanding-solutions"></a>ソリューションの詳細  
 ソリューションとは、エンド ツー エンドのビジネス ソリューションを開発するときに使用するプロジェクトを、グループ化して管理するコンテナーのことです。 ソリューションを使用すると、複数のプロジェクトを 1 単位として処理し、ビジネス ソリューションに役立つ 1 つ以上の関連プロジェクトをまとめることができます。  
  
 ソリューションには、さまざまな種類のプロジェクトを含めることができます。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを作成する場合は、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で用意されているソリューション内の [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクトで作業します。  
  
 新しいソリューションを作成すると、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] のソリューション エクスプローラーにソリューション フォルダーが自動的に追加され、拡張子 .sln および .suo のファイルが作成されます。  
  
-   *.sln ファイルには、ソリューションの構成情報、およびソリューション内のプロジェクトの一覧が格納されます。  
  
-   *.suo ファイルには、ソリューションを操作するうえでのユーザー設定情報が格納されます。  
  
 新しいプロジェクトを作成すると [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] でソリューションが自動的に作成されますが、空白のソリューションを作成して、プロジェクトを後で追加することもできます。  
  
> [!NOTE]  
>  既定では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で新しい [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクトを作成すると、そのソリューションは **プロジェクト エクスプローラー** ペインに表示されません。 既定の動作を変更するには、 **[ツール]** メニューの **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスで、 **[プロジェクトおよびソリューション]** を展開し、 **[全般]** をクリックします。 **[全般]** ページで、 **[常にソリューションを表示]** を選択します。  
  
## <a name="related-tasks"></a>Related Tasks  
 [ソリューション内の Integration Services プロジェクトを追加または削除する](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
 [新しい Integration Services プロジェクトを作成する](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
 [Integration Services プロジェクトにアイテムを追加する](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)  
  
 [プロジェクト アイテムをコピーする](../../2014/integration-services/copy-project-items.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [Integration Services プロジェクトの開発](../../2014/integration-services/development-of-an-integration-services-project.md)  
  
  
