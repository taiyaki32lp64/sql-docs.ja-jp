---
title: 自動実行アカウントの構成 (SSRS 構成マネージャー) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- security [Reporting Services], unattended report processing
- unattended report processing [Reporting Services]
- credentials [Reporting Services]
- external data sources [Reporting Services]
- accounts [Reporting Services]
- reports [Reporting Services], processing
ms.assetid: 4e50733e-bd8c-4bf6-8379-98b1531bb9ca
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4326c38c84ad7af8fb23a5dde035720a1a7024d4
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593303"
---
# <a name="configure-the-unattended-execution-account-ssrs-configuration-manager"></a>自動実行アカウントの構成 (SSRS 構成マネージャー)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、自動レポート処理とネットワークを介した接続要求の送信に使用される特別なアカウントが用意されています。 アカウントは次の場合に使用します。  
  
-   データベース認証を使用するレポートに対する接続要求のネットワーク経由での送信や、認証を必要としないまたは使用しない外部レポート データ ソースへの接続。 詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)」をご覧ください。

-   レポートに使用する外部の画像ファイルの取得。 匿名アクセスでアクセスできない画像ファイルを使用する場合は、自動レポート処理アカウントを構成し、アカウントに対してファイルへのアクセス許可を与えます。  
  
 自動レポート処理とは、ユーザーの要求ではなく、イベント (スケジュール ドリブンのイベントまたはデータ更新イベント) によって起動されたレポート実行処理を示します。 レポート サーバーは、自動レポート処理アカウントを使用して、外部データ ソースをホストしているコンピューターにログオンします。 レポート サーバー サービス アカウントの資格情報は他のコンピューターへの接続に使用されないため、このアカウントは必要です。  
  
> [!IMPORTANT]  
>  アカウントの構成は任意ですが、 構成しない場合は、一部のデータ ソースに接続するときのオプションを制限することになり、リモート コンピューターから画像ファイルを取得できない場合があります。 アカウントを構成する場合は、アカウントを最新の状態に保つ必要があります。 特に、パスワードの有効期限が切れたり、Active Directory でアカウント情報が変更されると、次回レポートを処理するときに "ログオンに失敗しました。(rsLogonFailed) ログオン失敗: ユーザー名が不明またはパスワードが正しくありません。" というエラーが発生します。 外部画像を取得したり外部コンピューターに接続要求を送信する場合でも、自動レポート処理アカウントの適切なメンテナンスは必須です。 構成したアカウントを使用していない場合は、アカウントを削除すると、日常的なアカウント メンテナンス作業を行わずに済みます。  
  
## <a name="how-to-configure-the-account"></a>アカウントの構成方法  
 ドメイン ユーザー アカウントを使用する必要があります。 目的上このアカウントは、レポート サーバー サービスの実行に使用されるアカウントとは別のアカウントである必要があります。 必ず最小限の権限 (十分なネットワーク接続権限のある読み取り専用アクセス) を持つアカウントを使用し、アクセスする対象を、レポート サーバーにデータ ソースとリソースを提供するコンピューターのみに制限してください。  
  
 アカウントを指定するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールまたは **rsconfig** ユーティリティを使用できます。 自動実行アカウントを構成する最も簡単な方法は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを実行して、[実行アカウント] ページで資格情報を指定することです。  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動し、構成するレポート サーバー インスタンスに接続します。 手順については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
2.  [実行アカウント] ページで、 **[実行アカウントの指定]** を選択します。  
  
3.  アカウントとパスワードを入力し、パスワードを再入力して、 **[適用]** をクリックします。  
  
### <a name="using-rsconfig-utility"></a>RSCONFIG ユーティリティの使用  
 アカウントを設定するもう 1 つの方法は、 **rsconfig** ユーティリティを使用することです。 アカウントを指定するには、 **rsconfig** の **-e**引数を使用します。 **rsconfig** に **-e** 引数を指定すると、構成ファイルにアカウント情報を書き込むようユーティリティに指示できます。 RSreportserver.config へのパスを指定する必要はありません。アカウントを構成するには、次の手順を実行します。  
  
1.  レポート サーバーにデータまたはサービスを提供するコンピューターおよびサーバーに対してアクセス権を持つ、ドメイン アカウントを作成または選択します。 少ない権限を持つアカウントを使用することをお勧めします (たとえば、読み取り専用権限)。  
  
2.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックし、 **「cmd」** と入力して **[OK]** をクリックして、コマンド プロンプトを開きます。  
  
3.  次のコマンドを入力して、ローカル レポート サーバー インスタンス上でアカウントを構成します。  
  
     **rsconfig -e -u\<ドメイン/ユーザー名> -p\<パスワード>**  
  
 **rsconfig -e** では、他にも引数がサポートされています。 構文の詳細およびコマンド例の表示方法については、「[rsconfig ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)」を参照してください。
 
### <a name="how-account-information-is-stored"></a>アカウント情報の保存方法  
 アカウントを設定すると、ローカルまたはリモートのレポート サーバー インスタンス上の RSreportserver.config ファイル内で、暗号化された値として次の設定が指定されます。  
  
```  
<UnattendedExecutionAccount>  
     <UserName></UserName>  
     <Password></Password>  
     <Domain></Domain>  
</UnattendedExecutionAccount>  
```  
  
 いったん値を設定すると、暗号化解除してプレーン テキストで表示することはできません。 値を入力し間違えた場合や、指定した値を忘れた場合は、Reporting Services 構成ツールを使用するか、 **rsconfig -e** を実行して最初からやり直す必要があります。  
  
## <a name="how-to-use-the-unattended-report-processing-account"></a>自動レポート処理アカウントの使用方法  
 画像ファイルを取得する際、レポート サーバーでは自動的にこのアカウントが使用され、ユーザー側で特別な操作を行う必要はありません。 このアカウントを使用してレポート用のデータを提供する外部データ ソースに接続するには、レポート データ ソースまたは共有データ ソースの [データ ソースのプロパティ] ページで **[資格情報の種類]** オプションを指定する必要があります。  
  
-   [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] または SharePoint サイトで、 **[資格情報は必要ありません]** オプションを選択します。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
 自動レポート処理アカウントは主に外部サーバーへの接続に使用されますが、データベース サーバーへのログインには使用されません。 アカウント資格情報を使用してデータベースにログインする場合は、資格情報を接続文字列に指定する必要があります。 データベース サーバーで Windows 統合セキュリティがサポートされ、自動実行レポート処理に使用されるアカウントにデータベースの読み取り権限がある場合は、 **Integrated Security=SSPI** を指定できます。 それ以外の場合は、接続文字列にユーザー名およびパスワードを入力する必要があり、これはデータ ソース接続プロパティを編集する権限を持つすべてのユーザーにクリア テキストで表示されます。  
  
 接続の確立後に自動実行レポート処理アカウントを使用してデータを取得することもできますが、それは推奨されません。 このアカウントは、ごく特定の機能に対してだけ使用されることを意図しています。 データの取得に使用した場合、意図された目的に反することになります。  
  
## <a name="how-to-maintain-the-unattended-report-processing-account"></a>自動レポート処理アカウントのメンテナンス方法  
 自動レポート処理アカウントを構成したら、アカウントとパスワードを最新の状態に保つ必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用すると、このアカウントに関する情報を保存している構成設定を更新できます。  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動し、構成するレポート サーバー インスタンスに接続します。  
  
2.  [実行アカウント] ページで、 **[実行アカウントの指定]** がオンになっていることを確認します。  
  
3.  新しいアカウントまたはパスワードを入力し、確認のためもう一度パスワードを入力して、 **[適用]** をクリックします。  
  
## <a name="how-to-delete-the-unattended-report-processing-account"></a>自動レポート処理アカウントの削除方法  
 アカウントを使用していない場合は、アカウントを削除すると、日常的なアカウント メンテナンス作業を行わずに済みます。  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動し、構成するレポート サーバー インスタンスに接続します。  
  
2.  [実行アカウント] ページで、 **[実行アカウントの指定]** をオフにします。  
  
3.  **[適用]** をクリックします。  
  
 アカウント情報が RSReportServer.config ファイルから削除されます。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー (SSRS ネイティブ モード)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  
