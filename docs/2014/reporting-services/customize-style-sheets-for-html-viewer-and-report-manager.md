---
title: HTML ビューアーおよびレポート マネージャーのスタイル シートのカスタマイズ |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 7c7745d69e234f81c2a331d214789e93e9fd4014
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "64568266"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>HTML ビューアーとレポート マネージャーのスタイル シートのカスタマイズに関する記事 (ページ、サイトなどの場合もあります)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 既定のカスケード スタイル シート (.css) ファイルがスタイルを定義する提供、**レポート**HTML ビューアーおよびレポート マネージャーのツールバー。 Web 開発者、またはカスケード スタイル シート作成に関する専門知識を持つユーザーであれば、各自の責任で既定のスタイルを変更し、色、フォント、およびツール バーやレポート マネージャーのレイアウトを変えることができます。 このリリースでは、既定のスタイル シートについても、そのスタイル シートの変更手順についても説明していません。  
  
 スタイル シートの変更に誤りがあると、レポートを開いたときにエラーが発生する可能性があります。 スタイル シートの変更方法がわからない場合は、既定のスタイル シートを使用してください。 スタイル シートをカスタマイズする場合は、変更を行う前に、既定のすべての .css ファイルのバックアップを作成してください。  
  
 スタイル シートを変更しても、レポート サーバーで実行するパブリッシュされたレポートの外観には影響しません。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]では、レポートはスタイル シートを参照しません。 レポート サーバーによって自動生成されるアドホック レポートは、レポート サーバーのプログラム ファイルに埋め込みリソースとして格納されているスタイル情報を使用します。 レポート デザイナーで作成するレポートでは、レポート定義で指定したフォント、色、およびレイアウトを使用します。 スタイルは、レイアウトのその他の部分と共にインラインで作成されます。  
  
> [!NOTE]  
>  定義済みのレポート スタイルを使用する場合は、レポート ウィザードを使用してレポートを作成します。 レポート ウィザードには、異なる色の組み合わせやフォントを使用した定型レポートの作成に利用できるさまざまなテーマが用意されています。 レポートのテーマを定義するスタイル テンプレートは変更できます。  
  
## <a name="reporting-services-style-sheets"></a>Reporting Services のスタイル シート  
 次の表に、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 環境で使用するスタイル シート (.css) ファイルの説明を示します。  
  
|スタイル シート|説明|  
|-----------------|-----------------|  
|Htmlviewer.css|HTML ビューアーの **[レポート]** ツール バーのカスタム スタイルを作成するためにテンプレートとして使用できるサンプル スタイル シートを提供します。<br /><br /> HTML ビューアーが使用する既定のスタイルは、レポート サーバーにコンパイルされます。 Htmlviewer.css ファイルは、ビューアーが使用するスタイルのサンプルを提供します。|  
|ReportingServices.css|レポート マネージャーのスタイルを定義します。|  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>カスタム スタイル シートを使用するための Reporting Services の構成  
 スタイル シートは、有効なカスケード スタイル シート (.css) ファイルであり、Styles フォルダーに格納されていることが必要です。 既定では、Styles フォルダーにある\<*ドライブ*>: SQL server \mssql \Program Files\Microsoft *。n*\Reporting Services\ReportServer\Styles します。  
  
 実行時に HTML ビューアーのカスタム スタイル シートを使用するには、次の方法を選択できます。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 構成ファイルに、<`HTMLViewerStyleSheet`> 設定を追加します。  
  
-   レポートの URL でスタイル シートを指定します。  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>RSReportServer.config ファイルの変更  
 RSReportServer.config ファイルを変更して、HTML ビューアーのカスタム スタイル シートを指定できます。 既定では、<`HTMLViewerStyleSheet`> 設定はファイルに含まれていません。 RSReportServer.config ファイルの <`Configuration`> セクションにこの設定を入力し、使用するスタイル シートを指定する必要があります。 スタイル シートを指定するときには、.css ファイルの拡張子は含めないでください。  
  
 次の例は、スタイル シートを指定する方法を示しています。  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>レポートの URL でのスタイル シートの指定  
 `rc:StyleSheet` URL アクセス パラメーターを使用して、レポートの URL でカスタム スタイル シートを指定できます。 URL アクセス パラメーターを指定する方法の詳細については、次を参照してください。 [URL アクセス パラメーター リファレンス](url-access-parameter-reference.md)します。  
  
 次の例は、カスタム スタイルを追加する方法を示しています。  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>参照  
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [HTML ビューアーとレポート ツールバー](html-viewer-and-the-report-toolbar.md)   
 [RSReportServer 構成ファイル](report-server/rsreportserver-config-configuration-file.md)  
  
  
