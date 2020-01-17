---
title: データベース オブジェクト セキュリティ (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], object security
- security [Master Data Services], database objects
ms.assetid: dd5ba503-7607-45d9-ad0d-909faaade179
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3eafc9720197ffc32cdca2ef58f91725befaaec1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483150"
---
# <a name="database-object-security-master-data-services"></a>データベース オブジェクト セキュリティ (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースでは、データは複数のデータベース テーブルに格納されており、ビューで表示できます。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションで保護されている可能性がある情報は、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースにアクセスできるユーザーであれば参照できます。  
  
 具体的には、従業員の給与情報が Employee モデルに含まれており、企業の財務情報が Account モデルに含まれている場合を考えることができます。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ユーザー インターフェイスでこれらのモデルへのユーザー アクセスを拒否できますが、データベースへのアクセス権を持つユーザーはこのデータを表示できます。  
  
 ユーザーが固有のデータを使用できるように、データベース オブジェクトに権限を付与できます。 権限付与の詳細については、「[GRANT (オブジェクトの権限の許可) (Transact-SQL)](/sql/t-sql/statements/grant-object-permissions-transact-sql)」を参照してください。 SQL server の保護の詳細については、「[SQL Server の保護](../relational-databases/security/securing-sql-server.md)」を参照してください。  
  
 次のタスクでは [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースへのアクセスが必要です。  
  
-   [データをステージングする](#Staging)  
  
-   [ビジネス ルールに対してデータを検証する](#rules)  
  
-   [バージョンを削除する](#Versions)  
  
-   [階層メンバーの権限を直ちに適用する](#Hierarchy)  
  
-   [システム管理者アカウントを変更します。](#SysAdmin)  
  
-   [システム設定を構成する](#SysSettings)  
  
##  <a name="Staging"></a> データをステージングする  
 次の表では、セキュリティ保護可能な各リソースの名前の一部に "name" を使用しています。 これは、エンティティの作成時に指定するステージング テーブルの名前を示します。 詳細については、次を参照してください[データのインポート&#40;マスター データ サービス。&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
|アクション|[セキュリティ保護可能なリソース]|アクセス許可|  
|------------|----------------|-----------------|  
|リーフ メンバーとその属性をステージング テーブルに読み込む|stg.name_Leaf|必須:INSERT<br /><br /> 省略可能:SELECT と UPDATE|  
|リーフ ステージング テーブルから MDS データベースの適切なテーブルにデータを読み込む|stg.udp_name_Leaf|EXECUTE|  
|統合メンバーとその属性をステージング テーブルに読み込む|stg.name_Consolidated|必須:INSERT<br /><br /> 省略可能:SELECT と UPDATE|  
|統合ステージング テーブルから MDS データベースの適切なテーブルにデータを読み込む|stg.udp_name_Consolidated|EXECUTE|  
|リーフ メンバーと相互に明示的階層内の統合メンバーのリレーションシップをステージング テーブルに読み込みます。|stg.name_Relationship|必須:INSERT<br /><br /> 省略可能:SELECT と UPDATE|  
|リレーションシップ ステージング テーブルから MDS の適切なテーブルにデータを読み込む|stg.udp_name_Relationship|EXECUTE|  
|ステージング テーブルのデータが MDS データベース テーブルに挿入されたときに発生したエラーを表示する|stg.udp_name_Relationship|SELECT|  
  
 詳細については、「[データのインポート &#40;マスター データ サービス&#41;](overview-importing-data-from-tables-master-data-services.md)」を参照してください。  
  
##  <a name="rules"></a> ビジネス ルールに対してデータを検証する  
  
|アクション|セキュリティ保護可能|アクセス許可|  
|------------|---------------|-----------------|  
|ビジネス ルールに対してデータのバージョンを検証する|mdm.udpValidateModel|EXECUTE|  
  
 詳細については、「 [検証ストアド プロシージャ (マスター データ サービス)](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)」を参照してください。  
  
##  <a name="Versions"></a> バージョンを削除する  
  
|アクション|[セキュリティ保護可能なリソース]|アクセス許可|  
|------------|----------------|-----------------|  
|削除するバージョンの ID を決定する|mdm.viw_SYSTEM_SCHEMA_VERSION|SELECT|  
|モデルのバージョンを削除する|mdm.udpVersionDelete|EXECUTE|  
  
 詳細については、「[バージョンを削除する (マスター データ サービス)](../../2014/master-data-services/delete-a-version-master-data-services.md)」を参照してください。  
  
##  <a name="Hierarchy"></a> 階層メンバーの権限を直ちに適用する  
  
|アクション|[セキュリティ保護可能なリソース]|アクセス許可|  
|------------|----------------|-----------------|  
|メンバー権限を直ちに適用する|mdm.udpSecurityMemberProcessRebuildModel|EXECUTE|  
  
 詳細については、「[メンバー権限を直ちに適用する (マスター データ サービス)](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md)」を参照してください。  
  
##  <a name="SysAdmin"></a> システム管理者アカウントを変更します。  
  
|アクション|[セキュリティ保護可能なリソース]|アクセス許可|  
|------------|----------------|-----------------|  
|新しい管理者の SID を決定する|mdm.tblUser|SELECT|  
|システム管理者アカウントを変更します。|mdm.udpSecuritySetAdministrator|EXECUTE|  
  
 詳細については、次を参照してください。[システム管理者アカウントを変更&#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)します。  
  
##  <a name="SysSettings"></a> システム設定を構成する  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]での動作を制御するために構成可能なシステム設定が用意されています。 これらの設定は [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] で調整できます。または、UPDATE アクセス権を持つ場合は、mdm.tblSystemSetting データベース テーブルで直接調整できます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../../2014/master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [セキュリティ (マスター データ サービス)](../../2014/master-data-services/security-master-data-services.md)  
  
  
