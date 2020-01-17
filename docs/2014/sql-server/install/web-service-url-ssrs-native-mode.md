---
title: Web サービス URL (SSRS ネイティブモード) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.reportservervirtualdirectory.F1
helpviewer_keywords:
- Reporting Services, Web service
ms.assetid: 9d210b5d-2a08-4e56-a4f5-c16715b00d79
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 01e5393ae638ddcecd04211a0a7e01e8116346a9
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952359"
---
# <a name="web-service-url-ssrs-native-mode"></a>Web サービス URL (SSRS ネイティブ モード)
  [Web サービス URL] ページを使用すると、レポート サーバーへのアクセスに使用する URL を構成または変更できます。 *URL 予約* は、指定した URL に基づいて作成されます。 URL 予約は、その後のレポート サーバー Web サービスへのアクセスに使用できるすべての URL の構文と規則を定義し、 レポート サーバー Web サービスのプレフィックス、ホスト、ポート、および仮想ディレクトリを指定します。 ホストの指定方法によっては、1 つの予約で複数の URL を定義できます。 ホストの既定値では、強いワイルドカードが指定されます。 強いワイルドカードを使用すると、レポート サーバーをホストするコンピューターに解決できるあらゆるホスト名を URL に指定できます。 構成と URL 予約の詳細については、次を参照してください[URL の構成&#40;SSRS 構成マネージャー&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)と[レポート サーバー Url の構成&#40;SSRS 構成マネージャー&#41; ](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
 このページを開くには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを起動して、ナビゲーション ウィンドウで **[Web サービス URL]** をクリックします。 詳細については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
 このページには、レポート サーバーの URL で一般的に使用される値が表示されます。 追加の URL を作成する場合、ホスト ヘッダーを使用する場合、または IP アドレスを特定の形式で指定する場合は、 **[詳細設定]** をクリックします。  
  
 **[適用]** をクリックすると、このページに Web サービスへのリンクが表示されます。 レポート サーバー データベースの作成前にこのリンクをクリックすると、"ページが見つかりません" というエラーが表示されます。 このエラーは、データベースを構成すると表示されなくなります。 詳細については、「[ネイティブ モードのレポート サーバー データベースの作成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)」を参照してください。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を再インストールした場合に、[すべて割り当て] の既定の IP アドレス値とポート 80 を使用しようとするとエラーが表示されるときは、通常、サービスの再起動後に URL を再作成することによってエラーを解決できます。  
  
## <a name="options"></a>および  
 **仮想ディレクトリ**  
 レポート サーバー Web サービスの仮想ディレクトリ名を指定します。 仮想名は、同じコンピューター上のレポート サーバー Web サービス インスタンスごとに 1 つだけ指定できます。  
  
 **[IP アドレス]**  
 TCP/IP ネットワーク上でレポート サーバー コンピューターを識別します。 有効な値は次のとおりです。  
  
-   **[すべて割り当て]** は、レポート サーバー アプリケーションを指す URL に、コンピューターに割り当てられている IP アドレスをどれでも使用できることを示します。 コンピューターに割り当てられている IP アドレスに対してドメイン ネーム サーバーによって解決されるわかりやすいホスト名 (コンピューター名など) も、この値の対象に含まれます。 これは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL の既定値です。  
  
-   **[すべて未割り当て]** は、IP アドレスまたはホスト名が正確に一致しない要求をレポート サーバーがすべて受け入れることを示します。 別の Web アプリケーションが既に使用している場合は、この値を使用しないでください。 使用すると、他のアプリケーションのサービスが中断されます。  
  
-   **[127.0.0.1]** は、localhost にアクセスする場合に使用します。 この値は、レポート サーバー コンピューターでのローカル管理をサポートします。 この値のみを選択すると、レポート サーバー コンピューターにローカルにログオンしているユーザーだけがアプリケーションにアクセスできるようになります。  
  
-   "*nnn.nnn.nnn.nnn* " は、コンピューターのネットワーク アダプター カードの IPv4 アドレスです。 ネットワークで IPv6 アドレス指定が使用されている場合、IP アドレスは 8 4 バイトの128ビット値になります。 \<header >:*nnnn: nnnn: nnnn: nnnn*という形式になります。  
  
     複数のカードがある場合は、それぞれに IP アドレスが割り当てられます。 この値のみを選択すると、アプリケーション アクセスがその IP アドレス (およびドメイン ネーム サーバーによってそのアドレスにマップされるホスト名) に限定されます。 localhost を使用してレポート サーバーにアクセスすることはできません。また、レポート サーバー コンピューターにインストールされている他のネットワーク アダプター カードの IP アドレスは使用できません。  
  
 **[TCP ポート]**  
 レポート サーバーの仮想ディレクトリ名を含む URL に対する HTTP 要求をレポート サーバーが監視するポートを指定します。  
  
 **[SSL 証明書]**  
 指定した IP アドレスに証明書をバインドします。 証明書をコンピューターにインストールして構成する必要があります。 Reporting Services には証明書の管理機能は用意されていません。 証明書は、IP アドレスに解決されるホスト名またはコンピューター名に対して発行されている必要があります。 たとえば、発行された証明書を使用する http://salesreports 、指定した IP アドレスが"salesreports"という名前のサーバーに解決する必要があります。  
  
 証明書を使用する場合は、RSReportServer.config ファイルの `UrlRoot` 構成設定を、証明書で登録されたコンピューターの完全修飾名を指すように変更する必要があります。 詳細については、 [オンライン ブックの「](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) ネイティブ モードのレポート サーバーでの SSL 接続の構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
 **[SSL ポート]**  
 SSL 接続のポートを指定します。  
  
 **ハイパーリンク**  
 現在のレポート サーバー インスタンスに対して定義されている URL が表示されます。  
  
 **詳細設定**  
 現在のアプリケーション インスタンスの追加の URL を作成する場合にクリックします。  
  
> [!NOTE]
>  既存の SSL バインドと URL 予約があり、SSL バインドを変更する (たとえば、別の証明書やホスト ヘッダーを使用する) 場合、次の手順を順番に実行することをお勧めします。  
> 
>  1.  まず、すべての URL 予約を削除します。  
> 2.  すべての SSL バインドを削除します。  
> 3.  URL と SSL バインドを作成し直します。  
> 
>  前の手順は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して行うことができます。  
> 
>  Microsoft Windows では、IP アドレスとポートの組み合わせごとに 1 つのバインドがサポートされています。 特定のホスト ヘッダー値を使用するようにレポート サーバーを構成し、ポートと IP アドレスの組み合わせに対する証明書が別のホスト ヘッダー値にも発行される場合、証明書と使用中の URL が一致しないことを示す警告がブラウザーに表示されます。  
> 
>  この問題を修正するには、すべてのバインドを削除し、一意の設定で新しいバインドを作成するか、ワイルドカードを使用して Reporting Services の URL 登録を構成してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services Configuration Manager の F1 ヘルプ&#40;トピック SSRS ネイティブ&#41;モード](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
