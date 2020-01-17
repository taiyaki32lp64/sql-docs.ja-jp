---
title: ユーザーおよびグループ (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- users [Master Data Services]
- groups [Master Data Services]
- users [Master Data Services], about users
- groups [Master Data Services], about groups
ms.assetid: ed08dd2d-248e-4b68-91d4-e9961cb50eed
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f52031d8dead33601dd9f60e5475da53b0b9c9d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102580"
---
# <a name="users-and-groups-master-data-services"></a>ユーザーおよびグループ (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションにアクセスするには、Windows ドメイン アカウント、または [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] がインストールされているサーバー コンピューター上のアカウントがユーザーに必要です。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] へのアクセスを許可するには、次のいずれかを実行します。  
  
-   ユーザー アカウントをドメインまたはローカル グループに追加するか、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]でグループの一覧にグループを追加します。  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]でユーザーの一覧にユーザー アカウントを追加します。  
  
    > [!NOTE]  
    >  ユーザーが [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]へのアクセス権があるグループに所属している場合、そのユーザーが初めて [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] または MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]にアクセスすると、そのユーザーの一覧にユーザー名が自動的に追加されます。  
  
 UI の **[エクスプローラー]** 機能領域で操作を実行するには、グループまたはユーザーに **[エクスプローラー]** 機能領域へのアクセス権、およびモデル オブジェクトへの権限が割り当てられている必要があります。  
  
 ユーザーまたはグループにその他の機能領域へのアクセス権が必要な場合、そのユーザーまたはグループには特定の機能領域へのアクセス権が割り当てられる必要があります。  
  
## <a name="best-practice"></a>推奨事項  
 管理を簡素化するには、グループを作成し、各グループに機能領域およびモデル オブジェクトへの権限を割り当てます。 また、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] の UI にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
 個々のユーザーに追加の権限を割り当てたり、ユーザーを [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]にアクセスできる複数のグループに含めたりしないでください。 また、特定のメンバーに対するグループのアクセスを制限する必要がない限り、階層メンバーの権限は使用しないでください。  
  
## <a name="see-also"></a>関連項目  
 [ユーザーを追加する (マスター データ サービス)](../master-data-services/add-a-user-master-data-services.md)   
 [グループを追加する (マスター データ サービス)](../master-data-services/add-a-group-master-data-services.md)   
 [ユーザーまたはグループを削除する (マスター データ サービス)](../master-data-services/delete-users-or-groups-master-data-services.md)   
 [ユーザーのアクセス許可のテスト (マスター データ サービス)](../master-data-services/test-a-user-s-permissions-master-data-services.md)  
  
  
