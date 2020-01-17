---
title: データ ソースの変換、埋め込まれた共有 (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 64879a7ab82f509f129cf43ab50c1cdbb3b7f913
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107408"
---
# <a name="convert-a-data-source-from-embedded-to-shared-report-builder-and-ssrs"></a>埋め込みデータ ソースから共有データ ソースへの変換 (レポート ビルダーおよび SSRS)
  レポート データ ペインの各データ ソースは、レポートに固有のものとして埋め込まれている場合と、共有されている場合とがあります。 レポート ビルダーにおける共有データ ソースの参照先は、レポート サーバー上または SharePoint サイト上にパブリッシュされた共有データ ソースです。 レポート デザイナーにおける共有データ ソースの参照先は、ソリューション エクスプローラーの **[共有データ ソース]** フォルダーに表示される共有データ ソースです。  
  
 埋め込みデータ ソースと共有データ ソースの相違点の詳細については、「[埋め込みおよび共有のデータ接続またはデータ ソース &#40;レポート ビルダーおよび SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)」を参照してください。  
  
 共有データ ソースの作成方法の詳細については、「[埋め込みデータ ソースまたは共有データ ソースを作成する &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>レポート デザイナー  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>埋め込みデータ ソースから共有データ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[共有データ ソースに変換]** をクリックします。  
  
    > [!NOTE]  
    >  レポート データ ペインが表示されていない場合は、 **[表示]** メニューの **[レポート データ]** をクリックします。 ペインがフローティング ウィンドウとして開く場合は、ドッキングすることができます。 詳細については、「[レポート デザイナーのレポート データ ペインをドッキングする (SSRS)](../tools/dock-the-report-data-pane-in-report-designer-ssrs.md)」を参照してください。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。 ソリューション エクスプローラーでは、同じ名前の共有データ ソースが **[共有データ ソース]** フォルダーに表示されます。  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>共有データ ソースを埋め込みデータ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[データ ソースのプロパティ]** ダイアログ ボックスを開いて、 **[埋め込み接続]** をクリックします。 必要な情報を入力します。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。  
  
## <a name="report-builder"></a>レポート ビルダー  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>埋め込みデータ ソースから共有データ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[データ ソースのプロパティ]** ダイアログ ボックスを開いて、 **[埋め込み接続]** をクリックします。 必要な情報を入力します。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>共有データ ソースを埋め込みデータ ソースに変換するには  
  
-   レポート データ ペインでデータ ソースを右クリックし、 **[データ ソースのプロパティ]** ダイアログ ボックスを開いて、 **[埋め込み接続]** をクリックします。 必要な情報を入力します。  
  
     レポート データ ペインでデータ ソース アイコンが共有データ ソースのアイコンに変わります。  
  
## <a name="see-also"></a>参照  
 [レポート データ ソースを管理する](manage-report-data-sources.md)   
 [Reporting Services でのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
