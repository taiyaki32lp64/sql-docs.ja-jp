---
title: モデルの構築 (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a6f3f669f0f1699618399bbfdccaf33f6e4c13a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092493"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>モデルの構築 (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]の管理者は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションで利用可能な管理機能のサブセットを実行できます。  
  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] で管理者が実行できるモデル構築タスクは次のとおりです。  
  
-   エンティティを作成する。 エンティティの詳細については、「 [エンティティ (マスター データ サービス)](../../master-data-services/entities-master-data-services.md)」を参照してください。  
  
-   ドメイン ベースの属性を含む、すべての型の属性を作成する。 属性の詳細については、「 [属性 (マスター データ サービス)](../../master-data-services/attributes-master-data-services.md) 」および「 [ドメインベースの属性 (マスター データ サービス)](../../master-data-services/domain-based-attributes-master-data-services.md)」を参照してください。  
  
 管理者は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたはWeb サービスを使用してモデルを作成する必要があります。 それにより、 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] を使用してモデル内でエンティティや属性を作成できます。 モデル オブジェクトの詳細については、「 [モデル (マスター データ サービス)](../../master-data-services/models-master-data-services.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 ほとんどの管理タスクは、引き続き [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービスを使用して実行する必要があります。 次の表に、管理者が MDS でタスクを完了するために使用できるツールを示します。  
  
|タスクの説明|ツール|トピック|  
|----------------------|----------|-----------|  
|モデルを作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービス|[モデルを作成する (マスター データ サービス)](../../master-data-services/create-a-model-master-data-services.md)|  
|エンティティを作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーション、Web サービス、または [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[エンティティの作成 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|ドメイン ベースの属性を作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーション、Web サービス、または [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[ドメイン ベースの属性の作成 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|属性グループを作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービス|[属性グループを作成する (マスター データ サービス)](../../master-data-services/create-an-attribute-group-master-data-services.md)|  
|ビジネス ルールを作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービス|[ビジネス ルールを作成しパブリッシュする (マスター データ サービス)](../../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|サブスクリプション ビューを作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービス|[サブスクリプション ビューを作成してデータをエクスポートする (マスター データ サービス)](../../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|階層を作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービス|[派生階層を作成する (マスター データ サービス)](../../master-data-services/create-a-derived-hierarchy-master-data-services.md)<br /><br /> [明示的階層を作成する (マスター データ サービス)](../../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|コレクションを作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービス|[コレクションを作成する (マスター データ サービス)](../../master-data-services/create-a-collection-master-data-services.md)|  
|データのバージョンを作成する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションまたは Web サービス|[バージョンをロックする (マスター データ サービス)](../../master-data-services/lock-a-version-master-data-services.md)|  
|モデルを配置する。|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーション、Web サービス、または MDSModelDeploy ツール|[MDSModelDeploy を使用したモデルの配置パッケージの作成](../../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [モデル (マスター データ サービス)](../../master-data-services/models-master-data-services.md)  
  
-   [エンティティ (マスター データ サービス)](../../master-data-services/entities-master-data-services.md)  
  
-   [属性 (マスター データ サービス)](../../master-data-services/attributes-master-data-services.md)  
  
-   [ドメインベースの属性 (マスター データ サービス)](../../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [属性グループ (マスター データ サービス)](../../master-data-services/attribute-groups-master-data-services.md)  
  
-   [ビジネス ルール (マスター データ サービス)](../../master-data-services/business-rules-master-data-services.md)  
  
-   [概要:データのエクスポート (マスター データ サービス)](../../master-data-services/overview-exporting-data-master-data-services.md)  
  
-   [階層 (マスター データ サービス)](../../master-data-services/hierarchies-master-data-services.md)  
  
-   [コレクション (マスター データ サービス)](../../master-data-services/collections-master-data-services.md)  
  
-   [バージョン (マスター データ サービス)](../../master-data-services/versions-master-data-services.md)  
  
-   [セキュリティ (マスター データ サービス)](../../master-data-services/security-master-data-services.md)  
  
-   [モデルの配置 (マスター データ サービス)](../../master-data-services/deploying-models-master-data-services.md)  
  
  
