---
title: Integration Services 配置ウィザード |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 721953c31a44a2ea02f480c9830e6347adfd4eb3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058006"
---
# <a name="integration-services-deployment-wizard"></a>Integration Services 配置ウィザード
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 配置ウィザードでは、プロジェクト配置モデルを使用して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスの SSISDB カタログにプロジェクトが配置されます。  
  
 開始する、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]で開いているプロジェクトからの展開ウィザード[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]を選択します**デプロイ**から、**プロジェクト**メニュー。 ウィザードを起動する[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]、展開、 **Integration Services カタログ** > **SSISDB**オブジェクト エクスプ ローラーでノードを右クリックし、**プロジェクト**フォルダー、およびクリック**プロジェクトの配置**します。  
  
 このウィザードでは、次の 4 つの手順を行います。 をクリックして **[次へ]** 次の手順に移動するまたは**前**前の手順に戻ります。  
  
1.  **ソースの選択**- 選択、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]に展開するプロジェクト。  
  
2.  **変換先を選択します。** -プロジェクトの配置先を選択します。  
  
3.  **レビュー** -選択内容を表示します。  
  
4.  **配置/結果**: プロジェクトを配置し、結果が表示されます。  
  
## <a name="select-source"></a>[ソースの選択]  
 作成したプロジェクト配置ファイルを展開するには、選択**プロジェクト配置ファイル**.ispac ファイルにパスを入力するかをクリックし、**参照**で検索する、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プロジェクト フォルダーです。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログにあるプロジェクトを配置するには、 **[Integration Services カタログ]** を選択し、サーバー名とカタログ内のプロジェクトのパスを入力します。  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でウィザードを起動すると、既定では、開いているプロジェクトがソースとして選択され、この手順が省略されます。 この手順に戻って、別のソースを選択してをクリックします。**前** をクリックまたは**ソースの選択**左側のウィンドウでします。  
  
## <a name="select-destination"></a>[配置先の選択]  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] カタログでプロジェクトの配置先フォルダーを選択するには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスを入力するか、 **[参照]** をクリックしてサーバーの一覧から選択します。 SSISDB でプロジェクトのパスを入力するか、 **[参照]** をクリックしてプロジェクトを選択します。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でウィザードを起動すると、既定では、接続されているサーバー インスタンスが選択され、選択したプロジェクトのパスが入力されます。 プロジェクトを別の場所に配置するようにこれらの値を変更できます。  
  
## <a name="review"></a>確認  
 プロジェクトを配置する前に、選択した設定をウィザードで確認できます。 選択内容を変更するには、 **[戻る]** をクリックするか、左ペインでいずれかの手順をクリックします。  
  
## <a name="deployresults"></a>配置/結果  
 クリックすると**デプロイ**から、**レビュー**  ページで、プロジェクトが展開されていると、**結果**ページは、各アクションの成否が表示されます。 アクションが失敗した場合は、 **[結果]** 列の **[失敗]** をクリックすると、エラーの説明が表示されます。 クリックして**レポートを保存しています.** 結果を XML ファイルに保存します。  
  
 **[閉じる]** をクリックしてウィザードを終了します。  
  
## <a name="see-also"></a>参照  
 [Integration Services サーバーへのプロジェクトの配置](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [プロジェクトとパッケージの展開](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
