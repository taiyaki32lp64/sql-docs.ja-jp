---
title: モデルの配置パッケージの例
ms.custom: ''
ms.date: 07/28/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- マスター データ サービス
- sample
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 19b4cc9cc9282fff784059e6ac39bf74792f95a4
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727879"
---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>SQL Server の例: モデルの配置パッケージ (MDS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]をインストールすると、データの入ったサンプル モデル パッケージが追加されます。 サンプル モデル パッケージの既定の場所は、\<ドライブ>\Program Files\Microsoft SQL Server\130\Master Data Services\Samples\Packages です。  
  
 サンプル モデル パッケージを配置する方法については、「 [サンプル モデルとデータを配置する](../master-data-services/master-data-services-installation-and-configuration.md#deploySample)」を参照してください。 サンプル モデル パッケージは、 [MDSModelDeploy ツール](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)を使用して配置します。  
  
> [!IMPORTANT]
>  **サンプルの更新: [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
> 
>  次の新しい機能をサポートするためにサンプル パッケージが更新されました。  
> 
>  -   多対多リレーションシップの表示。  
> 
>      詳細については、「 [サンプル モデル内の M2M リレーションシップ](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample)」を参照してください。  
> 
> -   ドメイン ベースの属性の指定できる値を制限します。  
> 
>      詳細については、「[ドメイン ベースの属性を作成する (マスター データ サービス)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)」を参照してください。  
> -   エンティティの変更に承認が必要。  
> 
>      詳細については、「[承認が必要 (マスター データ サービス)](../master-data-services/approval-required-master-data-services.md)」を参照してください。  
> -   ビジネス ルールでの Not および Else 演算子の使用。  
> 
>      詳細については、「 [ビジネス ルールの例](../master-data-services/business-rule-examples-master-data-services.md)」を参照してください。  
> -   カスタム インデックスの実装  
> 
>      詳細については、「[カスタム インデックス (マスター データ サービス)](../master-data-services/custom-index-master-data-services.md)」を参照してください。  
 

 
 マスター データ サービスのパッケージは、配置可能なモデル構造と (必要に応じて) モデル データを含んだ XML ファイルです。 モデル パッケージを使用して、モデルのコピーを MDS 環境間で移動したり、既存の [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 環境に新しいモデルを作成したりすることができます。  
  
## <a name="see-also"></a>参照  
 [MDSModelDeploy を使用したモデルの配置パッケージの配置](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
