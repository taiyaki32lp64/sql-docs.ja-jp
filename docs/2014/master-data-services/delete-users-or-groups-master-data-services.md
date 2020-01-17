---
title: ユーザーまたはグループを削除する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0114aa3ca6f6744303c3053003a622185d33f547
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479902"
---
# <a name="delete-users-or-groups-master-data-services"></a>ユーザーまたはグループを削除する (マスター データ サービス)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]にアクセスする必要のなくなったユーザーまたはグループを削除します。  
  
 ユーザーおよびグループを削除する場合、次の点に注意してください。  
  
-   ユーザーが [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]へのアクセスを持つグループのメンバーである場合、そのユーザーは、Active Directory またはローカル グループから削除されるまで [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] にアクセスできます。  
  
-   グループを削除した場合、そのメンバーを削除するまで、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] にアクセスしたことのあるグループのすべてのメンバーは **[ユーザー]** ボックスの一覧に表示されます。  
  
-   セキュリティの変更は、20 分間は MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] に反映されません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[ユーザー/グループの権限]** 機能領域にアクセスするための権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
### <a name="to-delete-users-or-groups"></a>ユーザーまたはグループを削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[ユーザー/グループの権限]** をクリックします。  
  
2.  ユーザーを削除するには、 **[ユーザー]** ページを表示します。 グループを削除するには、メニュー バーの **[グループの管理]** をクリックします。  
  
3.  グリッドで、削除するユーザーまたはグループの行を選択します。  
  
4.  **[選択したユーザーの削除]** または **[選択したグループの削除]** をクリックします。  
  
5.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ (マスター データ サービス)](../../2014/master-data-services/security-master-data-services.md)  
  
  
