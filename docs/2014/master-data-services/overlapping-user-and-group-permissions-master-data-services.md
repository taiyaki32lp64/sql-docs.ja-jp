---
title: ユーザー アクセス許可とグループ アクセス許可の重複 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- users [Master Data Services], resolving permissions
- permissions [Master Data Services], user and group overlaps
- groups [Master Data Services], resolving permissions
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6c3bdb745d836959f563d19dc9897b718a2c9b16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478882"
---
# <a name="overlapping-user-and-group-permissions-master-data-services"></a>ユーザー権限とグループ権限の重複 (Master Data Services)
  ユーザーの権限は、次の権限に基づきます。  
  
-   グループのメンバーシップの権限  
  
-   ユーザーに明示的に割り当てられた権限  
  
 ユーザーが複数のグループのメンバーであり、それらのグループがマスター データ マネージャーへのアクセス権を持っている場合、次の規則が適用されます。  
  
-   **拒否** が他のどの権限をオーバーライドします。  
  
-   **Update**オーバーライド**読み取り専用**します。  
  
 上記のルールは、 **[モデル]** タブと **[階層メンバー]** タブに適用されます。 権限は、各タブで解決された後で組み合わされます。 詳細については、「[権限の決定方法 (マスター データ サービス)](how-permissions-are-determined-master-data-services.md)」を参照してください。  
  
> [!NOTE]  
>  ユーザー権限とグループ権限の重複がどのように解決されているかは、ユーザー インターフェイスに表示できます。 **[モデル]** タブと **[階層メンバー]** タブにはドロップダウン リストがあり、そこから **[有効]** をクリックして有効な権限を表示できます。  
  
## <a name="example-1"></a>例 1  
 ![mds_conc_user_group_ex_1](../../2014/master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 ユーザーがグループ 1 とグループ 2 に属しています。  
  
 ユーザーが**読み取り専用**Product エンティティにアクセスを許可します。  
  
 グループ 1 には、Product エンティティに対する **更新** 権限が与えられています。  
  
 グループ 2 に**読み取り専用**Product エンティティにアクセスを許可します。  
  
 結果:ユーザーの有効な権限は、Product エンティティに対する **更新** 権限となります。  
  
## <a name="example-2"></a>例 2  
 ![mds_conc_user_group_ex_2](../../2014/master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 ユーザーがグループ 1 とグループ 2 に属しています。  
  
 ユーザーが**読み取り専用**Product エンティティにアクセスを許可します。  
  
 グループ 1 には、Product エンティティに対する **更新** 権限が与えられています。  
  
 グループ 2 には、Product エンティティに対する **拒否** 権限が与えられています。  
  
 結果:ユーザーの有効な権限は、Product エンティティに対する **拒否** 権限となります。  
  
## <a name="example-3"></a>例 3  
 ![mds_conc_user_group_ex_3](../../2014/master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 ユーザーがグループ 1 とグループ 2 に属しています。  
  
 ユーザーには、階層ノードのメンバーのグループに対する **更新** 権限が与えられています。  
  
 グループ 1 には**読み取り専用**階層ノードのメンバーのグループにアクセスを許可します。  
  
 グループ 2 に**読み取り専用**階層ノードのメンバーのグループにアクセスを許可します。  
  
 結果:ユーザーの有効な権限は、メンバーに対する **更新** 権限となります。  
  
## <a name="see-also"></a>関連項目  
 [権限の決定方法 (マスター データ サービス)](how-permissions-are-determined-master-data-services.md)   
 [モデル権限とメンバー権限の重複 (マスター データ サービス)](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  
