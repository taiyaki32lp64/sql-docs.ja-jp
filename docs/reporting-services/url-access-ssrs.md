---
title: URL アクセス (SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services]
- links [Reporting Services], URL access
- URL access [Reporting Services], about URL access
- parameters [Reporting Services], URL access
- report servers [Reporting Services], URL access
- hyperlinks [Reporting Services]
ms.assetid: 52c3f2a3-3d6d-4fee-9c46-83f366919398
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a18ad4fd1d79bc7eae5f45318cece55037c78010
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574248"
---
# <a name="url-access-ssrs"></a>URL アクセス (SSRS)
  SQL Server Reporting Services (SSRS) のレポート サーバーの URL アクセスにより、URL 要求を使用してレポート サーバーにコマンドを送信できます。 たとえば、ネイティブ モードのレポート サーバーや SharePoint ライブラリのレポートの表示をカスタマイズすることができます。 特定のレポート パラメーター値のセットを使用してレポートを表示したり、レポートの関心のある特定ページを表示することがあります。 この情報を、事前に定義された URL アクセス パラメーターを使用して URL にカプセル化することができます。 表示形式またはレポート ビューアーのルック アンド フィールのパラメーターを埋め込むことで、レポート サーバーによるレポートの処理方法をさらにカスタマイズできます。 その後、この URL を電子メールまたは Web ページに直接貼り付けて、他のユーザーがブラウザーから同じ方法でレポートにアクセスできるようにすることができます。  
  
 URL アクセスを使用して実行できる他のアクションは次のとおりです。  
  
-   ルック アンド フィールの調節などのコマンドを HTML ビューアーに送信する  
  
-   カタログ フォルダーの子の一覧を表示する  
  
-   カタログ アイテムの XML 定義を取得する  
  
-   特例のレポート履歴スナップショットを表示する  
  
-   レポート セッションを管理する  
  
 URL アクセスにより使用できるコマンドおよび設定の完全な一覧については、「 [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md)」(URL アクセス パラメーター リファレンス) を参照してください。  
  
## <a name="url-access-concepts"></a>URL アクセスの概念  
 レポート サーバーに対する URL 要求には、レポート サーバーによって処理されるパラメーターが含まれます。 レポート サーバーが URL 要求を処理する方法は、URL に含まれるパラメーター、パラメーター プレフィックス、アイテムの種類によって異なります。 レポート サーバーの URL は、World Wide Web Consortium W3C/IETF 共同ドラフト仕様として提案されている URL フォーマット ガイドラインに準拠します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の URL 機能は、標準的な URL アドレス指定をサポートするほとんどのインターネット ブラウザーやアプリケーションと互換性があります。  
  
### <a name="url-access-syntax"></a>URL アクセスの構文  
 URL 要求には、任意の順序で一覧表示される複数のパラメーターを含めることができます。 パラメーターはアンパサンド (&) によって区切られ、名前と値のペアは等号 (=) によって区切られます。  
  
```  
  
rswebserviceurl  
?  
reportpath  
      [&prefix:param=value]...n]  
  
```  
  
### <a name="syntax-description"></a>構文の説明  
 *rswebserviceurl*  
 レポート サーバーの Web サービスの URL。 ネイティブ モードでは、Reporting Services Configuration Manager に構成されているレポート サーバー インスタンスの Web サービスの URL です (「[レポート サーバー URL の構成 (SSRS 構成マネージャー)](../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)」を参照してください)。 例:  
  
```  
https://myrshost/reportserver  
https://machine.adventure-works.com/reportserver_MYNAMEDINSTANCE  
```  
  
 SharePoint 統合モードでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] に統合された SharePoint サイトの [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]プロキシの URL です。 例:  
  
```  
https://myspsite/subsite/_vti_bin/reportserver  
```  
  
> [!TIP]  
>  SharePoint および `_vti_bin` HTTP プロキシ経由で要求をルーティングする [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] プロキシ構文を URL に含めることは重要です。 プロキシによって、HTTP 要求にいくつかのコンテキストが追加されます。これは、SharePoint モード レポート サーバーに対してレポートを適切に実行するために必要なコンテキストです。  
  
 *pathinfo*  
 ネイティブ モードのレポート サーバー データベース内のアイテムの相対パス名、または SharePoint カタログ内のアイテムの完全修飾 URL。  
  
 カタログ アイテムのパス。 ネイティブ モードでは、スラッシュ ( **/** ) から始まるレポート サーバー データベース内のアイテムの相対パスです。 例:  
  
```  
/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2  
```  
  
 SharePoint 統合モードでは、アイテムの拡張子を含む、SharePoint ライブラリ内のアイテムの完全修飾 URL です。 例:  
  
```  
https://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl  
```  
  
 **&**  
 URL アクセス パラメーターの名前と値のペアを区切るために使用します。  
  
 **プレフィックス**  
 省略可。 URL アクセス パラメーターのプレフィックス ( `rs:` や `rc:`など)。レポート サーバー内で実行している特定のプロセスにアクセスします。  
  
> [!NOTE]  
>  URL アクセス パラメーターにプレフィックスが含まれていない場合は、レポート サーバーによってパラメーターがレポート パラメーターとして処理されます。 レポート パラメーターではパラメーター プレフィックスが使用されず、大文字と小文字が区別されます。  
  
 **param**  
 パラメーター名。  
  
 *value*  
 使用しているパラメーターの値に対応する URL テキスト。  
  
 **注:** 使用可能な URL アクセス パラメーターの一覧については、「 [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md)」(URL アクセス パラメーター リファレンス) を参照してください。 URL でレポート パラメーターを渡す例については、「 [URL 内でレポート パラメーターを渡す](../reporting-services/pass-a-report-parameter-within-a-url.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|リンク|  
|-----------------------|-----------|  
|レポート、共有データ ソース、リソースなどのレポート サーバー アイテムにアクセスする|[URL アクセスを使用したレポート サーバー アイテムへのアクセス](../reporting-services/access-report-server-items-using-url-access.md)|  
|レポート パラメーターをレポートに受け渡す|[URL 内でレポート パラメーターを渡す](../reporting-services/pass-a-report-parameter-within-a-url.md)|  
|日付、通貨など、ロケール固有の解釈を定義する URL アクセス文字列にレポート パラメーターのロケールを設定する|[URL でレポート パラメーターの言語を設定する](../reporting-services/set-the-language-for-report-parameters-in-a-url.md)|  
|レポートの表示形式をカスタマイズする表示拡張機能固有の設定を送信する|[URL でデバイス情報設定を指定する](../reporting-services/specify-device-information-settings-in-a-url.md)|  
|ブラウザーに表示せずに、レポートを直接ファイル形式にエクスポートする|[URL アクセスを使用してレポートをエクスポートする](../reporting-services/export-a-report-using-url-access.md)|  
|レポートを開き、文字列の場所に直接移動する|[URL アクセスを使用してレポートを検索する](../reporting-services/search-a-report-using-url-access.md)|  
|特例のレポート履歴スナップショットを表示する|[URL アクセスを使用してレポート履歴スナップショットを表示する](../reporting-services/render-a-report-history-snapshot-using-url-access.md)|  
  
## <a name="see-also"></a>参照  
 [URL 内でレポート パラメーターを渡す](../reporting-services/pass-a-report-parameter-within-a-url.md)   
 [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md)   
 [URL アクセスを使用した Reporting Services の統合](../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [レポートの検索、表示、管理 &#40;レポート ビルダーおよび SSRS&#41;](../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
