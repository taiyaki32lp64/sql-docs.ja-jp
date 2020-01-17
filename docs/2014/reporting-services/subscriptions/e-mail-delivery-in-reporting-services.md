---
title: Reporting Services の電子メール配信 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68024e36dd5f8188097ebcc673056c1b6d11e59b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100886"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Reporting Services の電子メール配信
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、個別のユーザーまたはグループに電子メールでレポートを送信するための電子メール配信拡張機能があります。 電子メール配信拡張機能を構成するには、Reporting Services 構成マネージャーを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ファイルを編集します。  
  
 電子メールでレポートを配信または受信するには、標準のサブスクリプションまたはデータ ドリブン サブスクリプションのいずれかを定義します。 サブスクライブまたは配信は、一度に 1 つのレポートに対してのみ実行できます。 1 通の電子メール メッセージで複数のレポートを配信するサブスクリプションを作成することはできません。 サブスクリプションの詳細については、次を参照してください。 [Create, Modify, and 標準サブスクリプションの削除&#40;Reporting Services ネイティブ モードの&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)します。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード&#124;SharePoint 2010 および SharePoint 2013<br /><br /> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード|  
  
## <a name="e-mail-delivery-options"></a>電子メール配信のオプション  
 レポート サーバーの電子メール配信では、以下の方法でレポートを配信できます。  
  
-   生成されたレポートに通知およびハイパーリンクを送信します。  
  
-   電子メール メッセージの [件名] 行を使用して通知を送信します。 既定では、サブスクリプション定義の [件名] に以下の変数が含まれます。サブスクリプションが処理されると、これらの変数はレポート固有の情報に置き換えられます。  
  
     **@ReportName** は、レポート名を指定します。  
  
     **@ExecutionTime** は、レポートが実行された時間を指定します。  
  
     これらの変数に静的なテキストを追加したり、各サブスクリプションの [件名] のテキストを変更することができます。  
  
-   埋め込みレポートまたは添付レポートを送信します。 表示形式およびブラウザーによって、レポートが埋め込まれるか添付されるかが決まります。  
  
     ブラウザーが HTML 4.0 および MHTML をサポートする場合、Web アーカイブ表示形式を選択すると、レポートがメッセージの一部として埋め込まれます。 その他すべての表示形式 (CSV、PDF など) では、添付ファイルとしてレポートを配信します。 RSReportServer 構成ファイルでこの機能を無効にすることができます。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポートを送信する前に、添付ファイルまたはメッセージのサイズを確認しません。 添付ファイルまたはメッセージがメール サーバーで許可された最大サイズを超えると、レポートは配信されません。 レポートが大きい場合は、他の配信オプション (URL や通知など) のいずれかを選択します。  
  
 サブスクリプションを作成したときにレポートをどのように配信するかを決定する配信オプションを設定します。 たとえば、サブスクリプションで **[リンクを含める]** を選択すると、電子メール メッセージには、レポートへのハイパーリンクが含まれます。  
  
## <a name="role-based-e-mail-settings"></a>ロールベースの電子メール設定  
 レポートをサブスクライブする場合、作業に使用する電子メール配信の設定は、ロールに "個別のサブスクリプションを管理" タスクが含まれるか、"すべてのサブスクリプションを管理" タスクが含まれるかによって異なります。  
  
|タスク|使用可能な設定|  
|----------|------------------------|  
|個別のサブスクリプションを管理|ユーザーが自分自身に対するレポートの配信を自動化できるようにするフィールドを示します。 このモードでは、電子メールの別名を受け取るフィールドは使用できません。|  
|すべてのサブスクリプションを管理|[宛先] フィールド、[CC] フィールド、[BCC] フィールド、[返信先] フィールドなど、より広範囲な配信をサポートするフィールドを示します。これらのフィールドを使用すると、より多くのサブスクライバーにレポートを送信できます。 電子メールの別名のフィールドの可用性は、RSReportServer 構成ファイルの設定で定義されます。|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>サブスクリプションへの電子メール アドレスの指定  
 イントラネット内部でレポートを配信し、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange サーバーに SMTP ゲートウェイを使用している場合、同僚に電子メールを送信するときと同様に、電子メールの別名を入力します。 配信が外部の電子メール アカウントに対して行われている場合は、完全な電子メール アドレスを入力します。 さらに電子メール アドレスを指定して、他のユーザーをサブスクリプションに追加すると、サブスクライバーは、このサブスクリプションから生成されるレポートの正確なコピーを取得します。  
  
 レポート サーバーは、電子メール アドレスの検証または電子メール サーバーからの電子メール アドレスの取得を行いません。 使用する電子メール アドレスを事前に把握する必要があります。 既定では、組織内部または組織外にある有効な電子メール アカウントに電子メールでレポートを送信することができます。 ただし、構成設定を使用して、名前で特定されるメール サーバー ホストに電子メールの配信を制限することができます。 組織のメンバー以外のユーザーへの電子メール配信をサポートする場合、追加のホストを指定することができます。  
  
 レポートの配信に使用する電子メール メッセージは、電子メール サーバーで定義される電子メール アカウントから送信する必要があります。 構成設定では、電子メール アカウントを指定します。 電子メール アカウントは、電子メール配信拡張機能で配信されるすべてのレポートに使用されます。つまり、複数のアカウントを指定したり、レポートごとにアカウントを変更することができません。  
  
## <a name="e-mail-server-configuration"></a>電子メール サーバーの構成  
 レポート サーバーは、標準の接続を介して電子メール サーバーに接続します。 SSL (Secure Sockets Layer) を使用して暗号化された通信は使用しません。 電子メール サーバーは、レポート サーバーと同じネットワーク上にあるリモートまたはローカルの簡易メール転送プロトコル (SMTP) サーバーである必要があります。  
  
 ネイティブ モード レポート サーバーの構成方法については、次のトピックを参照してください。  
  
-   [レポート サーバー電子メール配信用に構成&#40;SSRS 構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
  
-   [電子メールの設定 - Configuration Manager &#40;SSRS ネイティブ モード&#41;](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
  
 SharePoint モード レポート サーバーの構成方法については、次のトピックを参照してください。  
  
-   [Reporting Services サービス アプリケーションの電子メールの構成 (SharePoint 2010 および SharePoint 2013)](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
## <a name="see-also"></a>参照  
 [タスクと権限](../security/tasks-and-permissions.md)   
 [サブスクリプションと配信 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [データ ドリブン サブスクリプション](data-driven-subscriptions.md)   
 [ロールの割り当て](../security/role-assignments.md)  
  
  
