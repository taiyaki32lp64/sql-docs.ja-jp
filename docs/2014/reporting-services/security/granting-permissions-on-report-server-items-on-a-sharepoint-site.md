---
title: SharePoint サイトのレポート サーバー アイテムに対するアクセス許可の付与 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aa11481ed3c446becf2519a2ed149867456ac94a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101926"
---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>SharePoint サイトのレポート サーバー アイテムに対する権限の付与
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] は、SharePoint のサイトおよびライブラリにあるレポート サーバー アイテムへのアクセス許可に使用できる、組み込みのセキュリティ機能を提供します。 既にユーザーに権限を割り当てている場合、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] とレポート サーバーの統合設定を構成すると、直ちにそのユーザーがレポート サーバーのアイテムおよび操作にアクセスできるようになります。 既存の権限を使用して、レポート定義などのドキュメントのアップロード、レポートの表示、サブスクリプションの作成、アイテムの管理を実行できます。  
  
 権限をまだ割り当てていない場合、または [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]のセキュリティ機能の設定方法がわからない場合には、次のガイドラインに従ってください。  
  
1.  [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]の製品マニュアルで、標準的な SharePoint グループの既定のセキュリティ設定に関する説明に目を通し、権限とユーザー アクセスの管理方法を理解します。  
  
2.  レポート サーバーのアイテムと操作に対するアクセスに特に影響する権限を確認します。 詳細については、「 [レポート サーバー アイテムに対して Windows SharePoint Services の組み込みのセキュリティを使用する](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)」を参照してください。  
  
3.  定義済みの SharePoint グループに、ユーザー アカウントとグループ アカウントを割り当てます。  
  
4.  特定の必要性が生じた場合には、新しい権限レベルとグループを作成するか、既存の権限レベルとグループを変更して、サーバー アクセス権限を変更します。  
  
 レポート サーバー アイテムに [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] セキュリティ機能を使用するには、SharePoint 統合モードで動作するレポート サーバーが必要です。  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>権限、権限レベル、および SharePoint グループについて  
 次に、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]のセキュリティ機能を簡単に説明します。 詳細については、SharePoint サイトで Windows SharePoint ヘルプを参照してください。  
  
-   セキュリティ保護できるオブジェクトには、サイト、リスト、ライブラリ、フォルダー、ドキュメントなどがあります。  
  
-   権限とは、特定のタスクを実行するための許可を意味します。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] では 33 の権限があらかじめ定義されているので、それを組み合わせて権限レベルを設定します。  
  
-   権限レベルとは、サイト、ライブラリ、リスト、フォルダー、アイテム、ドキュメントなどのセキュリティ保護可能オブジェクトに関して、ユーザーまたは SharePoint グループに許可できる一連の権限です。 これは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]におけるロール定義に相当します。 あらかじめ 5 種類の権限レベルが定義されています。 必要に応じてそれをカスタマイズすることも、新規に作成することもできます。  
  
-   SharePoint グループとは、SharePoint サイトに対する権限を管理するために、またサイトのメンバーへの電子メール配信リストを作成するために、SharePoint サイトで作成できるユーザー グループです。 SharePoint グループは Windows のユーザー アカウントおよびグループ アカウント (フォーム認証を使用する場合はユーザー ログイン) で構成されます。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] には 3 つのグループがあります。 必要に応じてそれをカスタマイズすることも、新規に作成することもできます。  
  
-   権限の継承を利用することで、サブサイト、リスト、ライブラリ、およびアイテムで親サイトのセキュリティ設定を継承することができます。 継承された権限を使用して、SharePoint ライブラリに格納されているレポート サーバー アイテムにアクセスできます。 権限の継承と定義済み SharePoint グループを使用することで、配置が単純化され、ほとんどのレポート サーバー操作にすぐにアクセスできるようになります。  
  
## <a name="who-sets-permissions"></a>権限の設定者  
 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]をインストールし、SharePoint 構成ウィザードを実行し、ポータル サイトを作成した管理者は、既定のポータル サイト所有者になります。 サイト所有者は、ファームまたはスタンドアロンの SharePoint Web アプリケーションの権限をサーバー管理で設定でき、各 SharePoint Web アプリケーションのトップレベル サイトで権限を設定できます。 さらに、追加のサイト所有者を指定することもできます。  
  
 SharePoint Web アプリケーションのトップレベル サイトでは、サイト コレクション管理者がサイト階層全体で複数のサイトに対して権限を設定できます。 個々のサイトの所有者は、同じ操作をサブサイトに対して実行できます。  
  
 サーバー管理者またはサイト コレクション管理者は、他のサイト所有者が権限を設定できるかどうかを決定するオプションを設定できます。 持っている権限のレベルによっては、SharePoint グループや権限レベルの作成やカスタマイズを行えない場合があります。  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>定義済み SharePoint グループと権限レベルの使用  
 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 製品マニュアルでは、標準の SharePoint グループ ( *Site name* **所有者**, *Site name* **メンバー**、および *Site name* **閲覧者**) を使用し、サイト レベルで権限を割り当てることが推奨されています。 権限を割り当てるユーザーのほとんどは、" *Site name* **閲覧者** " グループまたは " *Site name* **メンバー** "グループのメンバーになるはずです。 親サイトの権限は、サイト階層全体に継承されます。 制限を追加する必要がある特定のアイテムに対しては、権限の継承を無効にできます。  
  
 定義済みの SharePoint グループと、対応する権限レベルを次に示します。  
  
-   **所有者** グループにはフル コントロール権限が与えられるので、このグループ メンバーは、サイトのコンテンツ、ページ、または機能を変更できます。 フル コントロールのアクセスは、サイト管理者のみに制限する必要があります。  
  
-   **メンバー** グループには投稿レベルの権限が与えられます。このグループのメンバーは、ページの表示、アイテムの編集、変更の送信による承認の要求、リストへのアイテムの追加と削除を実行できます。  
  
-   **閲覧者** グループには読み取りレベルの権限が与えられます。グループ メンバーは、ページ、リスト アイテム、およびドキュメントを表示できます。  
  
 SharePoint グループには、多数のレポート サーバー操作にすぐにアクセスできるようにするための権限レベルが用意されています。 必要なアクセス レベルを提供する組み込みセキュリティ設定がない場合には、カスタム グループまたはカスタム権限レベルを作成できます。  
  
 既定のセキュリティ機能によってサポートされるレポート サーバー操作の詳細については、「 [レポート サーバー アイテムに対して Windows SharePoint Services の組み込みのセキュリティを使用する](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)」を参照してください。  
  
 組み込みセキュリティ機能を使用するには、SharePoint グループに Windows ユーザー アカウントまたはグループ アカウントを割り当てる必要があります。 ソフトウェアのインストール時に [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] へのアクセスが自動的に与えられるサーバー管理者およびポータル サイト所有者を除いて、すべてのユーザーにこのサーバーへのアクセスを許可する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レポート サーバー アイテムに対して Windows SharePoint Services の組み込みのセキュリティを使用する](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 定義済みの SharePoint グループと権限レベルを使用してレポート サーバー アイテムにアクセスする方法を説明します。  
  
 [レポート サーバー アイテムの SharePoint サイトおよびリスト権限のリファレンス](sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 レポート サーバー操作へのアクセスに使用できるすべての SharePoint 製品権限のリファレンスです。  
  
 [SharePoint Web アプリケーションのレポート サーバー操作に対する権限を設定する](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 カスタム レポートに必要な権限と、機能を利用できるようにするための手法について説明します。  
  
 [Compare Roles and Tasks in Reporting Services to SharePoint Groups and Permissions](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 SharePoint グループを [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の定義済みロール定義と比較する方法の概要を説明します。  
  
 [SharePoint サイト上のレポート サーバー アイテムに対する権限の設定 (Reporting Services の SharePoint 統合モード)](set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 レポート ビルダーを起動してモデル アイテム セキュリティを設定するための権限を持つ、新しい SharePoint グループを作成する方法を示します。 このトピックでは、レポート サーバーの任意のアイテムまたは操作にカスタム権限を設定する際の一般的ガイドラインも示します。  
  
## <a name="see-also"></a>参照  
 [SharePoint サイト上のレポート サーバー アイテムに対する権限の設定 (Reporting Services の SharePoint 統合モード)](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services のセキュリティと保護](reporting-services-security-and-protection.md)  
  
  
