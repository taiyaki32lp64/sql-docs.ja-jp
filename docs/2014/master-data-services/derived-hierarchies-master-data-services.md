---
title: 派生階層 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies
- hierarchies [Master Data Services], derived hierarchies
- derived hierarchies, about derived hierarchies
ms.assetid: a0fbd519-a10e-4cbd-92e6-5de9b8d3e3f0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: af5bbc51420d8f32144bc91f687ae58b86d10d52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479418"
---
# <a name="derived-hierarchies-master-data-services"></a>派生階層 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] の派生階層は、モデル内のエンティティ間に既に存在するドメインベースの属性のリレーションシップから派生します。  
  
 派生階層を作成することで、モデル内の既存のドメイン ベースの属性リレーションシップを強調表示できます。  
  
## <a name="leaf-members-group-other-leaf-members"></a>他のリーフ メンバーをグループ化するリーフメンバー  
 派生階層では、1 つのエンティティのリーフ メンバーを使用して別のエンティティのリーフ メンバーをグループ化します。 派生階層は、これらのエンティティの間のリレーションシップに基づいています。 これに対し、明示的階層は単一エンティティのメンバーに基づき、指定した任意の方法で構造化されます。  
  
 派生階層の構造は、基になるデータに影響を与えることなく変更できます。 モデル内にリレーションシップが存在している限り、派生階層を削除してもマスター データには影響しません。  
  
## <a name="explicit-hierarchies-versus-derived-hierarchies"></a>明示的階層と派生階層  
 次の表は、明示的階層と派生階層の相違点の一部を示しています。  
  
|明示的階層|派生階層|  
|--------------------------|-------------------------|  
|構造はユーザーによって定義される|構造はドメイン ベースの属性間のリレーションシップから派生する|  
|単一のエンティティからのメンバーを含む|複数のエンティティからのメンバーを含む|  
|他のメンバーをグループ化する統合メンバーを使用する|1 つのエンティティのリーフ メンバーを使用して、別のエンティティのリーフ メンバーをグループ化する|  
|不規則になる場合がある|常に一定のレベル数を含む|  
  
## <a name="creating-a-variable-depth-hierarchy"></a>変数の深さ階層の作成  
 変数の深さ階層の作成方法として、次の 2 種類の方法をお勧めします。  
  
-   すべてのレベルの属性を同じにする場合は、単一のエンティティを作成してから、エンティティに基づくドメイン ベースの属性を使用してそのエンティティの再帰型階層を作成します。  
  
-   リーフ メンバーに 1 セットの属性が必要で、上位レベルにはもう 1 セット属性が必要な場合は、派生階層に 2 つのエンティティを作成します。 リーフ エンティティに対しては、親エンティティに基づくドメイン ベースの属性を使用します。 親エンティティに対しては、親エンティティ自体に基づくドメイン ベースの属性を使用します。  
  
## <a name="derived-hierarchy-example"></a>派生階層の例  
 次の例では、Product エンティティのリーフ メンバーは Subcategory エンティティのリーフ メンバーによってグループ化されています。Subcategory エンティティは、Category エンティティのリーフ メンバーによってグループ化されています。 Product エンティティには Subcategory というドメイン ベースの属性があり、Subcategory エンティティには Category というドメイン ベースの属性があるので、この階層は有効です。  
  
 階層構造は、メンバーがグループ化されている方法を示します。 ほとんどのメンバーを持つエンティティは一番下に位置します。  
  
 ![モデル構造体から派生した階層](../../2014/master-data-services/media/mds-conc-derived-hierarchy-structure.gif "モデル構造から派生した階層")  
  
 派生階層では、Product と Subcategory 間のリレーションシップを強調表示してから、Subcategory と Category 間のリレーションシップを強調表示できます。 この階層内にメンバーを表示すると、ツリー内の各レベルに同じエンティティのメンバーが含まれています。  
  
 ![マウンテン バイク派生階層の例](../../2014/master-data-services/media/mds-conc-derived-hierarchy-example.gif "マウンテン バイク派生階層の例")  
  
 この種類の階層では、無効なレベルにメンバーを移動できません。 たとえば、自転車 Road-650 は、Road Bikes というサブカテゴリから Mountain Bikes という別のサブカテゴリに移動することはできますが、 1 {Bikes} などのカテゴリの直下に移動することはできません。 階層ツリー内でメンバーを移動するたびに、メンバーのドメイン ベースの属性値は、移動を反映して変更されます。  
  
## <a name="notes"></a>メモ  
 派生階層ツリー内のすべてのメンバーは、コードによって並べ替えられます。 並べ替え順序は変更できません。  
  
 メンバーのドメイン ベースの属性が空で、その属性が派生階層で使用される場合、そのメンバーは階層内に表示されません。 属性への値の設定を要求するビジネス ルールを作成してください。 詳細については、「[属性値を要求する &#40;マスター データ サービス&#41;](require-attribute-values-master-data-services.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|新しい派生階層を作成する。|[派生階層を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|既存の派生階層のレベルを非表示にするか、または削除する。|[派生階層のレベルを非表示にするか削除する (マスター データ サービス)](../../2014/master-data-services/hide-or-delete-levels-in-a-derived-hierarchy-master-data-services.md)|  
|既存の派生階層の名前を変更する。|[派生階層名を変更する (マスター データ サービス)](../../2014/master-data-services/change-a-derived-hierarchy-name-master-data-services.md)|  
|既存の派生階層を削除する。|[派生階層を削除する (マスター データ サービス)](../../2014/master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
|||  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [ドメインベースの属性 (マスター データ サービス)](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [明示的階層 (マスター データ サービス)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [再帰型階層 (マスター データ サービス)](../../2014/master-data-services/recursive-hierarchies-master-data-services.md)  
  
-   [明示的なキャップを持つ派生階層 (マスター データ サービス)](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)  
  
-   [コレクション (マスター データ サービス)](../../2014/master-data-services/collections-master-data-services.md)  
  
  
