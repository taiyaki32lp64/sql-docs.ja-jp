---
title: Reporting Services の電子メール配信 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b2d5f511fe6008801b25f7c93300911851482025
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305044"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Reporting Services の電子メール配信
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、個別のユーザーまたはグループに電子メールでレポートを送信するための電子メール配信拡張機能があります。 電子メールでレポートを配信するには、1) 電子メール配信のレポート サーバーを構成し、2) 標準のサブスクリプションまたはデータ ドリブン サブスクリプションのいずれかを定義します。 単一のサブスクリプションでは、1 通の電子メール メッセージで複数のレポートを配信できません。 ただし、複数のサブスクリプションを作成することはできます。  
  
 レポート サーバーは、標準の接続を介して電子メール サーバーに接続します。 SSL (Secure Sockets Layer) を使用して暗号化された通信は使用しません。 電子メール サーバーは、レポート サーバーと同じネットワーク上にあるリモートまたはローカルの簡易メール転送プロトコル (SMTP) サーバーである必要があります。  
  
 サブスクリプションを作成する詳細な手順については、次を参照してください。  
  
-   [ネイティブ モード レポート サーバーのサブスクリプションの作成と管理](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [SharePoint モード レポート サーバーのサブスクリプションの作成と管理](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード|  
  
## <a name="e-mail-delivery-options"></a>電子メール配信のオプション  
 レポート サーバーの電子メール配信では、以下の方法でレポートを配信できます  
  
-   生成されたレポートに通知およびハイパーリンクを送信します。  
  
-   電子メール メッセージの [件名] 行を使用して通知を送信します。 既定では、サブスクリプション定義の [件名] に以下の変数が含まれます。サブスクリプションが処理されると、これらの変数はレポート固有の情報に置き換えられます。  
  
     **\@ReportName** は、レポート名を指定します。  
  
     **\@ExecutionTime** は、レポートが実行された時間を指定します。  
  
     これらの変数に静的なテキストを追加したり、各サブスクリプションの [件名] のテキストを変更することができます。  
  
-   埋め込みレポートまたは添付レポートを送信します。 表示形式およびブラウザーによって、レポートが埋め込まれるか添付されるかが決まります。  
  
     ブラウザーが HTML 4.0 および MHTML をサポートする場合、Web アーカイブ表示形式を選択すると、レポートがメッセージの一部として埋め込まれます。 その他すべての表示形式 (CSV、PDF など) では、添付ファイルとしてレポートを配信します。 ネイティブ モードのレポート サーバーについては、RSReportServer.config 構成ファイルでこの機能を無効にできます。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポートを送信する前に、添付ファイルまたはメッセージのサイズを確認しません。 添付ファイルまたはメッセージがメール サーバーで許可された最大サイズを超えると、レポートは配信されません。 レポートが大きい場合は、他の配信オプション (URL や通知など) のいずれかを選択します。  
  
 サブスクリプションを作成したときにレポートをどのように配信するかを決定する配信オプションを設定します。 たとえば、サブスクリプションで **[リンクを含める]** を選択すると、電子メール メッセージには、レポートへのハイパーリンクが含まれます。  
  
## <a name="native-mode-role-based-e-mail-settings"></a>ネイティブ モード ロールベースの電子メール設定  
 ネイティブ モードのレポート サーバー環境では、作業に使用する電子メール配信の設定は、ロールに "個別のサブスクリプションを管理" タスクが含まれるか、"すべてのサブスクリプションを管理" タスクが含まれるかによって異なります。  
  
|タスク|使用可能な設定|  
|----------|------------------------|  
|個別のサブスクリプションを管理|ユーザーが自分自身に対するレポートの配信を自動化できるようにするフィールドを示します。 このモードでは、電子メールの別名を受け取るフィールドは使用できません。|  
|すべてのサブスクリプションを管理|[宛先] フィールド、[CC] フィールド、[BCC] フィールド、[返信先] フィールドなど、より広範囲な配信をサポートするフィールドを示します。これらのフィールドを使用すると、より多くのサブスクライバーにレポートを送信できます。 電子メールの別名のフィールドの可用性は、RSReportServer 構成ファイルの設定で定義されます。|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>サブスクリプションへの電子メール アドレスの指定  
 イントラネット内部でレポートを配信し、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange サーバーに SMTP ゲートウェイを使用している場合、同僚に電子メールを送信するときと同様に、電子メールの別名を入力します。 配信が外部の電子メール アカウントに対して行われている場合は、完全な電子メール アドレスを入力します。 さらに電子メール アドレスを指定して、他のユーザーをサブスクリプションに追加すると、サブスクライバーは、このサブスクリプションから生成されるレポートの正確なコピーを取得します。  
  
 レポート サーバーは、電子メール アドレスの検証または電子メール サーバーからの電子メール アドレスの取得を行いません。 使用する電子メール アドレスを事前に把握する必要があります。 既定では、組織内部または組織外にある有効な電子メール アカウントに電子メールでレポートを送信することができます。 ただし、構成設定を使用して、名前で特定されるメール サーバー ホストに電子メールの配信を制限することができます。 組織のメンバー以外のユーザーへの電子メール配信をサポートする場合、追加のホストを指定することができます。  
  
 レポートの配信に使用する電子メール メッセージは、電子メール サーバーで定義される電子メール アカウントから送信する必要があります。 構成設定では、電子メール アカウントを指定します。 電子メール アカウントは、電子メール配信拡張機能で配信されるすべてのレポートに使用されます。つまり、複数のアカウントを指定したり、レポートごとにアカウントを変更することができません。  
  
## <a name="controlling-e-mail-delivery"></a>電子メール配信の制御  
 特定のホスト ドメインへの電子メールの配信を制限するようにレポート サーバーを構成できます。 たとえば、 **RSReportServer.config** 構成ファイルに一覧されたドメインを除くすべてのドメインに、ネイティブ レポート サーバーからレポートが配信されないようにすることができます。  
  
 また、サブスクリプションの **[宛先]** フィールドを非表示にするように構成を設定することもできます。 この場合、レポートは、サブスクリプションを定義するユーザーにのみ配信されます。 ただし、レポートがユーザーに送信された後で、このレポートが転送されることを明示的に防ぐことはできません。  
  
 レポートの配信を制御する最も効果的な方法は、レポート サーバーからレポート サーバーの URL のみを送信するように構成することです。 レポート サーバーでは、Windows 認証およびロールベースの承認モデルを使用して、レポートへのアクセスを制御します。 ユーザーが表示権限のないレポートを電子メールで誤って受信しても、レポート サーバーはレポートを表示しません。 サブスクリプションの詳細については、次を参照してください。  
  
## <a name="e-mail-server-configuration"></a>電子メール サーバーの構成  
 ネイティブ モード レポート サーバーの場合、電子メール配信拡張機能は、ネイティブ モード [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ファイルを編集することで構成されます。 SharePoint モード レポート サーバーの場合、電子メール配信拡張機能は、SharePoint 管理ページと PowerShell スクリプトで構成されます。  
  
 
 ネイティブ モードのレポート サーバーを構成する方法については、「 [電子メールの設定 - Reporting Services のネイティブ モード (構成マネージャー)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)」を参照してください。
 
 
 SharePoint モード レポート サーバーの構成方法については、次のトピックを参照してください。  
  
  
## <a name="see-also"></a>参照  
 [タスクと権限](../../reporting-services/security/tasks-and-permissions.md)   
 [サブスクリプションと配信 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [データ ドリブン サブスクリプション](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [ロールの割り当て](../../reporting-services/security/role-assignments.md)  
  
  
