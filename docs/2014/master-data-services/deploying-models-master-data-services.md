---
title: モデルの配置 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], about deployment packages
- deployment packages [Master Data Services]
ms.assetid: 30085c08-034f-4efe-80fe-408f9091ff5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6b631686e9daf716bb124ce5fadaf7575420a114
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483145"
---
# <a name="deploying-models-master-data-services"></a>モデルの配置 (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]におけるパッケージは、配置可能なモデル構造と (必要に応じて) モデル データを含んだ XML ファイルです。 モデル パッケージを使用して、モデルのコピーを MDS 環境間で移動したり、既存の MDS 環境に新しいモデルを作成したりすることができます。  
  
> [!IMPORTANT]  
>  パッケージは、そのパッケージが作成されたエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にのみ配置できます。 つまり、 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] で作成されたパッケージを [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 以降に配置することはできません。  
  
## <a name="tools-for-deploying-models"></a>モデルを展開するためのツール  
 モデル パッケージを使用するには、3 つのツールをニーズに応じて使い分けることができます。  
  
-   **MDSModelDeploy ツール**: モデル オブジェクトとデータを作成して配置するには、MDSModelDeploy.exe ツールを使用します。 MDS をインストールするときに、既定のパスを選択した場合は、このツールはあります*ドライブ*: \Program Files\Microsoft SQL server \120\master Data services \configuration にあります。  
  
-   **モデル配置ウィザード**: モデルの構造のみのパッケージを作成して配置するには、[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションのウィザードを使用します。 このウィザードを使用して、データを配置することはできません。  
  
-   **モデル パッケージ エディター**: モデル パッケージを編集するには、ModelPackageEditor.exe を使用してモデル パッケージ エディター ウィザードを起動します。 このウィザードを使用して、MDSModelDeploy ツールまたはモデル配置ウィザードによって作成されたパッケージを編集します。 MDS をインストールするときに、既定のパスを選択した場合は、このツールはあります*ドライブ*: \Program Files\Microsoft SQL server \120\master Data services \configuration にあります。  
  
> [!IMPORTANT]  
>  MDSDeployModel を使用すると、新しいモデルの作成、モデルの複製の作成、または既存のモデルとそのデータの更新を実行できます。 MDSModelDeploy ツールを使用して既存のモデルとそのデータを更新するときに、配置先モデルに存在するエンティティ、属性、またはメンバーがパッケージに含まれていない場合は、MDSModelDeploy によって、そのエンティティ、属性、またはメンバーがモデルから削除されることはありません。  
  
## <a name="what-packages-contain"></a>パッケージに含められるもの  
 モデル パッケージは、.pkg 拡張子付きで保存される XML ファイルです。 配置パッケージを作成する場合、データを含めるかどうかを決定できます。 データを含める場合は、含めるデータのバージョンを選択する必要があります。  
  
 パッケージには、すべてのモデル オブジェクトが含まれています。 オブジェクトを次に示します。  
  
-   [エンティティ]  
  
-   属性  
  
-   属性グループ  
  
-   階層  
  
-   コレクション  
  
-   ビジネス ルール  
  
-   バージョン フラグ  
  
-   サブスクリプション ビュー  
  
 ユーザー定義メタデータ、ファイル属性、ユーザーの権限、およびグループの権限は含めることができません。 モデルを配置した後、これらを手動で更新する必要があります。  
  
## <a name="sample-packages"></a>サンプル パッケージ  
 サンプル パッケージ ファイルは [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]のインストールに含まれています。 このパッケージ ファイルは、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]をインストールした Master Data Services\Samples\Packages ディレクトリにあります。 MDSModelDeploy ツールを使用してサンプル パッケージを配置したときに、サンプル モデルが作成されデータが読み込まれます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|MDSModelDeploy ツールを使用して、モデル オブジェクトとデータの新しい配置パッケージを作成します。|[MDSModelDeploy を使用したモデルの配置パッケージの作成](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|ウィザードを使用して、モデル オブジェクトのみの新しい配置パッケージを作成します。|[ウィザードを使用したモデルの配置パッケージの作成](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)|  
|MDSModelDeploy ツールを使用して、モデル オブジェクトとデータのパッケージを配置します。|[MDSModelDeploy を使用したモデルの配置パッケージの配置](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|ウィザードを使用して、モデル オブジェクトのみのパッケージを配置します。|[ウィザードを使用したモデルの配置パッケージの展開](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)|  
|モデル全体ではなく、モデルの選択した部分を配置するには、モデルの配置パッケージを編集します。|[モデルの配置パッケージの編集](../../2014/master-data-services/edit-a-model-deployment-package.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [モデル配置オプション (マスター データ サービス)](model-deployment-options-master-data-services.md)  
  
  
