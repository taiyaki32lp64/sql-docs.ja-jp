---
title: データベース ログイン、ユーザー、およびロール
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
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
ms.openlocfilehash: 7200d919975a644321e596f66349a2a8aae26f99
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729484"
---
# <a name="database-logins-users-and-roles-master-data-services"></a>データベース ログイン、ユーザー、およびロール (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] には、 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] データベースをホストする [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンスに自動的にインストールされるログイン、ユーザー、およびロールがあります。 これらのログイン、ユーザー、およびロールは変更しないでください。  
  
## <a name="logins"></a>ログイン  
  
|Login|説明|  
|-----------|-----------------|  
|**mds_dlp_login**|UNSAFE アセンブリを作成できます。 詳細については、「 [アセンブリの作成](../relational-databases/clr-integration/assemblies/creating-an-assembly.md)」を参照してください。<br /><br /> \- ランダムに生成されたパスワードでのログインは無効です。<br /><br /> \- [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの場合は、dbo にマップされます。<br /><br /> \- msdb の場合は、mds_clr_user がこのログインにマップされます。|  
|**mds_email_login**|通知に使用されるログインは有効です。<br /><br /> msdb および [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの場合は、mds_email_user がこのログインにマップされます。|  
  
## <a name="msdb-users"></a>msdb ユーザー  
  
|ユーザー|説明|  
|----------|-----------------|  
|**mds_clr_user**|使用されていません。 mds_dlp_login にマップされます。|  
|**mds_email_user**|通知に使用します。<br /><br /> \- mds_email_login にマップされます。<br /><br /> \- DatabaseMailUserRole ロールのメンバーです。|  
  
## <a name="master-data-services-database-users"></a>マスター データ サービス データベース ユーザー  
  
|ユーザー|説明|  
|----------|-----------------|  
|**mds_email_user**|通知に使用します。<br /><br /> \- mdm スキーマに対する SELECT 権限があります。<br /><br /> \- mdm.MemberGetCriteria ユーザー定義テーブル型に対する EXECUTE 権限があります。<br /><br /> \- mdm.udpNotificationQueueActivate ストアド プロシージャに対する EXECUTE 権限があります。|  
|**mds_schema_user**|mdm スキーマと mdq スキーマを所有します。 既定のスキーマは mdm です。<br /><br /> ログインはマップされません。|  
|**mds_ssb_user**|Service Broker タスクを実行するために使用します。<br /><br /> \- すべてのスキーマに対する DELETE、INSERT、REFERENCES、SELECT、および UPDATE 権限があります。<br /><br /> \- ログインはマップされません。|  
  
## <a name="master-data-services-database-role"></a>マスター データ サービス データベース ロール  
  
|ロール|説明|アクセス許可|  
|----------|-----------------|-----------------|  
|**mds_exec**|このロールには、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] Web アプリケーションを作成してアプリケーション プールのアカウントを指定したときに [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] で指定したアカウントが含まれます。|すべてのスキーマに対する EXECUTE 権限<br /><br /> <br /><br /> 次のテーブルに対する ALTER、INSERT、および SELECT 権限<br /><br /> mdm.tblStgMember<br /><br /> mdm.tblStgMemberAttribute<br /><br /> mdm.tbleStgRelationship<br /><br /> <br /><br /> 次のテーブルに対する SELECT 権限<br /><br /> mdm.tblUser<br /><br /> mdm.tblUserGroup<br /><br /> mdm.tblUserPreference<br /><br /> <br /><br /> 次のビューに対する SELECT 権限<br /><br /> mdm.viw_SYSTEM_SECURITY_NAVIGATION<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL_MEMBER<br /><br /> mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>スキーマ  
  
|ロール|説明|  
|----------|-----------------|  
|**mdm**|mdq スキーマに含まれている関数以外のすべての [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース オブジェクトおよび Service Broker オブジェクトが含まれます。|  
|**mdq**|正規表現または類似性に基づくメンバーの結果のフィルター処理や書式設定通知電子メールに関連する [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース関数が含まれます。|  
|**stg**|ステージング処理に関連する [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース テーブル、ストアド プロシージャ、およびビューが含まれます。 これらのオブジェクトは削除しないでください。 ステージング処理の詳細については、「[概要: テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [データベース オブジェクト セキュリティ (マスター データ サービス)](../master-data-services/database-object-security-master-data-services.md)  
  
  
