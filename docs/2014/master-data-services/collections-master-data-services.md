---
title: コレクション (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0dbf84d6fd3253a3b4d945693090fdad00d077ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483543"
---
# <a name="collections-master-data-services"></a>コレクション (Master Data Services)
  コレクションは、1 つのエンティティのリーフ メンバーと統合メンバーのグループです。 コレクションは、完全な階層を必要としない場合で、レポートまたは分析のためにメンバーのさまざまなグループを表示するとき、または分類を作成する必要があるときに使用します。  
  
## <a name="what-collections-contain"></a>コレクションに含められるもの  
 コレクションは、メンバーが同じエンティティ内に存在する限り、含めることができるメンバーの数または種類が制限されません。 コレクションには、複数の必須および任意の明示的階層に属するリーフ メンバーと統合メンバーを含めることができます。  
  
 コレクションを作成しても、階層構造は作成されません。作成されるのはメンバーのフラット リストです。 階層からノードを選択し、コレクションに追加すると、選択した統合メンバーだけがコレクションに追加されます。  
  
 コレクションに他のコレクションを含めることもできます。 コレクションのコレクションを使用して、分類を作成できます。  
  
 コレクションを作成すると、作成者は所有者として自動的に一覧に表示されます。 管理者の場合は、必要に応じて、コレクションの他の属性を作成できます。  
  
> [!NOTE]  
>  コレクションを作成するには、明示的階層でエンティティを有効にしておく必要があります。 詳細については、次を参照してください。[明示的階層およびコレクションに対してエンティティを有効にする&#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)します。  
  
## <a name="subscription-views-for-collections"></a>コレクションのサブスクリプション ビュー  
 コレクションを表示するサブスクリプション ビューには 2 つの種類があります。 **コレクション属性** 形式では、コレクションのリストと、コレクションに関係のある属性 (説明や所有者など) の一覧が表示されます。 **コレクション** 形式では、すべてのコレクション内のすべてのメンバーと、各メンバーの重みおよび並べ替え順序が表示されます。 詳細については、次を参照してください。[データのエクスポート&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)します。  
  
 コレクションで特定のメンバーに重みの値を設定した場合、関連するサブスクリプション ビューでその値を使用できます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|明示的階層とコレクションに対してエンティティを有効にする。|[明示的階層およびコレクションに対してエンティティを有効にする&#40;マスター データ サービス&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)|  
|新しいコレクションを作成する。|[コレクションを作成する (マスター データ サービス)](../../2014/master-data-services/create-a-collection-master-data-services.md)|  
|既存のコレクションにメンバーを追加する。|[コレクションにメンバーを追加する (マスター データ サービス)](../../2014/master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [明示的階層 (マスター データ サービス)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [データのエクスポート&#40;マスター データ サービス&#41;](overview-exporting-data-master-data-services.md)  
  
  
