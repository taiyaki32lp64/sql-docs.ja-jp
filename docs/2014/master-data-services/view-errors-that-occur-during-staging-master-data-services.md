---
title: ステージング処理 (マスター データ サービス) の中に発生したエラーの表示 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 75b7fb5a1b98f599a07e47101f93268779ca39b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478567"
---
# <a name="view-errors-that-occur-during-the-staging-process-master-data-services"></a>ステージング処理中に発生したエラーの表示 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、ステージング処理中に発生したエラーを表示できます。 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースには、エラーを表示する 2 つのビューがあります。  
  
-   stg.viw_name_MemberErrorDetails (リーフ メンバーまたは統合メンバーの更新用)。  
  
-   stg.viw_name_RelationshipErrorDetails (階層のリレーションシップの更新用)。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースでは、stg.viw_name_MemberErrorDetails ビューまたは stg.viw_name_RelationshipErrorDetails ビューのどちらかに対する SELECT 権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
### <a name="to-view-staging-errors"></a>ステージング エラーを表示するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssDE](../includes/ssde-md.md)] データベースの [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンスに接続します。  
  
2.  新しいクエリを開きます。  
  
3.  名前を viw_Product_MemberErrorDetails などのステージング テーブルの名前に置き換えて、次のテキストを入力します。  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  クエリを実行します。 エラーの詳細が **ErrorDescription** フィールドに表示されます。  
  
## <a name="next-steps"></a>次の手順  
 エラー メッセージの詳細については、「[ステージング処理のエラー (マスター データ サービス)](../../2014/master-data-services/staging-process-errors-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データのインポート&#40;マスター データ サービス&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [ステージング処理のトラブルシューティング (マスター データ サービス)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
