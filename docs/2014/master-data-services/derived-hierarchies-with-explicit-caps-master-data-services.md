---
title: 明示的なキャップを持つ派生階層 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], derived hierarchies with explicit caps
- explicit hierarchies, derived hierarchies with explicit caps
- derived hierarchies, derived hierarchies with explicit caps
ms.assetid: 6a82ff66-c137-4757-99bb-787d189b4295
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1b444e554fdaa58f8483a339df83bd59f768cef2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483047"
---
# <a name="derived-hierarchies-with-explicit-caps-master-data-services"></a>明示的なキャップを持つ派生階層 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]の、派生階層の最上位レベルとして使用される明示的階層のレベルは、明示的なキャップを持つ派生階層と呼ばれます。  
  
 明示的階層は、派生階層の最上位のエンティティと同じエンティティに基づく必要があります。  
  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のユーザー インターフェイス (UI) で明示的階層を派生階層の最上位にドラッグして、この種類の階層を作成します。  
  
 ![mds_conc_explicit_cap_UI_structure](../../2014/master-data-services/media/mds-conc-explicit-cap-ui-structure.gif "mds_conc_explicit_cap_UI_structure")  
  
## <a name="derived-hierarchy-with-explicit-cap-example"></a>明示的なキャップを持つ派生階層の例  
 この例では、明示的階層のメンバーは Subcategory エンティティのメンバーです。 派生階層の最上位レベルのメンバーも Subcategory エンティティのメンバーです。  
  
 ![mds_conc_explicit_cap_UI_example](../../2014/master-data-services/media/mds-conc-explicit-cap-ui-example.gif "mds_conc_explicit_cap_UI_example")  
  
 明示的階層を派生階層の最上位で使用することにより、派生階層は不規則になります。  
  
## <a name="rules"></a>ルール  
  
-   明示的キャップを持つ 1 つの派生階層に設定できる明示的階層は 1 つだけです。  
  
-   同じ明示的階層を複数の派生階層のキャップとして使用できます。  
  
-   明示的なキャップを持つ派生階層に階層メンバーの権限を割り当てることはできません。 権限を明示的階層または派生階層に個々に割り当てた場合、権限は両方の階層に影響します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|派生階層を作成する。|[派生階層を作成する (マスター データ サービス)](create-a-derived-hierarchy-master-data-services.md)|  
|明示的階層を作成する。|[明示的階層を作成する (マスター データ サービス)](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|既存の派生階層を削除する。|[派生階層を削除する (マスター データ サービス)](../../2014/master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
|||  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [派生階層 (マスター データ サービス)](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [明示的階層 (マスター データ サービス)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
