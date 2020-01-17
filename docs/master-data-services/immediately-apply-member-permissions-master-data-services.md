---
title: メンバー権限を直ちに適用する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], applying permissions immediately
- permissions [Master Data Services], applying member permissions immediately
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 82ad2fad9645d3d8277abac6328d23c7b18a0c94
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729218"
---
# <a name="immediately-apply-member-permissions-master-data-services"></a>メンバー権限を直ちに適用する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で、メンバー セキュリティが定期的に適用されるのを待つ代わりに、メンバー権限を直ちに適用できます。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースで mdm.udpSecurityMemberProcessRebuildModel ストアド プロシージャを実行するための権限が必要です。 詳細については、「[データベース オブジェクト セキュリティ (マスター データ サービス)](../master-data-services/database-object-security-master-data-services.md)」を参照してください。  
  
### <a name="to-immediately-apply-hierarchy-member-permissions"></a>階層メンバーの権限を直ちに適用するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssDE](../includes/ssde-md.md)] データベースの [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンスに接続します。  
  
2.  新しいクエリを作成します。  
  
3.  次のテキストを入力します。その場合、 *database* をデータベースの名前で置き換え、 *Model_Name* をモデルの名前で置き換えます。  
  
    ```  
    USE [database];  
    GO  
  
    DECLARE @Model_ID INT;  
    SELECT @Model_ID = ID FROM mdm.tblModel WHERE [Name] = N'Model_Name';  
    EXEC [mdm].[udpSecurityMemberProcessRebuildModel] @Model_ID=@Model_ID, @ProcessNow=1;  
    GO  
    ```  
  
4.  クエリを実行します。  
  
## <a name="see-also"></a>参照  
 [階層メンバーの権限を割り当てる (マスター データ サービス)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [階層メンバーの権限 (マスター データ サービス)](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
