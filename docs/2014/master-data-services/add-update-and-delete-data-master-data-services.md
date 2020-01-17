---
title: 追加、データ更新および削除 (マスター データ サービス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b6295ead-bd2f-49dd-8756-35c6afb59648
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2212e7424f22ecca2619ef7215bf94b0dbb62875
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054272"
---
# <a name="add-update-and-delete-data-master-data-services"></a>データの追加、更新、および削除 (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]のモデルに一括でデータの追加および変更を行えます。  
  
 **前提条件**  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの stg.\<名前>_Leaf、 stg.\<名前>_Consolidated、stg.\<名前>_Relationship の各テーブルにデータを挿入するアクセス許可が必要です。  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの stg.udp_\<名前>_Leaf、stg.udp\_\<名前>_Consolidated、または the stg.udp\_\<名前>_Relationship の各ストアド プロシージャのいずれかを実行するアクセス許可が必要です。  
  
-   モデルのステータスが **[コミット済み]** でないことが必須です。  
  
 **[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに対してデータの追加、更新、および削除を行うには**  
  
1.  必須フィールドの値を指定するなど、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの適切なステージング テーブルにインポートするメンバーを準備します。 ステージング テーブルの概要については、次を参照してください[データのインポート&#40;マスター データ サービス。&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
    -   リーフ メンバーの場合、テーブルは stg.\<名前>_Leaf になります。ここで、\<名前> は対応するエンティティを指します。 必須フィールドの詳細については、「[リーフ メンバー ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)」を参照してください。  
  
    -   統合メンバーの場合、テーブルは stg.\<名前>_Consolidated になります。 必須フィールドの詳細については、「[統合メンバー ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)」を参照してください。  
  
    -   明示的階層内のメンバーの位置を移動する場合、テーブルは stg.\<名前>_Relationship になります。 必須フィールドの詳細については、「[リレーションシップ ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/relationship-staging-table-master-data-services.md)」を参照してください。  
  
         明示的階層内のメンバーの移動の概要については、次を参照してください。[データのインポート&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)します。  
  
    -   **[ImportType]** フィールドの値を使用して、メンバーの新規作成、メンバーの非アクティブ化、またはメンバーの削除を行っていることを指定します。 値の詳細については、「[リーフ メンバー ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)」および「[統合メンバー ステージング テーブル (マスター データ サービス)](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)」を参照してください。  
  
         非アクティブ化とメンバーの削除の概要については、次を参照してください。[データのインポート&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)します。  
  
2.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースのデータベース エンジン インスタンスに接続します。  
  
     詳細については、「 [SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md)」を参照してください。  
  
3.  [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインポートおよびエクスポート] ウィザードを使用して、データをステージング テーブルにインポートします。  
  
     詳細については、「 [SQL Server Import and Export Wizard](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」を参照してください。  
  
4.  次のいずれかを実行して、ステージング テーブルからデータを [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] テーブルに読み込みます。  
  
    -   データの移動先のステージング テーブルに対応するステージング ストアド プロシージャを実行します。  
  
         ステージング ストアド プロシージャとステージング テーブルの概要については、次を参照してください。[データのインポート&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)します。 ステージング ストアド プロシージャのパラメーターの詳細およびコード例については、「[ステージング ストアド プロシージャ (マスター データ サービス)](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)」を参照してください。  
  
    -   マスター データ管理の **[統合管理]** 機能領域 を使用します。  
  
         **[ステージング バッチ]** ページで、ドロップダウン リストでデータの追加先のモデルを選択してから、 **[バッチの開始]** をクリックします。 バッチ処理の状態が、 **[状態]** フィールドに示されます。 状態の詳細については、「[インポート状態 (マスター データ サービス)](../../2014/master-data-services/import-statuses-master-data-services.md)」を参照してください。  
  
         ![マスター データ マネージャーでの [ステージング バッチ] ページ](../../2014/master-data-services/media/mds-staging-batches.png "マスター データ マネージャーでの [ステージング バッチ] ページ")  
  
         ステージング処理は、 **の** [ステージング バッチの間隔] [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]設定に定められた間隔で開始されます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../../2014/master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
5.  ステージング中に発生したエラーを表示します。 詳細については、次を参照してください。[ステージング処理中に発生したエラーの表示&#40;Master Data Services&#41; ](view-errors-that-occur-during-staging-master-data-services.md)と[ステージング処理のエラー &#40;Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md)します。  
  
6.  ビジネス ルールに対してデータを検証します。  
  
     マスター データ マネージャーで、モデルの **[エクスプ ローラー]** 機能領域に移動してから、データを検証するビジネス ルールを適用します。 詳細については、「[ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス)](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)」を参照してください。 データの検証にはストアド プロシージャを使用することもできます。 詳細については、「 [検証ストアド プロシージャ (マスター データ サービス)](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)」を参照してください。  
  
     ステージング テーブルからデータを読み込む場合、ビジネス ルールに対してデータが自動的に検証されることはありません。 検証とその実施タイミングの詳細については、「[検証 (マスター データ サービス)](../../2014/master-data-services/validation-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データのインポート&#40;マスター データ サービス&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
  
