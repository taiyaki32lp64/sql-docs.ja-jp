---
title: データのインポート (マスター データ サービス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], about staging process
- importing data [Master Data Services]
- staging process [Master Data Services]
ms.assetid: 181d1e22-379c-45d1-b03c-e1e22ff14164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7f5f5e7d6c4706dee09c90237c2363f6cbf46b02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479014"
---
# <a name="data-import-master-data-services"></a>データのインポート (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]内のデータのモデルを作成すると、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースでデータの追加と変更ができるようになります。   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ステージング テーブル、ストアド プロシージャ、マスター データ マネージャーを使います。  
  
 使用することも、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]、MDS リポジトリにデータを追加する ([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]データベース)。 詳細については、次を参照してください。[データのパブリッシュ&#40;MDS アドインの Excel&#41;](microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)します。  
  
 データを追加して更新するときに、次の操作を行うことができます。  
  
-   メンバーの読み込みと更新、属性値の更新  
  
-   メンバーの非アクティブ化と削除  
  
-   明示的階層メンバーの移動  
  
 データの追加と更新には、次の主要なタスクが含まれます。  
  
1.  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースのステージング テーブルにデータを読み込みます。  
  
2.  ステージング テーブルから適切な [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] テーブルにデータを読み込みます。  
  
     ステージング ストアド プロシージャや [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] を使って、データを読み込みます。  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] では、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] ステージング プロセスのサポートは非推奨とされました。  
  
## <a name="deactivating-and-deleting-members"></a>メンバーの非アクティブ化と削除  
 非アクティブにしたメンバーは、再びアクティブにできます。 メンバーを再びアクティブにすると、階層およびコレクションにおける属性とメンバーシップが復元されます。 以前のトランザクションはすべてそのままです。 マスター データ マネージャーの **[バージョン管理]** 機能領域の管理者は、非アクティブになっているトランザクションを表示できます。  
  
 削除したメンバーは、システムから完全に削除されます。 そのメンバーのすべてのトランザクション、すべてのリレーションシップ、およびすべての属性が完全に削除されます。  
  
> [!NOTE]  
>  ステージングを使用してメンバーを再アクティブ化することはできません。 マスター データ マネージャーで手動で行う必要があります。 詳細については、「[メンバーまたはコレクションを再アクティブ化する (マスター データ サービス)](reactivate-a-member-or-collection-master-data-services.md)」を参照してください。  
>   
>  ステージングを使用してコレクションを削除または非アクティブ化することはできません。 手動でのコレクションの非アクティブ化の詳細については、「[メンバーまたはコレクションを削除する (マスター データ サービス)](../../2014/master-data-services/delete-a-member-or-collection-master-data-services.md)」を参照してください。  
  
## <a name="moving-explicit-hierarchy-members"></a>明示的階層メンバーの移動  
 明示的階層に含まれるメンバーの位置を一括で移動するときは、次を指定できます。  
  
-   統合メンバーの親として統合メンバー。  
  
-   リーフ メンバーの親として統合メンバー。  
  
-   リーフ メンバーまたは統合メンバーの兄弟としてリーフ メンバー。  
  
-   リーフ メンバーまたは統合メンバーの兄弟として統合メンバー。  
  
## <a name="staging-tables-and-stored-procedures"></a>ステージング テーブルとストアド プロシージャ  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースには、データを設定できる、次の種類のステージング テーブルが含まれています。  
  
-   [リーフ メンバー ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)  
  
-   [統合メンバー ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)  
  
-   [リレーションシップ ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/relationship-staging-table-master-data-services.md)  
  
 モデル内の各エンティティには、ステージング テーブルがあります。 テーブル名は、対応するエンティティと、リーフ メンバーなどのエンティティ型を示します。 次の画像は、通貨、顧客、製品のエンティティのステージング テーブルを示しています。  
  
 ![MDS データベースのステージング テーブル](../../2014/master-data-services/media/mds-stagingtables.png "MDS データベースのステージング テーブル")  
  
 テーブルの名前はエンティティの作成時に指定され、変更できません。 ステージング テーブルの名前に _1 またはその他の数値が含まれる場合は、エンティティの作成時にその名前のテーブルが既に存在していたことを示します。  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] には、次の種類のステージング ストアド プロシージャが含まれています。  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
 モデル内の各エンティティには、リーフ メンバー、統合メンバー、リレーションシップ ステージング テーブルに対応する 3 つのストアド プロシージャがあります。  次の画像は、通貨、顧客、製品のエンティティのステージング ストアド テーブルを示しています。  
  
 ![MDS データベースのステージング ストアド プロシージャ](../../2014/master-data-services/media/mds-stagingstoredprocedures.png "MDS データベースのステージング ストアド プロシージャ")  
  
 ストアド プロシージャの詳細については、「[ステージング ストアド プロシージャ (マスター データ サービス)](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)」を参照してください。  
  
## <a name="logging-transactions"></a>トランザクションのログ記録  
 データまたはリレーションシップのインポート時または更新時に発生するトランザクションは、すべてログに記録することができます。 ストアド プロシージャのオプションによって、このログ記録が可能になります。 ステージング処理を [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]から開始する場合、ログ記録は行われません。  
  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]では、 **[すべてのステージング トランザクションをログに記録]** 設定がステージング データのこのメソッドに適用されません。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [検証 (マスター データ サービス)](../../2014/master-data-services/validation-master-data-services.md)  
  
-   [ビジネス ルール (マスター データ サービス)](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
