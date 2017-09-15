---
title: "(レポート ビルダーおよび SSRS) のデータの表示 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a458fdf9-fb2a-4fee-9fbd-b38f36e91753
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 209938a6f1f5562fb3e5bfb70be713d2eb9b8285
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="rendering-data-report-builder-and-ssrs"></a>データの表示 (レポート ビルダーおよび SSRS)
  HTML、MHTML、Word、Excel、PDF、Image などのレイアウト レンダラーを使用した場合、データとその構造は変更されません。 CSV (コンマ区切り) や XML などのデータ レンダラー形式を使用してエクスポートした場合、視覚的なレイアウト要素は表示されません。 CSV および XML では、レポートを表示する際に、特定の規則がレポート本文とそのコンテンツに適用されます。 これらの規則により、データがこの形式でどのように表示されるかが決定します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 データ レンダラーを使用すると、次のことが可能になります。  
  
-   データベースへのインポート。 CSV は、SQL Server や Microsoft Access などの多くのデータベース アプリケーションで簡単にインポートできる一般的な形式です。  
  
-   Excel へのインポート。 CSV レンダラーを使用して、データを Excel にエクスポートします。ただし、視覚的なレイアウトは含まれません。 データを Excel にインポートすると、グラフ、式、ピボット テーブルなど、標準の Excel ツールを利用できます。  
  
-   XSLT 変換。 XSLT を XML レンダラーの出力に適用できます。 このサーバー側の変換は、事実上あらゆる形式にデータを変換できる強力な手法です。  
  
-   データ交換/EDI。 外部プロセスによって、レポートの CSV または XML 表示を要求し、そのデータを使用することができます。  
  
 データ レンダラーの形式は、レイアウト レンダラーとは別のプロパティ セットによって制御されます。 データ レンダラーのみに適用される、 **[プロパティ]** ペインのプロパティ セットを次に示します。  
  
-   DataElementOutput プロパティは、エクスポート時に特定のアイテムをデータに含めるかどうかを制御します。  
  
-   DataElementName プロパティは、データ要素の名前を制御します。 CSV では、CSV の列ヘッダーの名前が制御されます。 XML では、アイテムの XML 要素または属性の名前になります。  
  
-   DataElementStyle プロパティは、XML において、レポート アイテムが要素と属性のどちらとして表示されるかを制御します。  
  
 CSV エクスポート オプションでは、書式を持たないコンマ区切りのプレーン テキスト形式のファイルとしてレポート データが保存されます。 既定では、コンマ (,) を使用してフィールドおよび行を区切りますが、この設定は、デバイス情報設定で構成できます。 エクスポートされたファイルは、Office SharePoint Server などのスプレッドシート プログラムで開いたり、他のプログラムのインポート形式として使用できます。 .csv ファイルは、メモ帳などのテキスト エディターで開きます。 URL としてアクセスした場合は、.csv ファイルから **text/csv**の MIME の種類が返されます。 ファイルは、MIME バージョン 1.0 形式のファイルになります。 CSV ファイル形式でレポートを表示する方法の詳細については、「[Exporting to a CSV File &#40;Report Builder and SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)」(CSV ファイルへのエクスポート &#40;レポート ビルダーおよび SSRS&#41;) を参照してください。  
  
 [レポート データが含まれている XML ファイル] エクスポート オプションを指定すると、レポートが XML ファイルとして保存されます。 レポートの XML スキーマは、各レポート固有のものです。 XML エクスポート オプションでは、レポート レイアウト情報は保存されません。 このオプションで生成された XML は、データベースにインポートしたり、XML データ メッセージとして使用したり、カスタム アプリケーションに送信することができます。 XML ファイル形式でレポートを表示する方法の詳細については、「[Exporting to XML &#40;Report Builder and SSRS&#41;](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)」(XML へのエクスポート &#40;レポート ビルダーおよび SSRS&#41;) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services &#40; の改ページレポート ビルダーおよび SSRS &#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [レンダリングの動作と #40 です。レポート ビルダーおよび SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [対話機能のさまざまなレポート表示拡張機能と #40 です。レポート ビルダーおよび SSRS &#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [レポート アイテムのレンダリング & #40 です。レポート ビルダーおよび SSRS &#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、およびリスト &#40; です。レポート ビルダーおよび SSRS &#41; です。](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Reporting Services デバイス情報設定](http://go.microsoft.com/fwlink/?LinkId=102515)  
  
  