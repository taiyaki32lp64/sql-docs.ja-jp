---
title: サービス プロジェクトの開発、統合の |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- Integration Services projects, creating
- SQL Server Integration Services projects, creating
- SSIS projects, creating
ms.assetid: 6e90b016-36a5-415e-9440-a20199fffff0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3211a79c21f4c180590b53e869f9a19939b0dd19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059461"
---
# <a name="development-of-an-integration-services-project"></a>Integration Services プロジェクトの開発
  プロジェクトに [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを追加します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成して作業するには、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 環境をインストールする必要があります。 詳細については、「 [Integration Services のインストール](install-windows/install-integration-services.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で新しい [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクトを作成する場合は、 **[新しいプロジェクト]** ダイアログ ボックスに **[Integration Services プロジェクト]** テンプレートが表示されます。 このプロジェクト テンプレートでは、パッケージを 1 つ含む新しいプロジェクトが作成されます。  
  
## <a name="projects-and-solutions"></a>プロジェクトとソリューション  
 プロジェクトはソリューション内に保存されます。 最初にソリューションを作成し、次に [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトをそのソリューションに追加できます。 既存のソリューションがない場合、最初にプロジェクトを作成したときに [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] は自動的にソリューションを作成します。 1 つのソリューションにさまざまな種類の複数のプロジェクトを含めることができます。  
  
> [!NOTE]  
>  既定では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で新しい [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]プロジェクトを作成すると、そのソリューションは **ソリューション エクスプローラー** ペインに表示されません。 既定の動作を変更するには、 **[ツール]** メニューの **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスで、 **[プロジェクトおよびソリューション]** を展開し、 **[全般]** をクリックします。 **[全般]** ページで、 **[常にソリューションを表示]** を選択します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [新しい Integration Services プロジェクトを作成する](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
-   [Integration Services プロジェクトにアイテムを追加する](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)  
  
-   [ソリューション内の Integration Services プロジェクトを追加または削除する](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
  
