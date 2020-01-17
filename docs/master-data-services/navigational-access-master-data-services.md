---
title: ナビゲーション アクセス
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- navigational access [Master Data Services]
- security [Master Data Services], navigational access
ms.assetid: 3403b7b0-44e2-48c3-a1b7-9c4612b874b8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c167d33c29a78100e5a0f1bfcd987dc50368cdc4
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728996"
---
# <a name="navigational-access-master-data-services"></a>ナビゲーション アクセス (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  ナビゲーション アクセスは、 **[モデル]** タブで割り当てられるモデル オブジェクト セキュリティに適用されます。  
  
 ナビゲーション アクセスは、セキュリティを割り当てたレベルよりも高いレベルへのアクセスです。  
  
 この例では、権限がエンティティに割り当てられているため、ナビゲーション アクセスがモデル レベルで付与されます。  
  
 ![mds_conc_inheritance_model](../master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **エンティティ**  
  
 エンティティ、リーフ メンバー、またはその統合メンバーに権限を割り当てた場合、ナビゲーション アクセスにより、すべてのメンバーの名前およびコードの読み取りまたは更新を実行できます。 また、モデル名を読み取ることもできます。  
  
 **属性**  
  
 属性に権限を割り当てた場合、ナビゲーション アクセスにより、エンティティのすべてのメンバーの名前およびコードの読み取りまたは更新を実行できます。 また、モデル名を読み取ることもできます。  
  
 **コレクション**  
  
 コレクションに権限を割り当てた場合、名前、コード、説明、および所有者 ID の読み取りまたは更新を実行できます。 また、モデル名を読み取ることもできます。  
  
## <a name="see-also"></a>参照  
 [権限の決定方法 (マスター データ サービス)](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
