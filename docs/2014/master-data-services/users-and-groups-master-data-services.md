---
title: ユーザーおよびグループ (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 58373531871a5db8ff859280de52cbe21562bfb5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478627"
---
# <a name="users-and-groups-master-data-services"></a>ユーザーおよびグループ (Master Data Services)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションにアクセスするには、Windows ドメイン アカウント、または [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] がインストールされているサーバー コンピューター上のアカウントがユーザーに必要です。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] へのアクセスを許可するには、次のいずれかを実行します。  
  
-   ユーザー アカウントをドメインまたはローカル グループに追加するか、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]でグループの一覧にグループを追加します。  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]でユーザーの一覧にユーザー アカウントを追加します。  
  
    > [!NOTE]  
    >  ユーザーが [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]へのアクセス権があるグループに所属している場合、そのユーザーが初めて [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] または MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]にアクセスすると、そのユーザーの一覧にユーザー名が自動的に追加されます。  
  
 UI の **[エクスプローラー]** 機能領域で操作を実行するには、グループまたはユーザーに **[エクスプローラー]** 機能領域へのアクセス権、およびモデル オブジェクトへの権限が割り当てられている必要があります。  
  
 ユーザーまたはグループにその他の機能領域へのアクセス権が必要な場合、そのユーザーまたはグループは管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
## <a name="best-practice"></a>推奨事項  
 管理を簡素化するには、グループを作成し、各グループに機能領域およびモデル オブジェクトへの権限を割り当てます。 また、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] の UI にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
 個々のユーザーに追加の権限を割り当てたり、ユーザーを [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]にアクセスできる複数のグループに含めたりしないでください。 また、特定のメンバーに対するグループのアクセスを制限する必要がない限り、階層メンバーの権限は使用しないでください。  
  
## <a name="see-also"></a>参照  
 [ユーザーを追加する (マスター データ サービス)](../../2014/master-data-services/add-a-user-master-data-services.md)   
 [グループを追加する (マスター データ サービス)](../../2014/master-data-services/add-a-group-master-data-services.md)   
 [ユーザーまたはグループを削除する (マスター データ サービス)](../../2014/master-data-services/delete-users-or-groups-master-data-services.md)   
 [ユーザーのアクセス許可のテスト (マスター データ サービス)](../../2014/master-data-services/test-a-user-s-permissions-master-data-services.md)  
  
  
