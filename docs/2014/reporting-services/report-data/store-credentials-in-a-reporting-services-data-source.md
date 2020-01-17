---
title: Reporting Services データ ソースに資格情報を保存する | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e2c29e97a360b9e595b972643645e2e8d549c67
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892018"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Store Credentials in a Reporting Services Data Source
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポート サーバーが、レポートに必要な外部データにアクセスするときに使用する、保存された資格情報を構成できます。 保存された資格情報は、レポートを自動実行する場合に使用されます。たとえば、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] サブスクリプションがレポートを電子メールとしてパブリッシュする場合などです。 この資格情報は、レポート処理がスケジュールで設定されている場合、または、レポート処理がトリガーされた場合に、レポート サーバーによって取得されて使用されます。 このトピックでは、ネイティブ モードと SharePoint モードの両方のレポート サーバーに対して、保存された資格情報を構成する方法について説明します。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint モード|  
  
 **このトピックの内容:**  
  
-   [レポート固有のデータ ソース用の保存された資格情報を構成する (ネイティブ モード)](#bkmk_stored_credentials_data_source_native)  
  
-   [レポート固有のデータ ソース用の保存された資格情報を構成する (SharePoint モード)](#bkmk_stored_credentials_data_source_sharepoint)  
  
-   [共有データ ソース用の保存された資格情報を構成する (ネイティブ モード)](#bkmk_stored_credentials_shared_data_source_native)  
  
-   [共有データ ソース用の保存された資格情報を構成する (SharePoint モード)](#bkmk_stored_credentials_shared_data_source_sharepoint)  
  
##  <a name="bkmk_top"></a> 保存された資格情報のセキュリティ ポリシー要件  
 ![as_powerpivot_refresh_sss_set_key](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") 保存された資格情報に使用するアカウントを、レポート サーバー上で、次のいずれかのセキュリティ ポリシー用に構成する必要があります。 環境に必要な最小レベルの権限を持つポリシーを選択することをお勧めします。  
  
1.  **ローカル ログオンを許可する**。 詳細については、「 [ローカル ログオンを許可する](https://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx)」を参照してください。  
  
2.  **バッチ ジョブとしてログオン**。 詳細については、「 [バッチ ジョブとしてログオン](https://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx)」を参照してください。  
  
3.  ポリシーに関する一般的な情報については、「 [グループ ポリシー オブジェクトのセキュリティの設定を編集する](https://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx)」を参照してください。  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> レポート固有のデータ ソース用の保存された資格情報を構成する (ネイティブ モード)  
  
1.  ネイティブ モードのレポート マネージャーで、レポートが含まれているフォルダーに移動します。 コンテキスト メニューをクリックします![レポート マネージャーの ssrs 項目のコンテキスト メニュー](../media/ssrs-report-manager-item-context-menu.png "レポート マネージャーの ssrs 項目のコンテキスト メニュー")。  
  
2.  **[管理]** をクリックして、 **[データ ソース]** をクリックします。  
  
3.  **[カスタム データ ソース]** をクリックします。  
  
4.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を選択します。  
  
5.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 以下に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  **[接続に使用する認証]** で、 **[レポート サーバーに保存され、セキュリティで保護された資格情報]** をクリックします。  
  
7.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<ドメイン>\\<アカウント\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[データ ソースへの接続時に Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[データ ソースへの接続が確立した後に、認証されているユーザーの権限を借用する]** を選択できます。  
  
8.  **[適用]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](../../2014-toc/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")[保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> レポート固有のデータ ソース用の保存された資格情報を構成する (SharePoint モード)  
  
1.  レポートを含むドキュメント ライブラリを参照し、開くメニューをクリックします![ssrs 項目のドキュメント ライブラリのコンテキスト メニュー](../media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")。  
  
2.  2 番目の開くメニューをクリックし![ssrs 項目のドキュメント ライブラリのコンテキスト メニュー](../media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")、 **[データ ソースの管理]** をクリックします。  
  
3.  資格情報を使用して構成する **[カスタム]** データ ソースの名前をクリックします。  
  
4.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を選択します。  
  
5.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 以下に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  **[資格情報]** で、 **[格納された資格情報]** を選択します。  
  
7.  **[ユーザー名]** と **[パスワード]** を入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<ドメイン>\\<アカウント\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[実行コンテキストをこのアカウントに設定する]** を選択できます。  
  
8.  **[OK]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](../../2014-toc/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")[保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> 共有データ ソース用の保存された資格情報を構成する (ネイティブ モード)  
  
1.  ネイティブ モードのレポート マネージャーで、共有データ ソース アイテムに移動します。 ![共有データ ソースのアイコン](../media/hlp-16datasource.png "共有データ ソースのアイコン")  
  
2.  コンテキスト メニューをクリックし![レポート マネージャーの ssrs 項目のコンテキスト メニュー](../media/ssrs-report-manager-item-context-menu.png "レポート マネージャーの ssrs 項目のコンテキスト メニュー")、 **[管理]** をクリックします。  
  
3.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を指定します。  
  
4.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、接続文字列に資格情報を指定しないことをお勧めします。  
  
     以下に、ローカルの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<ドメイン>\\<アカウント\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[データ ソースへの接続時に Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[データ ソースへの接続が確立した後に、認証されているユーザーの権限を借用する]** を選択できます。  
  
6.  **[適用]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](../../2014-toc/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")[保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> 共有データ ソース用の保存された資格情報を構成する (SharePoint モード)  
  
1.  ドキュメント ライブラリで、共有データ ソース項目を参照します。![共有データ ソースのアイコン](../media/hlp-16datasource.png "共有データ ソースのアイコン")  
  
2.  コンテキスト メニューをクリックし![ssrs アイテム項目のドキュメント ライブラリのコンテキスト メニュー](../media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")、2 番目のコンテキスト メニューをクリックします![ssrs 項目のドキュメント ライブラリのコンテキスト メニュー](../media/ssrs-sharepoint-item-context-menu.png "ssrs 項目のドキュメント ライブラリのコンテキスト メニュー")。  
  
3.  **[データ ソース定義の編集]** をクリックします。  
  
4.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を指定します。  
  
5.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、接続文字列に資格情報を指定しないことをお勧めします。  
  
     以下に、ローカルの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<ドメイン>\\<アカウント\> という形式で指定し、 **[Windows 資格情報として使用する]** を選択します。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[実行コンテキストをこのアカウントに設定する]** を選択できます。  
  
7.  **[OK]** をクリックします。  
  
     ![[トップに戻る] リンクで使用される矢印アイコン](../../2014-toc/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")[保存された資格情報のセキュリティ ポリシーの要件](#bkmk_top)  
  
## <a name="see-also"></a>関連項目  
 [レポート データ ソースに関する資格情報と接続情報を指定する](../../integration-services/connection-manager/data-sources.md)   
 [レポートのデータ ソースのプロパティを構成する &#40;レポート マネージャー&#41;](configure-data-source-properties-for-a-report-report-manager.md)   
 [共有データ ソースを作成、削除、または変更する &#40;レポート マネージャー&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [[データ ソース] プロパティ ページ &#40;レポート マネージャー&#41;](../data-sources-properties-page-report-manager.md)   
 [[新しいデータ ソース] ページ (レポート マネージャー)](../new-data-source-page-report-manager.md)  
  
  
