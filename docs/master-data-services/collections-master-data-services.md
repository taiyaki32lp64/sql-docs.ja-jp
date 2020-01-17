---
title: コレクション
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 19a9d925b07b83e5ed26b73484cea955773364c6
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728606"
---
# <a name="collections-master-data-services"></a>コレクション (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  コレクションは、1 つのエンティティのリーフ メンバーと統合メンバーのグループです。 コレクションは、完全な階層を必要としない場合で、レポートまたは分析のためにメンバーのさまざまなグループを表示するとき、または分類を作成する必要があるときに使用します。  
  
> [!NOTE]  
>  コレクションの使用は非推奨とされます。  
  
## <a name="what-collections-contain"></a>コレクションに含められるもの  
 コレクションは、メンバーが同じエンティティ内に存在する限り、含めることができるメンバーの数または種類が制限されません。 コレクションには、複数の必須および任意の明示的階層に属するリーフ メンバーと統合メンバーを含めることができます。  
  
 コレクションを作成しても、階層構造は作成されません。作成されるのはメンバーのフラット リストです。 階層からノードを選択し、コレクションに追加すると、選択した統合メンバーだけがコレクションに追加されます。  
  
 コレクションに他のコレクションを含めることもできます。 コレクションのコレクションを使用して、分類を作成できます。  
  
 コレクションを作成すると、作成者は所有者として自動的に一覧に表示されます。 管理者の場合は、必要に応じて、コレクションの他の属性を作成できます。  
  
## <a name="subscription-views-for-collections"></a>コレクションのサブスクリプション ビュー  
 コレクションを表示するサブスクリプション ビューには 2 つの種類があります。 **コレクション属性** 形式では、コレクションのリストと、コレクションに関係のある属性 (説明や所有者など) の一覧が表示されます。 **コレクション** 形式では、すべてのコレクション内のすべてのメンバーと、各メンバーの重みおよび並べ替え順序が表示されます。 詳細については、「[概要: データのエクスポート (マスター データ サービス)](../master-data-services/overview-exporting-data-master-data-services.md)」を参照してください。  
  
 コレクションで特定のメンバーに重みの値を設定した場合、関連するサブスクリプション ビューでその値を使用できます。  
  
## <a name="related-tasks"></a>関連タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|新しいコレクションを作成する。|[コレクションを作成する (マスター データ サービス)](../master-data-services/create-a-collection-master-data-services.md)|  
|既存のコレクションにメンバーを追加する。|[コレクションにメンバーを追加する (マスター データ サービス)](../master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [明示的階層 (マスター データ サービス)](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [概要: データのエクスポート (マスター データ サービス)](../master-data-services/overview-exporting-data-master-data-services.md)  
  
  
