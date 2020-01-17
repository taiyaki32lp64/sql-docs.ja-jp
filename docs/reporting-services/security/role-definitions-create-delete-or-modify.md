---
title: ロールを作成、削除、または変更する (Management Studio) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
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
ms.openlocfilehash: f079b7b16f485b92c60952d082281a1dba52d024
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570545"
---
# <a name="role-definitions---create-delete-or-modify"></a>ロールの定義 - 作成、削除、または変更

Reporting Services には、レポート サーバーへのアクセス レベルをあらかじめ定義したロールが用意されています。 レポート サーバーへのアクセスを必要とするユーザーまたはグループごとに、許可されるタスクを定義するロールが割り当てられます。 ロールは、レポート サーバー全体に対して定義されます。 ロールの定義と使用方法は、レポート サーバーのすべての領域全体で一貫させる必要があります。

ロールを作成、変更、または削除するには、[!INCLUDE[SQL Server Management Studio](../../includes/ssmanstudiofull-md.md)] を使用できます。 削除できるのは、使用されていないロールだけです。

 作成したロールにユーザーおよびグループを割り当てるには、SSRS Web ポータルを使用します。 詳細については、「[レポート サーバーへのユーザー アクセスを許可する](../../reporting-services/security/grant-user-access-to-a-report-server.md)」をご覧ください。

> [!NOTE]  
>レポート サーバーが SharePoint 統合モード用に構成されている場合、統合先の SharePoint サイトに接続すると、レポート サーバーのコンテンツや操作へのアクセスを制御する権限レベルを閲覧および変更できます。

## <a name="to-create-a-role-definition"></a>ロールの定義を作成するには

1. オブジェクト エクスプローラーで、レポート サーバーのノードを展開します。

2. [セキュリティ] フォルダーを展開します。

3. アイテムレベルのロールの定義を作成する場合は、 **[ロール]**  >  **[新しいロール]** をクリックします。

    また、システムレベルのロールの定義を作成する場合は、 **[システム ロール]**  >  **[新しいシステム ロール]** をクリックします。

4. ロールに対する一意の名前を入力します。 名前には、少なくとも 1 つの文字が含まれている必要があります。 スペースや特定の記号を含めることもできますが、文字 `[; : \ / @ & = + , $ / * < > | "]` を含めることはできません。

5. 必要に応じて、説明を入力します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、この説明はこのページでのみ表示されます。 Web ポータルからこのアイテムを表示するユーザーは、この説明をそのツールで参照できます。

6. このロールのメンバーが実行できるタスクを選択します。

7. **[OK]** を選択します。

### <a name="to-delete-or-modify-a-role-definition"></a>ロールの定義を削除または変更するには  

1. オブジェクト エクスプローラーで、レポート サーバーのノードを展開します。

2. [セキュリティ] フォルダーを展開します。

3. アイテムレベルのロールの定義を削除または変更するには、[ロール] フォルダーを展開し、次のいずれかのアクションを実行します。

    1. ロールの定義を削除するには、アイテムを右クリックし、 **[削除]** をクリックします。 **[カタログ アイテムの削除]** ダイアログ ボックスが表示されます。 **[OK]** を選択して、ロールを削除します。
  
    2. ロールの定義を変更するには、項目を右クリックし、 **[プロパティ]** をクリックします。 **[ユーザー ロールのプロパティ]** ダイアログ ボックスの [全般] ページが表示されます。

         このロールのメンバーが実行できるタスクを選択し、 **[OK]** を選択します。
  
4. システム レベルのロールの定義を削除または変更するには、 **[システム ロール]** フォルダーを展開します。 次のいずれかのアクションを実行します。

- システム ロールの定義を削除するには、アイテムを右クリックし、 **[削除]** を選択します。 **[カタログ アイテムの削除]** ダイアログ ボックスが表示されます。 **[OK]** を選択して、ロールを削除します。

- システム ロールの定義を変更するには、アイテムを右クリックし、 **[プロパティ]** を選択します。 **[システム ロールのプロパティ]** ダイアログ ボックスの [全般] ページが表示されます。 このロールのメンバーが実行できるタスクを選択し、 **[OK]** を選択して変更を適用します。

## <a name="see-also"></a>参照

 [Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
 [ロールの割り当てを作成および管理する](../../reporting-services/security/create-and-manage-role-assignments.md)  
 [SQL Server Management Studio の Reporting Services &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
