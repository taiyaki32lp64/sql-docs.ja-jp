---
title: 印刷コントロールを使用したブラウザーからのレポートの印刷 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 535d35ad80f940e7d3ed4a9163b2e65757088e58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581166"
---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>印刷コントロールを使用したブラウザーからのレポートの印刷 (レポート ビルダーおよび SSRS)
  レポートを表示するための最も一般的なクライアント アプリケーションはブラウザーですが、ブラウザーの印刷機能はレポートの印刷には適していません。 ブラウザーの印刷機能は、Web ページを印刷するための機能です。 通常、ブラウザーから印刷したページには、Web ページ上にあるすべての可視要素と、ページまたは Web サイトを識別するヘッダーおよびフッター情報が含まれます。 ブラウザーからの印刷では現在のウィンドウの内容が印刷されるため、 レポートが数ページあっても最初のページしか印刷されません。また、レポート ページのサイズが印刷ページのサイズより大きい場合には、ページの全体を印刷しきれない場合もあります。  
  
 ブラウザーで表示したレポートの印刷品質を向上させ、複数のページを印刷するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で提供されているクライアント側印刷機能を使用します。 クライアント側印刷機能では、標準の **[印刷]** ダイアログ ボックスを使用して、印刷する前に、プリンターの選択、ページと余白の指定、およびレポートのプレビューを行うことができます。 クライアント側印刷機能は、ブラウザーの **[ファイル]** メニューの **[印刷]** コマンドの代わりに使用できます。 クライアント側印刷機能を使用すると、レポートがデザインどおりに印刷され、Web ページの印刷で表示されるような余分な要素は印刷されません。  
  
 クライアント側印刷機能を使用するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX コントロールをインストールする必要があります。 詳細については、「 [Reporting Services のクライアント側印刷機能の有効化と無効化](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>印刷オプション  
 レポートの印刷プロパティを構成するには、 **[印刷]** ダイアログ ボックスで **[プロパティ]** ボタンをクリックします。 **[用紙サイズ]** は、レポート定義で定義されているレポート ページ サイズの既定の高さと幅によって決まります。 指定できる値は、利用できるプリンターの種類とその機能によって異なります。 [幅] と [高さ] には、そのコンピューター上で構成されたプリンター ドライバーによって決まる既定値が表示されます。 これらの値を変更すると、指定したサイズでレポートが印刷されます。 ページの幅と高さは、それぞれ **[印刷の向き]** ( **[縦]** または **[横]** ) で決まります。 表示される既定の印刷の向きは、レポートのページの幅と高さで決まります。  
  
> [!NOTE]  
>  **[印刷]** ダイアログ ボックスおよび既定のプリンター設定 (幅、高さ、ページの向き) は、レポート定義で決まります。  
  
### <a name="print-preview"></a>印刷プレビュー  
 レポートをプレビューするには、 **[印刷]** ダイアログ ボックスで **[プレビュー]** ボタンをクリックします。 これによりレポートの最初のページが別のプレビュー ウィンドウ内に表示されます。 残りのページは、レポート サーバーでレポートが表示されると利用可能になります。 レポートのプレビューは、EMF 形式で表示されます。 プレビューでは前後のページに移動することができ、最後のページに到達すると、 **[次へ]** ボタンが無効になります。  
  
### <a name="adjusting-print-margins"></a>余白の調整  
 レポートを印刷する前に、表示される EMF レポートの余白を変更できます。 余白を変更するには、 **[印刷]** ダイアログ ボックスで **[プレビュー]** ボタンをクリックします。 プレビュー ページの上部にある **[余白]** ボタンをクリックします。 [余白] ダイアログ ボックスが表示されます。 必要に応じて上下および左右の余白を設定します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)] ダイアログ ボックスが閉じ、プレビューの表示および印刷の設定が保存されます。  
  
## <a name="see-also"></a>参照  
 [レポートの印刷 (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [レポートの印刷 (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
  
  
