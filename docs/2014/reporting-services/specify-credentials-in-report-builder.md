---
title: レポート ビルダーでの資格情報の指定 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7412ce68-aece-41c0-8c37-76a0e54b6b53
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 432b41216418cd1ad1bae70557c95a589f5e78dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101139"
---
# <a name="specify-credentials-in-report-builder"></a>レポート ビルダーでの資格情報の指定
  資格情報は、データ ソースからデータの取得を試みるユーザーの認証に使用されます。 データ ソースの所有者が、使用する資格情報の種類を決定します。 たとえば、データベース管理者は、Windows のユーザー名とパスワードの入力をユーザーに求めることができます。  
  
 レポート定義の各データ ソース定義では、名前および接続文字列のほか、統合セキュリティを使用するかどうかと、必要な資格情報が指定されなかった場合にどんなプロンプトを表示するかを指定します。 資格情報は、レポート定義に保存されません。 レポートがレポート サーバー上でパブリッシュされると、その後はデータ ソースをレポート定義とは別に管理できます。 データ ソースの所有者は、レポート サーバー上の埋め込みデータ ソースと共有データ ソースの両方に対して資格情報を指定できます。  
  
> [!NOTE]  
>  レポート サーバーの管理者は、レポート サーバーを参照して共有データ ソースまたはモデルを選択する操作や、レポートを開く操作または保存する操作を実行するための適切な権限をユーザーに許可する必要があります。 詳細については、次を参照してください。[インストール、アンインストール、およびレポート ビルダーのサポート](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-when-credentials-are-used"></a>資格情報が使用されるタイミングについて  
 レポート ビルダーでは、資格情報はレポート サーバーに接続するときと、埋め込みデータ ソースの作成、データセット クエリの実行、レポートのプレビューなどのデータ関連タスクに使用されます。 資格情報はレポートに格納されません。 資格情報は、レポート サーバー上またはローカル クライアント上で個別に管理されます。 次の一覧に、指定する必要がある資格情報の種類、それらの資格情報の格納場所、およびそれらの資格情報の使用方法を示します。  
  
-   [[Reporting Services ログイン] ダイアログ ボックス &#40;レポート ビルダー&#41;](report-builder/reporting-services-login-dialog-box-report-builder.md) で入力するレポート サーバーの資格情報。  
  
     レポート サーバーまたは SharePoint サイトに対して最初に保存、パブリッシュ、または参照を実行するとき、資格情報を入力する必要がある場合があります。 入力した資格情報は、レポート ビルダー セッションが終了するまで使用されます。 資格情報の保存を選択した場合、資格情報はユーザー設定と共に、使用しているコンピューターに安全に格納されます。 以降のレポート ビルダー セッションでは、同じレポート サーバーまたは SharePoint サイトへの接続に、保存した資格情報が使用されます。 レポート サーバーの管理者または SharePoint 管理者は、使用する資格情報を指定します。  
  
-   埋め込みデータ ソースの [[資格情報] &#40;[データ ソースのプロパティ] ダイアログ ボックス&#41; &#40;レポート ビルダー&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md) ページで入力するデータ ソースの資格情報。  
  
     これらの資格情報は、外部データ ソースへのデータ接続を行うために、レポート サーバーによって使用されます。 一部の種類のデータ ソース用に、資格情報をレポート サーバーに安全に格納できます。 これらの資格情報により、他のユーザーは基になるデータ接続の資格情報を指定することなく、レポートを実行できます。  
  
-   データセット クエリの実行時、データセット フィールドの更新時、またはレポートのプレビュー時に [[データ ソースの資格情報の入力] ダイアログ ボックス &#40;レポート ビルダー&#41;](report-data/enter-data-source-credentials-dialog-box-report-builder.md) で入力するデータ ソースの資格情報。  
  
     これらの資格情報は、レポート ビルダーから外部データ ソースにデータ接続を行うために、または資格情報の入力を求めるように構成されたレポートをプレビューするために使用されます。 このダイアログ ボックスで入力した資格情報は、レポート サーバーに格納されず、他のユーザーが使用することはできません。 レポート ビルダーは、クエリの実行またはレポートのプレビューのたびに資格情報を入力しなくても済むように、レポート編集セッション中に資格情報をキャッシュします。  
  
     共有データ ソースの場合は、 **[パスワードを保存する]** オプションを使用して、資格情報をユーザー設定と共に、使用しているコンピューターにローカルに保存します。 レポート ビルダーは、対応する外部データ ソースに接続するたびに、保存されている資格情報を使用します。  
  
 詳細については、「[[全般] &#40;[データ ソースのプロパティ] ダイアログ ボックス&#41; &#40;レポート ビルダー&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)」および「[レポート ビルダーでのレポートのプレビュー](report-builder/previewing-reports-in-report-builder.md)」を参照してください。  
  
## <a name="types-of-credentials"></a>資格情報の種類  
 データ ソースでサポートされる資格情報の種類は、データ ソースの所有者によって指定されます。 たとえば、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースにアクセスするために、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のログイン ユーザー名とパスワードの入力が必要になる場合があります。 また、別のデータ ソースにアクセスする際には、Windows ユーザー名とパスワードが必要になる場合もあります。 資格情報が必要とされないデータ ソースもあります。  
  
### <a name="options-for-specifying-credentials"></a>資格情報を指定するためのオプション  
 データ ソースの資格情報の指定に関しては、次のオプションがあります。  
  
-   現在の Windows ユーザー (統合セキュリティとも呼ばれます) を使用する。  
  
-   保存されているユーザー名とパスワードを使用する。  
  
-   ユーザーに資格情報を要求する。  
  
-   資格情報を必要としない。  
  
### <a name="windows-integrated-security"></a>Windows 統合セキュリティ  
 **[Windows 認証 (統合セキュリティ) を使用する]** を選択した場合は、現在のユーザーのセキュリティ トークンがデータ ソースに渡されます。 この場合、ユーザーはユーザー名やパスワードを入力することを要求されません。 通常、このオプションでは、委任機能が有効になっている必要があります。 委任機能が有効でない場合は、同じコンピューターに配置されているデータ ソースにアクセスする場合にのみ、このオプションを使用できます。  
  
### <a name="user-name-and-password-login"></a>ユーザー名とパスワードによるログイン  
 **[次のユーザー名とパスワードを使用]** を選択した場合、データ ソースへのアクセスにはユーザー名およびパスワードの指定が必要になります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースの場合は、この資格情報がデータベース ログイン用となる可能性があります。 この資格情報は、認証用にデータ ソースに渡されます。  
  
### <a name="prompted-credentials"></a>資格情報の要求  
 資格情報の要求を指定した場合、レポートにアクセスするユーザーがデータを取得するには、それぞれがユーザー名とパスワードを入力する必要があります。 機密データを含むレポートには、このオプションを使用することをお勧めします。 要求される資格情報は、Windows アカウントまたはデータベース ログインのいずれかです。 指定した資格情報がデータベース サーバーによって認識されない場合や、指定したユーザーにデータを取得するための権限が与えられていない場合、接続は失敗します。  
  
### <a name="no-credentials"></a>資格情報を使用しない  
 このデータ ソースでは資格情報が必要とされません。 レポート サーバー上でこのレポートを実行するには、自動実行用のアカウントを構成する必要があります。 詳細については、次を参照してください。[自動実行アカウントを構成する&#40;SSRS 構成マネージャー&#41; ](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)で、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]ドキュメント[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][オンライン ブックの「](https://go.microsoft.com/fwlink/?linkid=121312)します。  
  
## <a name="see-also"></a>参照  
 [インストール、アンインストール、およびレポート ビルダーのサポート](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)   
 [埋め込みおよび共有のデータ接続またはデータ ソース (レポート ビルダーおよび SSRS)](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [レポート ビルダーのオプション ダイアログ ボックスで、設定&#40;レポート ビルダー&#41;](report-builder/set-default-options-for-report-builder.md)   
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
  
