---
title: Azure Resource Explorer を使用して Azure SQL リソースを調べる
titleSuffix: Azure Data Studio
description: Azure Resource Explorer を使用して、Azure SQL Server、Azure SQL Database、Azure SQL Managed Instance を調査し、管理する方法について学習します。
ms.custom: seodec18
author: yanancai
ms.author: yanacai
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.date: 09/24/2018
ms.openlocfilehash: 2a1f62ed9266b0575f037dfe9541a026a4c1ed29
ms.sourcegitcommit: db715cad313055c8b42d547be686de8755342d65
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801136"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>Azure Resource Explorer を使用して Azure SQL リソースを調査および管理する

このドキュメントでは、[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] の Azure Resource Explorer を使用して、Azure SQL Server、Azure SQL Database、Azure SQL Managed Instance のリソースを調査し、管理する方法について学習します。

>[!NOTE]
>Azure Resource Explorer は SQL Server 2019 でサポートされています。 その後、[拡張機能マネージャー](extensions.md)または **[ファイル]**  >  **[Install Package from VSIX Package]\(VSIX パッケージからパッケージをインストールする\)** を使用して、拡張機能をインストールできます。

## <a name="connect-to-azure"></a>Azure に接続する

SQL プラグインをインストールした後、Azure アイコンが左側のメニュー バーに表示されます。 アイコンをクリックして Azure Resource Explorer を開きます。 Azure アイコンが表示されない場合は、左側のメニュー バーを右クリックし、 **[Azure Resource Explorer]** を選択します。

### <a name="add-an-azure-account"></a>Azure アカウントを追加する

Azure アカウントに関連付けられている SQL リソースを表示するには、まず [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] にアカウントを追加する必要があります。

1. 左下の [アカウント管理] アイコンから、または Azure Resource Explorer の **[Azure にサインイン]** から、 **[リンクされたアカウント]** ダイアログを開きます。

    ![Azure にサインインする](media/azure-resource-explorer/sign-in-to-azure.png)

2. **[リンクされたアカウント]** ダイアログで **[アカウントの追加]** をクリックします。

    ![Azure アカウントを追加する](media/azure-resource-explorer/add-an-azure-account.png)

3. **[コピーして開く]** をクリックして、認証用のブラウザーを開きます。

    ![ブラウザーで認証ページを開く](media/azure-resource-explorer/open-authentication-in-browser.png)

4. Web ページに**ユーザー コード**を貼り付け、 **[続行]** をクリックして認証を行います。

    ![ブラウザーでの認証](media/azure-resource-explorer/authenticate-in-browser.png)

5. [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] の **[リンクされたアカウント]** ダイアログで、ログインしている Azure アカウントが表示されます。

    ![Azure アカウントにサインインする](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>Azure アカウントをさらに追加する

複数の Azure アカウントは [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] でサポートされています。 Azure アカウントをさらに追加するには、 **[リンクされたアカウント]** ダイアログの右上にあるボタンをクリックし、「Azure アカウントを追加する」セクションと同じ手順に従って、Azure アカウントをさらに追加します。

![Azure アカウントをさらに追加する](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>Azure アカウントを削除する

既にログインしている Azure アカウントを削除するには

1. 左下の [アカウント管理] アイコンを使用して、 **[リンクされたアカウント]** ダイアログを開きます。
2. 削除するには、Azure アカウントの右側にある **[X]** ボタンをクリックします。

    ![Azure アカウントの削除](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>サブスクリプションのフィルター

Azure アカウントにログインすると、その Azure アカウントに関連付けられているすべてのサブスクリプションが Azure Resource Explorer に表示されます。 Azure アカウントごとにサブスクリプションをフィルター処理できます。

1. Azure アカウントの右側にある **[サブスクリプションの選択]** ボタンをクリックします。

   ![サブスクリプションのフィルター](media/azure-resource-explorer/filter-subscription.png)

2. 参照するアカウント サブスクリプションのチェック ボックスをオンにして、 **[OK]** をクリックします。

   ![サブスクリプションの選択](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>Azure SQL リソースを調べる

Azure Resource Explorer で Azure SQL リソースを移動するには、Azure アカウントとリソースの種類のグループを展開します。

現在、Azure Resource Explorer では、Azure SQL Server、Azure SQL Database、Azure SQL Managed Instance をサポートしています。

## <a name="connect-to-azure-sql-resources"></a>Azure SQL リソースに接続する

Azure Resource Explorer では、クエリおよび管理のために SQL Server およびデータベースに接続する際に役立つクイック アクセスが提供されます。

1. ツリー ビューから、接続する SQL リソースを探索します。
2. リソースを右クリックして **[接続]** を選択し、リソースの右側にある [接続] ボタンを見つけることもできます。

   ![Azure SQL リソースへの接続](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. 開いている **[接続]** ダイアログで、パスワードを入力し、 **[接続]** をクリックします。

   ![SQL 接続ダイアログ](media/azure-resource-explorer/sql-connection-dialog.png)
4. 接続に成功すると、新しく接続された SQL Server またはデータベースを使って、 **[サーバー]** ウィンドウが自動的に開きます。

## <a name="next-steps"></a>次の手順

- [[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] を使用した Azure SQL データベースに対する接続およびクエリ](quickstart-sql-database.md)
- [[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] を使用した Azure SQL Data Warehouse のデータに対する接続およびクエリ](quickstart-sql-dw.md)