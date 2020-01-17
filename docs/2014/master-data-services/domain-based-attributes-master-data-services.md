---
title: ドメインベースの属性 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], about domain-based attributes
- domain-based attributes [Master Data Services]
- attributes [Master Data Services], domain-based attributes
ms.assetid: df6f33ff-97f6-466c-af74-9780b2247473
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 52c15f1b41e6e1a970ad07a8779e5ed810c4a50b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483862"
---
# <a name="domain-based-attributes-master-data-services"></a>ドメインベースの属性 (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でのドメイン ベースの属性とは、別のエンティティからのメンバーによって値が設定される属性です。 ドメイン ベースの属性によって、ユーザーが無効な属性値を入力することを防止できることから、ドメイン ベースの属性は制約リストと考えることもできます。 属性値を選択するには、ユーザーは一覧から選択する必要があります。  
  
## <a name="domain-based-attribute-example"></a>ドメイン ベースの属性の例  
 次の図では、Product エンティティに Subcategory というドメイン ベースの属性があります。 Subcategory 属性は Subcategory エンティティの値によって設定されます。  
  
 Subcategory エンティティには Category というドメイン ベースの属性があります。 Category 属性は Category エンティティの値によって設定されます。  
  
 ![エンティティ内のドメイン ベースの属性](../../2014/master-data-services/media/mds-conc-domain-based-attribute-conceptual.gif "エンティティ内のドメイン ベースの属性")  
  
## <a name="use-same-entity-for-multiple-domain-based-attributes"></a>複数のドメイン ベースの属性に同じエンティティを使用する  
 複数のエンティティのドメイン ベースの属性として同じエンティティを使用できます。 たとえば、Yes、No、Maybe というメンバーを持つ YesNoIndicator という名前のエンティティを作成できます。 InStock というドメイン ベースの属性を作成して、YesNoIndicator エンティティをソースとして使用できます。 また、Approved という別のドメイン ベースの属性を作成し、YesNoIndicator エンティティをソースとして使用することもできます。 YesNoIndicator エンティティのメンバーのリストからユーザーによる選択を行う場合は、エンティティをドメイン ベースの属性として使用できます。  
  
## <a name="domain-based-attributes-form-derived-hierarchies"></a>ドメイン ベースの属性による派生階層の形成  
 ドメイン ベースの属性のリレーションシップは、派生階層の基盤となります。 詳細については、「[派生階層 (マスター データ サービス)](derived-hierarchies-master-data-services.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|既存のエンティティを元にして新しいドメインベースの属性を作成する。|[ドメイン ベースの属性を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|新規エンティティを作成する。|[エンティティを作成する (マスター データ サービス)](../../2014/master-data-services/create-an-entity-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [派生階層 (マスター データ サービス)](derived-hierarchies-master-data-services.md)  
  
-   [属性 (マスター データ サービス)](../../2014/master-data-services/attributes-master-data-services.md)  
  
-   [エンティティ (マスター データ サービス)](../../2014/master-data-services/entities-master-data-services.md)  
  
  
