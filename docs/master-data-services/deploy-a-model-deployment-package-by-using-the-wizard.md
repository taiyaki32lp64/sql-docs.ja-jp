---
title: モデル配置パッケージの配置 (ウィザード)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], deploying
- models [Master Data Services], deploying a package
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7e41af6f7b5f1d2a770400ab66191f7957937659
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729393"
---
# <a name="deploy-a-model-deployment-package-by-using-the-wizard"></a>ウィザードを使用したモデルの配置パッケージの展開

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  モデル オブジェクトのみが含まれているパッケージを配置するには、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のモデル配置ウィザードを使用します。 データを含むパッケージを配置する必要がある場合は、「 [MDSModelDeploy を使用したモデルの配置パッケージの配置](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)」を参照してください。  
  
> [!IMPORTANT]  
>  パッケージは、そのパッケージが作成されたエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にのみ配置できます。 つまり、 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] で作成されたパッケージを [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]に配置することはできません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   ターゲット **環境の** [システム管理] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 機能領域にアクセスする権限が必要です。  
  
-   モデルの配置パッケージが必要です。 詳細については、「 [ウィザードを使用したモデルの配置パッケージの作成](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)」を参照してください。  
  
-   モデルを配置する環境の管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-deploy-a-model-deployment-package-of-model-objects-only"></a>モデル オブジェクトのみのパッケージを配置するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデル ビュー]** ページのメニュー バーから **[システム]** をポイントして **[配置]** をクリックします。  
  
3.  **[モデル配置ウィザード]** で **[配置]** をクリックします。  
  
4.  **[参照]** をクリックします。  
  
5.  配置パッケージ (.pkg ファイル) を見つけて **[開く]** をクリックします。  
  
6.  **[次へ]** をクリックします。  
  
7.  パッケージが読み込まれたら **[次へ]** をクリックします。  
  
8.  モデルが既に存在する場合は、 **[既存のモデルを更新する]** を選択することによって、そのモデルを更新できます。 新しいモデルを作成するには、 **[新しいモデルを作成する]** を選択し、 **[次へ]** をクリックした後に新しいモデルの名前を入力できます。  
  
9. **[完了]** をクリックして、ウィザードを終了します。  
  
 **注:**  
  
-   パッケージ内のサブスクリプション ビューの名前が、既存のモデル内のサブスクリプション ビューの名前と同じである場合、" **配置機能サブスクリプション ビューが名前変更されました**" という警告が表示されます。 さらに、このビューは *modelname.subscriptionviewname*として作成されます。 この名前が既に使用されている場合、サブスクリプション ビューは作成されません。  
  
-   配置プロセスには、次の 4 つの手順があります。  
  
    1.  モデル オブジェクトが作成されます。  
  
    2.  サブスクリプション ビューが作成されます。  
  
    3.  ビジネス ルールが作成されます。  
  
-   新しいモデルまたは複製モデルを作成する場合、いずれかの手順の実行中にプロセスが失敗すると、モデルは削除されます。  
  
     モデルを更新する場合、最初の 3 つの手順のいずれかでプロセスが失敗すると、その手順から先のプロセスは続行されません。ただし、既に行われた変更はロールバックされません。  
  
## <a name="next-steps"></a>次の手順  
 ファイル属性、ユーザーとグループの権限は、モデル配置パッケージに含まれていません。 モデルを配置した後、これらを手動で更新する必要があります。 詳細については、以下をご覧ください。  
  
-   [モデル オブジェクト権限を割り当てる (マスター データ サービス)](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [モデルの配置 (マスター データ サービス)](../master-data-services/deploying-models-master-data-services.md)  
  
  
