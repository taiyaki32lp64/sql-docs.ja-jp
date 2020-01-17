---
title: ロールを作成、削除、または変更する (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 066c69298126cbc635d388d75659b98dcff95917
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101806"
---
# <a name="create-delete-or-modify-a-role-management-studio"></a>ロールを作成、削除、または変更する (Management Studio)
  Reporting Services には、レポート サーバーへのアクセス レベルをあらかじめ定義したロールが用意されています。 レポート サーバーにアクセスする各ユーザーまたはグループは、実行できるタスクが定義されたロールを介して、レポート サーバーにアクセスすることになります。 ロールは、レポート サーバー全体に対して定義されます。 レポート サーバーの特定の部分についてロール定義を変更したり、状況に依存するようなロールを指定したりすることはできません。  
  
 ロールを作成、変更、または削除するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用します。 削除できるのは、使用されていないロールだけです。  
  
 作成したロールにユーザーおよびグループを割り当てるには、レポート マネージャーを使用します。 詳細については、「 [レポート サーバーへのユーザー アクセスを許可する &#40;レポート マネージャー&#41;](grant-user-access-to-a-report-server.md)」を参照してください。  
  
> [!NOTE]  
>  レポート サーバーが SharePoint 統合モード用に構成されている場合、統合先の SharePoint サイトに接続すると、レポート サーバーのコンテンツや操作へのアクセスを制御する権限レベルを閲覧および変更できます。  
  
### <a name="to-create-a-role-definition"></a>ロールの定義を作成するには  
  
1.  オブジェクト エクスプローラーで、レポート サーバーのノードを展開します。  
  
2.  [セキュリティ] フォルダーを展開します。  
  
3.  アイテムレベルのロールの定義を作成する場合は、 **[ロール]** を右クリックし、 **[新しいロール]** をポイントします。  
  
     また、システム レベルのロールの定義を作成する場合は、 **[システム ロール]** を右クリックし、 **[新しいシステム ロール]** をポイントします。  
  
4.  ロールに対する一意の名前を入力します。 名前には、少なくとも 1 つの文字が含まれている必要があります。 スペースおよび記号を含めることもできますが、; ? : \@ & = +, $/* \< > |"または/。  
  
5.  必要に応じて、説明を入力します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、この説明はこのページでのみ表示されます。 レポート マネージャーを使用してこのアイテムを表示するユーザーは、この説明をレポート マネージャーで参照できます。  
  
6.  このロールのメンバーが実行できるタスクを選択します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-or-modify-a-role-definition"></a>ロールの定義を削除または変更するには  
  
1.  オブジェクト エクスプローラーで、レポート サーバーのノードを展開します。  
  
2.  [セキュリティ] フォルダーを展開します。  
  
3.  アイテムレベルのロールの定義を削除または変更するには、[ロール] フォルダーを展開します。 次のいずれかを実行します。  
  
    1.  ロールの定義を削除するには、アイテムを右クリックし、 **[削除]** をクリックします。 **[オブジェクトの削除]** ダイアログ ボックスが表示されます。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  ロールの定義を変更するには、アイテムを右クリックし、 **[プロパティ]** をクリックします。 **[ユーザー ロールのプロパティ]** ダイアログ ボックスの [全般] ページが表示されます。  
  
         このロールのメンバーが実行できるタスクを選択し、 **[OK]** をクリックします。  
  
4.  システム レベルのロールの定義を削除または変更するには、 **[システム ロール]** フォルダーを展開します。 次のいずれかを実行します。  
  
    1.  システム ロールの定義を削除するには、アイテムを右クリックし、 **[削除]** をクリックします。 **[オブジェクトの削除]** ダイアログ ボックスが表示されます。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  システム ロールの定義を変更するには、アイテムを右クリックし、 **[プロパティ]** をクリックします。 **[システム ロールのプロパティ]** ダイアログ ボックスの [全般] ページが表示されます。  
  
         このロールのメンバーが実行できるタスクを選択し、 **[OK]** をクリックして変更を適用します。  
  
## <a name="see-also"></a>参照  
 [Management Studio でレポート サーバーに接続する](../tools/connect-to-a-report-server-in-management-studio.md)   
 (作成-と-管理-ロール-assignments.md)   
 [SQL Server Management Studio の Reporting Services &#40;SSRS&#41;](../tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  
