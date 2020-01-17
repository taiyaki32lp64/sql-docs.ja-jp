---
title: データのエクスポート (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f92a74caa74c5cf15e917cd6c15aef9506a60180
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482840"
---
# <a name="exporting-data-master-data-services"></a>データのエクスポート (Master Data Services)
  サブスクリプション ビューを作成して、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データをサブスクライブ システムにエクスポートできます。 これにより、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースにパブリッシュされたデータを任意のサブスクライブ システムで表示できます。 ビューの詳細については、「 [ビュー](../relational-databases/views/views.md)」を参照してください。  
  
## <a name="subscription-view-formats"></a>サブスクリプション ビュー形式  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]でビューを作成する場合は、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] によって提供される一連の標準ビュー形式から選択します。 これらの形式を使用して、以下を表示するビューを作成できます。  
  
-   すべてのリーフ メンバーとその属性  
  
-   すべての統合メンバーとその属性  
  
-   すべてのコレクションとその属性  
  
-   コレクションに明示的に追加されたメンバー  
  
-   親子形式またはレベル形式の派生階層内のメンバー  
  
-   エンティティのすべての明示的階層内のメンバー (親子形式またはレベル形式)  
  
## <a name="subscription-views-can-become-out-of-date"></a>サブスクリプション ビューが古くなる可能性  
 エンティティまたは階層のサブスクリプション ビューを作成後、関連付けられたモデル オブジェクトへの変更が自動的にビューに反映されるわけではありません。 モデル オブジェクトに対する変更を反映するには、必要に応じて [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] でサブスクリプション ビューを再生成する必要があります。 モデル オブジェクトが変更されると、 **[エクスポート]** ページの **[変更]** 列が **[True]** に更新されます。 **[True]** は、サブスクリプション ビューを編集して保存する必要があることを示します。この操作により、ビューが再生成されます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|マスター データのサブスクリプション ビューを作成する。|[サブスクリプション ビューを作成&#40;マスター データ サービス&#41;](create-a-subscription-view-to-export-data-master-data-services.md)|  
|既存のサブスクリプション ビューを削除する。|[サブスクリプション ビューを削除する (マスター データ サービス)](../../2014/master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [サブスクリプション ビュー形式 (マスター データ サービス)](../../2014/master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [ビュー](../relational-databases/views/views.md)  
  
  
