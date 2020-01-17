---
title: Reporting Services とインターネット インフォメーション サービスのサイド バイ サイド インストール | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b854add44b256078cd19963f2ef22d55a7b3d300
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "64330630"
---
# <a name="install-reporting-and-internet-information-services-side-by-side"></a>Reporting Services とインターネット インフォメーション サービスのサイド バイ サイド インストール

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services (SSRS) とインターネット インフォメーション サービス (IIS) は、同じコンピューターにインストールして実行できます。 対処する必要のある相互運用性の問題は、使用している IIS のバージョンによって異なります。  
  
|IIS のバージョン|問題|[説明]|  
|-----------------|------------|-----------------|  
|8.0, 8.5|あるアプリケーションに対して送信された要求が、別のアプリケーションによって受け付けられます。<br /><br /> URL 予約には、HTTP.SYS による優先順位規則が適用されます。 同じ仮想ディレクトリ名を持ち、共にポート 80 を監視するアプリケーションが複数存在するとき、これらのアプリケーションに宛てて送信された要求は、目的のアプリケーションの URL 予約が、もう一方のアプリケーションの URL 予約よりもあいまいに指定されていた場合、意図したターゲットに到達しない可能性があります。|特定の条件下では、URL 予約体系において他の URL エンドポイントに優先する登録済みのエンドポイントが、他のアプリケーション宛ての HTTP 要求を受信する場合があります。<br /><br /> この競合は、レポート サーバー Web サービスおよび [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] に対し、一意の仮想ディレクトリ名を使用することによって回避できます。<br /><br /> このシナリオについては、このトピックで詳しく説明します。|  
  
## <a name="precedence-rules-for-url-reservations"></a>URL 予約の優先順位規則  
 IIS と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]間の相互運用性の問題を解決するには、まず URL 予約の優先順位規則を理解しておく必要があります。 優先順位規則とは、簡単に言えば、"より明示的に定義された値を持つ URL 予約が、その URL に合致した要求を先に受け取ることができる" ということです。  
  
-   仮想ディレクトリを指定する URL 予約は、仮想ディレクトリが省略された URL 予約よりも明示的である。  
  
-   単一アドレスが指定された URL 予約 (IP アドレス、完全修飾ドメイン名、ネットワーク コンピューター名、またはホスト名) は、ワイルドカードよりも明示的である。  
  
-   厳密なワイルドカードを指定する URL 予約は、弱いワイルドカードよりも明示的である。  
  
 次の表は、一連の URL 予約の例を、最も明示的なものから順に列挙したものです。  
  
|例|要求|  
|-------------|-------------|  
|`https://123.234.345.456:80/reports`|`https://123.234.345.456/reports` または (ドメイン名サービスが、IP アドレスを対応するホスト名に解決できる場合) `https://\<computername>/reports` に送信されたすべての要求が受信されます。|  
|`https://+:80/reports`|URL に "reports" という仮想ディレクトリ名が含まれている限り、任意の IP アドレス (またはそのコンピューターの有効なホスト名) に送信されたすべての要求が受信されます。|  
|`https://123.234.345.456:80`|`https://123.234.345.456` または (ドメイン名サービスが、IP アドレスを対応するホスト名に解決できる場合) `https://\<computername>` を指定するすべての要求が受信されます。|  
|`https://+:80`|**[すべて割り当て]** にマップされたすべてのアプリケーション エンドポイントについて、まだ他のアプリケーションによって受信されていない要求が受信されます。|  
|`https://*:80`|**[すべて未割り当て]** にマップされたアプリケーション エンドポイントについて、まだ他のアプリケーションによって受信されていない要求が受信されます。|  
  
 ポートが競合している場合は、「System.IO.FileLoadException: ファイルが別のプロセスで使用されているため、プロセスはファイルにアクセスできません (HRESULT からの例外: 0x80070020)」というエラー メッセージが表示されます。  
  
## <a name="url-reservations-for-iis-80-85-with-sql-server-reporting-services"></a>IIS 8.0、8.5 と SQL Server Reporting Services の URL 予約  
 前のセクションで取り上げた優先順位規則を踏まえて考えると、Reporting Services と IIS に対して定義された URL 予約が、両者の相互運用性にどのように貢献しているかがわかります。 Reporting Services は、そのアプリケーションの仮想ディレクトリ名を明示的に指定する要求を受信します。一方、IIS は、それ以外のすべての要求を受信し、それらを IIS のプロセス モデル内で実行されるアプリケーションに送ることになります。  
  
|アプリケーション|URL 予約|[説明]|受信する要求|  
|-----------------|---------------------|-----------------|---------------------|  
|レポート サーバー|`https://+:80/ReportServer`|厳密なワイルドカード、ポート 80、レポート サーバーの仮想ディレクトリ|レポート サーバーの仮想ディレクトリを指定するすべての要求をポート 80 で受信します。 https://\<コンピューター名>/reportserver に対するすべての要求が、レポート サーバー Web サービスによって受信されます。|  
|Web ポータル|`https://+:80/Reports`|厳密なワイルドカード、ポート 80、Reports という仮想ディレクトリ|reports という仮想ディレクトリを指定するすべての要求をポート 80 で受信します。 https://\<コンピューター名>/reports に対するすべての要求が [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]によって受信されます。|  
|IIS|`https://*:80/`|弱いワイルドカード、ポート 80|まだ他のアプリケーションによって受信されていない残りの要求をすべてポート 80 で受信します。|  

## <a name="side-by-side-deployments-of-sql-server-reporting-services-on-iis-80-85"></a>IIS 8.0、8.5 での SQL Server Reporting Services のサイド バイ サイド配置

 IIS と Reporting Services 間の相互運用性の問題は、IIS Web サイトに、Reporting Services で使用されているものと同じ仮想ディレクトリ名が存在する場合に発生します。 たとえば、次のような構成を考えてみます。  
  
-   ポート 80、仮想ディレクトリ名 "Reports" に割り当てられた IIS Web サイトが存在。  
  
-   レポート サーバー インスタンスを既定の構成でインストール。URL 予約でポート 80 を指定し、[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] アプリケーションで仮想ディレクトリ名 "Reports" を使用。  
  
 この構成では、 https://\<コンピューター名>:80/reports に送信された要求は、[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]によって受信されます。 レポート サーバー インスタンスのインストール後、IIS の Reports 仮想ディレクトリ経由でアクセスされるアプリケーションは、要求を受け取ることができなくなります。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の新旧のバージョンをサイド バイ サイド配置で実行した場合、前述したルーティングの問題が発生する可能性があります。 これは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のすべてのバージョンでは、レポート サーバーと [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] アプリケーションの仮想ディレクトリ名として "ReportServer" と "Reports" が使用されているため、IIS には "reports" と "reportserver" という仮想ディレクトリが高い確率で存在していると考えられるためです。  
  
 すべてのアプリケーションが確実に要求を受信できるようにするには、次のガイドラインに従います。  
  
-   Reporting Services のインストールでは、Reporting Services と同じポート上の IIS Web サイトで使用されていない仮想ディレクトリ名を使用するようにします。 競合が生じた場合は、Reporting Services を "ファイルのみ" のモード (インストール ウィザードで [サーバーを構成せずにインストールする] オプションを使用) でインストールします。こうすることで、セットアップの完了後に、仮想ディレクトリを自分で構成できるようになります。 構成が競合している場合は、「System.IO.FileLoadException: ファイルが別のプロセスで使用されているため、プロセスはファイルにアクセスできません (HRESULT からの例外: 0x80070020)」というエラー メッセージが表示されます。  
  
-   手動構成のインストールでは、構成する URL に既定の名前付け規則を採用します。 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] を名前付きインスタンスとしてインストールする場合は、仮想ディレクトリの作成時にインスタンス名を含めるようにします。  

## <a name="next-steps"></a>次の手順

[レポート サーバーの URL の構成](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[URL の構成](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Reporting Services ネイティブ モードのレポート サーバーのインストール](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
