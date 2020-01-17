---
title: システム管理者アカウント (マスター データ サービス) の変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 911bd20c7d232bca52fdf9dca294bd7a4924d984
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054134"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>システム管理者アカウントの変更 (マスター データ サービス)
  として指定されているユーザー アカウントを変更することができます、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]システム管理者です。  
  
> [!WARNING]  
>  この手順が完了すると、前のシステム管理者のユーザー アカウントは削除されます。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   新しい管理者のユーザー名を[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]のユーザーの一覧に追加する必要があります。 詳細については、次を参照してください。[ユーザーを追加&#40;Master Data Services&#41;](add-a-user-master-data-services.md)します。  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースで mdm.tblUser を表示して mdm.udpSecurityMemberProcessRebuildModel ストアド プロシージャを実行するための権限が必要です。 詳細については、「[データベース オブジェクト セキュリティ (マスター データ サービス)](../../2014/master-data-services/database-object-security-master-data-services.md)」を参照してください。  
  
### <a name="to-change-the-administrator-account"></a>管理者アカウントを変更するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssDE](../includes/ssde-md.md)] データベースの [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンスに接続します。  
  
2.  Mdm.tbluser で、新しい管理者である値をコピーしたユーザーを検索、`SID`列。  
  
3.  新しいクエリを作成します。  
  
4.  次のテキスト入力交換*domain \user_name*を新しい管理者のユーザー名と*SID*手順 2. でコピーした値を持つ。  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  クエリを実行します。  
  
## <a name="see-also"></a>参照  
 [管理者 (マスター データ サービス)](../../2014/master-data-services/administrators-master-data-services.md)  
  
  
