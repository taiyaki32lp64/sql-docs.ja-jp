---
title: モデル アクセス許可 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 733827ecace64ef86b54831f63fd8c2889203919
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478963"
---
# <a name="model-permissions-master-data-services"></a>モデル権限 (Master Data Services)
  モデル権限は、モデル内に存在するすべてのエンティティ、派生階層、明示的階層、およびコレクションに適用されます。 モデルに割り当てられる権限は、個々のオブジェクトでオーバーライドすることができます。  
  
> [!NOTE]  
>  ユーザーがモデル管理者の場合、そのモデルはユーザー インターフェイスのすべての機能領域に表示されます。 それ以外の場合、モデルは **[エクスプローラー]** 機能領域にのみ表示されます。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
|権限|説明|  
|----------------|-----------------|  
|**読み取り専用です。**|**エクスプ ローラー**モデルが表示されますが、ユーザーを追加できません、またはメンバーの削除、および属性値、階層メンバーシップ、またはコレクションのメンバーシップを更新することはできません。|  
|**Update**|**エクスプ ローラー**モデルを表示、およびユーザーが追加され、メンバーの削除、属性値、階層メンバーシップ、およびコレクションのメンバーシップを更新します。|  
|**Deny**|モデルが表示されません。|  
  
 モデルに権限を割り当てると、ユーザーはすべてのバージョンのモデルにアクセスできるようになります。 個々のバージョンに権限を割り当てることはできません。  
  
## <a name="see-also"></a>参照  
 [モデル オブジェクト権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [モデル オブジェクト権限 (マスター データ サービス)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [エンティティ権限 (マスター データ サービス)](../../2014/master-data-services/entity-permissions-master-data-services.md)   
 [コレクション アクセス許可 (マスター データ サービス)](../../2014/master-data-services/collection-permissions-master-data-services.md)  
  
  
