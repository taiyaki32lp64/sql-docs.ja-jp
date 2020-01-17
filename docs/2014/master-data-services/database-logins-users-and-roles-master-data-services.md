---
title: データベース ログイン、ユーザー、およびロール (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], database roles
- database [Master Data Services], users
- security [Master Data Services], database users
- database [Master Data Services], roles
- database [Master Data Services], logins
- security [Master Data Services], database logins
ms.assetid: 72ee383e-a619-461b-9f9d-1cac162ab0c5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e9352910554e5f946f21eae3b51a7d87ff1106bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479754"
---
# <a name="database-logins-users-and-roles-master-data-services"></a>データベース ログイン、ユーザー、およびロール (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] には、 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] データベースをホストする [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンスに自動的にインストールされるログイン、ユーザー、およびロールがあります。 これらのログイン、ユーザー、およびロールは変更しないでください。  
  
## <a name="logins"></a>Login  
  
|Login|説明|  
|-----------|-----------------|  
|`mds_dlp_login`|UNSAFE アセンブリを作成できます。<br /><br /> \- ランダムに生成されたパスワードでのログインは無効です。<br /><br /> \- [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの場合は、dbo にマップされます。<br /><br /> \- msdb の場合は、mds_clr_user がこのログインにマップされます。<br /><br /> <br /><br /> 詳細については、「 [アセンブリの作成](../relational-databases/clr-integration/assemblies/creating-an-assembly.md)」を参照してください。|  
|`mds_email_login`|通知に使用されるログインは有効です。<br /><br /> msdb および [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの場合は、mds_email_user がこのログインにマップされます。|  
  
## <a name="msdb-users"></a>msdb ユーザー  
  
|ユーザー|説明|  
|----------|-----------------|  
|`mds_clr_user`|使用されていません。<br /><br /> mds_dlp_login にマップされます。|  
|`mds_email_user`|通知に使用します。<br /><br /> mds_email_login にマップされます。<br /><br /> ロールのメンバーを示します。ロールのメンバーです。|  
  
## <a name="master-data-services-database-users"></a>マスター データ サービス データベース ユーザー  
  
|ユーザー|説明|  
|----------|-----------------|  
|`mds_email_user`|通知に使用します。<br /><br /> mdm スキーマに対する SELECT 権限があります。<br /><br /> mdm.MemberGetCriteria ユーザー定義テーブル型に対する EXECUTE 権限があります。<br /><br /> mdm.udpNotificationQueueActivate ストアド プロシージャに対する EXECUTE 権限があります。|  
|**mds_schema_user**|mdm スキーマと mdq スキーマを所有します。 既定のスキーマは mdm です。<br /><br /> ログインはマップされません。|  
|**mds_ssb_user**|Service Broker タスクを実行するために使用します。<br /><br /> すべてのスキーマに対する DELETE、INSERT、REFERENCES、SELECT、および UPDATE 権限があります。<br /><br /> ログインはマップされません。|  
  
## <a name="master-data-services-database-role"></a>マスター データ サービス データベース ロール  
  
|ロール|説明|  
|----------|-----------------|  
|`mds_exec`|このロールには、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] Web アプリケーションを作成してアプリケーション プールのアカウントを指定したときに [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] で指定したアカウントが含まれます。 mds_exec ロールには次の権限があります。<br /><br /> **EXECUTE**すべてのスキーマに対する権限。<br /><br /> **ALTER**、**挿入**、および**選択**これらのテーブルに対する権限。<br />mdm.tblStgMember<br />mdm.tblStgMemberAttribute<br />mdm.tbleStgRelationship<br /><br /> **選択**これらのテーブルに対する権限。<br />mdm.tblUser<br />mdm.tblUserGroup<br />mdm.tblUserPreference<br /><br /> **選択**これらのビューに対する権限。<br />mdm.viw_SYSTEM_SECURITY_NAVIGATION<br />mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br />mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL_MEMBER<br />mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>スキーマ  
  
|ロール|説明|  
|----------|-----------------|  
|`mdm`|mdq スキーマに含まれている関数以外のすべての [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース オブジェクトおよび Service Broker オブジェクトが含まれます。|  
|`mdq`|正規表現または類似性に基づくメンバーの結果のフィルター処理や書式設定通知電子メールに関連する [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース関数が含まれます。|  
|**stg**|ステージング処理に関連する [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース テーブル、ストアド プロシージャ、およびビューが含まれます。 これらのオブジェクトは削除しないでください。 ステージング処理の詳細については、次を参照してください。[データのインポート&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)します。|  
  
## <a name="see-also"></a>参照  
 [データベース オブジェクト セキュリティ (マスター データ サービス)](../../2014/master-data-services/database-object-security-master-data-services.md)  
  
  
