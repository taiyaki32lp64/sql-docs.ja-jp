---
title: SharePoint サイト上のレポート サーバー アイテムに対するアクセス許可の設定 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
ms.assetid: 2467c657-a3bf-4ec3-a88c-8877df19823d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8bdd50291a009189bf894300cdea4633fdd952f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570612"
---
# <a name="set-permissions-for-report-server-items-on-a-sharepoint-site"></a>SharePoint サイト上のレポート サーバー アイテムに対する権限の設定
  既定のセキュリティ設定では必要なレベルのアクセスが提供されない場合は、新しい権限レベルを作成して、特定のレポート サーバー アイテムまたは処理に対するアクセスを提供できます。 カスタム セキュリティ設定は、アクセスを特定のレポートに制限する場合に便利です。  
  
 権限レベルおよびグループを作成できるのはサイト所有者だけです。 権限レベルは、サイト全体でグローバルに使用されます。 新しい権限レベルを作成した場合、他のサイト所有者もその権限レベルを使用できるようになります。  
  
 ほとんどの権限は、親サイトから継承されます。 特定のライブラリまたはアイテムに権限を割り当てた場合は、権限の継承が無効になるので、サイト階層のその分岐に関する権限管理に追加のオーバーヘッドが生じます。  
  
 権限は、レポート定義 (.rdl)、モデル (.smdl)、および共有データ ソース (.rsds) ファイルに対して設定できます。 同一のアイテムについて、継承された権限とそのアイテムに対して管理する権限を組み合わせることはできません。 権限を直接管理することを選択した場合、継承された権限は現在のアイテムに対して無効になります。 後で権限の継承を再開する場合、 **[アクション]** メニューの **[権限の継承]** を選択します。  
  
 モデル内のエンティティおよびパースペクティブに対する権限を設定するには、モデルに対するフル コントロール レベルの権限が必要です。 フル コントロールには、サイト所有者とフル コントロール レベルの権限を持つ他の SharePoint グループに与えられるサイト レベルの権限である "権限の管理" が含まれます。 特定のユーザーがモデル アイテム セキュリティを設定できるようにするには、権限の継承を無効にした後で、高度な権限 (たとえばフル コントロール) をモデル ファイル上のユーザーまたはグループに許可する必要があります。 アイテム (たとえばライブラリ内のファイル) に対するフル コントロールを許可した場合、権限のスコープはそのアイテムであり、親や同じライブラリ内の他のアイテムには及びません。 モデルに対する権限の管理権限が与えられたユーザーは、SharePoint サイトまたはモデル デザイナーを介して、設定されたモデル アイテム セキュリティを使用できます。  
  
### <a name="to-set-permissions-on-an-individual-report-model-or-data-source"></a>レポート、モデル、またはデータ ソースに対して個別に権限を設定するには  
  
1.  まだライブラリが開いていない場合は、サイド リンク バーでライブラリの名前をクリックします。 ライブラリの名前が表示されていない場合は、 **[すべてのサイト コンテンツの表示]** をクリックし、ライブラリの名前をクリックします。  
  
2.  レポート、レポート モデル、または共有データ ソース ファイルをポイントします。  
  
3.  下矢印をクリックし、メニューの **[権限の管理]** をクリックします。  
  
4.  **[アクション]** メニューの **[権限の編集]** をクリックし、 **[OK]** をクリックして操作を確定します。  
  
5.  そのファイルを使用する権限がないユーザーまたはグループに権限を与えるには、 **[新規作成]** をクリックし、 **[ユーザーの追加]** をクリックします。  
  
6.  既存のユーザーまたはグループの権限を削除または変更するには、まずユーザーまたはグループの横にあるチェック ボックスをオンにします。次に、 **[アクション]** をクリックし、 **[ユーザー権限の削除]** または **[ユーザー権限の編集]** をクリックします。  
  
### <a name="to-set-permissions-that-enable-model-item-security"></a>モデル アイテム セキュリティを有効にする権限を設定するには  
  
1.  サイトに対する "権限の管理権限" を持つアカウントを使用して、SharePoint サイトにログインします。  
  
2.  モデルが格納されているライブラリを開きます。  
  
3.  モデルをポイントします。  
  
4.  モデルの横にある下矢印をクリックし、 **[権限の管理]** をクリックします。  
  
5.  **[アクション]** をクリックします。  
  
6.  **[権限を編集]** をクリックします。 **[OK]** をクリックします。  
  
7.  **[新規作成]** をクリックします。  
  
8.  **[ユーザーの追加]** をクリックします。  
  
9. [ユーザー/グループ] で、ユーザー アカウントを入力します。  
  
10. **[ユーザーへの権限の直接付与]** を選択します。  
  
11. **[フル コントロール]** をクリックします。  
  
12. **[OK]** をクリックします。 特定のモデルの権限の管理権限が与えられたユーザーは、モデルを開いて、モデル内の権限を編集できます。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー アイテムに対して Windows SharePoint Services の組み込みのセキュリティを使用する](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)   
 [SharePoint Web アプリケーションのレポート サーバー操作に対するアクセス許可を設定する](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [SQL Server Reporting Services と SharePoint グループの役割とタスクの比較とアクセス許可](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [レポート サーバー アイテムの SharePoint サイトおよびリスト権限のリファレンス](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
