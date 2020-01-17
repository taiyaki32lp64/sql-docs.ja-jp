---
title: レポート データ ソース内の資格情報を SharePoint サイトから更新する | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a9908e340dadeb1108e68ca10f466276c14df23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575433"
---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>レポート データ ソース内の資格情報を SharePoint サイトから更新する
  このトピックでは、レポートに埋め込まれたデータ ソースや、SharePoint ドキュメント ライブラリ内に保存された共有データ ソースを更新する方法について説明します。  
  
 多くのレポートには、データ ソースが含まれていたり、Windows 認証を使用するように構成された共有データ ソースが使用されていることがあります。 SharePoint ドキュメント ライブラリ内に保存されたレポートに関するデータ警告を作成する場合など、状況によっては、データ ソース資格情報を更新して、保存済み資格情報を使用するようにしたり、資格情報を要求しないようにする必要があります。  
  
 保存された資格情報をレポートで使用するために、新しい SQL Server ログインを作成および使用する場合があります。 詳細については、「 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)」を参照してください。  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>保存された資格情報を使用するように埋め込みデータソースを更新するには  
  
1.  レポートを保存した SharePoint ドキュメント ライブラリに移動します。  
  
2.  レポートの展開ドロップダウン メニューのアイコンをクリックし、 **[データ ソースの管理]** をクリックします。  
  
     [データ ソースの管理] ページが開きます。  
  
3.  **[名前]** 列で、データ ソースをクリックします。  
  
4.  **[接続の種類]** で、 **[カスタム データ ソース]** オプションが選択されていることを確認します。  
  
     このオプションは、データ ソースがレポートに埋め込まれることを示します。  
  
5.  レポートを別の種類のデータ ソース、別のサーバー、または別のデータ ストアに接続したい場合を除き、 **[データ ソースの種類]** オプションと **[接続文字列]** オプションはそのままにします。  
  
6.  **[資格情報]** で、 **[格納された資格情報]** を選択します。 このオプションは、データ ソースで資格情報が不要な場合、または他の方法で資格情報を渡している場合にのみ機能します。  
  
     状況によっては、 **[資格情報は必要ありません]** オプションを使用することもできます。  
  
     一部の種類のデータ ソースについては、レポート サーバーで自動実行アカウントを構成する必要があります。 詳細については、「[外部データ ソースのデータを追加する (SSRS)](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)」および「[自動実行アカウントの構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」で、対応するデータ ソースの種類に関するトピックを参照してください。  
  
7.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<ドメイン>\\<アカウント\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[データ ソースへの接続時に Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[実行コンテキストをこのアカウントに設定する]** を選択できます。  
  
8.  データ ソースが更新後の資格情報を使用して接続できるかどうかを確認するには、 **[接続テスト]** をクリックします。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>保存された資格情報を使用するように共有データソースを更新するには  
  
1.  共有データ ソースを保存した SharePoint ドキュメント ライブラリに移動します。  
  
2.  共有データ ソースの展開ドロップダウン メニューのアイコンをクリックし、 **[データ ソース定義の編集]** をクリックします。  
  
     [データ ソース] ページが開きます。  
  
3.  共有データ ソースを別の種類のデータ ソース、別のサーバー、または別のデータ ストアに接続したい場合を除き、 **[データ ソースの種類]** オプションと **[接続文字列]** オプションはそのままにします。  
  
4.  **[資格情報]** で、 **[格納された資格情報]** を選択します。  
  
     状況によっては、 **[資格情報は必要ありません]** オプションを使用することもできます。 このオプションは、データ ソースで資格情報が不要な場合、または他の方法で資格情報を渡している場合にのみ機能します。  
  
     一部の種類のデータ ソースについては、レポート サーバーで自動実行アカウントを構成する必要があります。 詳細については、「[外部データ ソースのデータを追加する (SSRS)](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)」および「[自動実行アカウントの構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」で、対応するデータ ソースの種類に関するトピックを参照してください。  
  
5.  ユーザー名とパスワードを入力します。  
  
    -   このアカウントが Windows ドメイン ユーザー アカウントである場合は、\<ドメイン>\\<アカウント\> という形式で指定し、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにします。  
  
    -   ユーザー名とパスワードがデータベースの資格情報である場合は、 **[データ ソースへの接続時に Windows 資格情報として使用する]** を選択しないでください。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[実行コンテキストをこのアカウントに設定する]** を選択できます。  
  
6.  データ ソースが更新後の資格情報を使用して接続できるかどうかを確認するには、 **[接続テスト]** をクリックします。  
  
7.  [このデータ ソースを有効にする] が選択されていることを確認します。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [SharePoint ライブラリへのドキュメントのアップロード &#40;Reporting Services の SharePoint モード&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  
