---
title: ドキュメント マップの作成 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c200a97b-67f2-499f-8374-3ed1ebe3f33c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cbfbc1b1d26f53e5ee8d3e04fc506048d76b3d28
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593672"
---
# <a name="create-a-document-map-report-builder-and-ssrs"></a>ドキュメント マップの作成 (レポート ビルダーおよび SSRS)

ドキュメント マップは、表示レポート内のレポート アイテムへのナビゲーション リンクのセットを提供します。 ドキュメント マップを含むレポートを表示すると、別のサイド ペインがレポートの横に表示されます。 ドキュメント マップ内のリンクをクリックすると、そのアイテムが表示されているレポート ページに移動できます。 レポート セクションとグループは、リンクの階層として配置されます。 ドキュメント マップ内のアイテムをクリックすると、レポートが更新され、ドキュメント マップのアイテムに対応したレポートの領域が表示されます。  
  
 ドキュメント マップにリンクを追加するには、レポート アイテムの **DocumentMapLabel** プロパティを、作成したテキストに設定するか、またはドキュメント マップに表示するテキストになる式に設定します。 テーブル グループやマトリックス グループの一意の値を、ドキュメント マップに追加することもできます。 たとえば、色別に分けられたグループの場合、それぞれの色は、その色のグループ インスタンスが表示されているレポート ページへのリンクとなります。  
  
 また、ドキュメント マップの表示にオーバーライドされるレポートの URL を作成することもできます。このようにすると、ドキュメント マップを表示せずにレポートを実行し、レポート ビューアーのツール バーの **[ドキュメント マップの表示/非表示]** ボタンをクリックして表示を切り替えることができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DocMapRenderExtensions"></a> ドキュメント マップと表示拡張機能  
 ドキュメント マップは、HTML 表示拡張機能 (プレビュー、レポート ビューアーなど) で使用します。 他の表示拡張機能では、異なる手段でドキュメント マップが表示されます。  
  
-   PDF では、ドキュメント マップは [しおり] ペインとして表示されます。  
  
-   Excel では、ドキュメント マップはリンクの階層を含む名前付きのワークシートとして表示されます。 レポート セクションは、同じワークブック内の、ドキュメント マップと共に含まれる別のワークシートに表示されます。  
  
-   Word では、ドキュメント マップは目次として使用されます。  
  
-   Atom、TIFF、XML、および CSV では、ドキュメント マップは無視されます。  
  
 詳細については、「[さまざまなレポート表示拡張機能の対話機能 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)」を参照してください。  
  
##  <a name="AddRptItemToMap"></a>   
#### <a name="to-add-a-report-item-to-a-document-map"></a>ドキュメント マップにレポート アイテムを追加するには  
  
1.  デザイン ビューで、テーブル、マトリックス、ゲージなど、ドキュメント マップに追加するレポート アイテムを選択します。 プロパティ ペインにレポート アイテム プロパティが表示されます。  
  
    > [!NOTE]  
    >  Tablix データ領域を選択するには、任意のセルをクリックして行ハンドルおよび列ハンドルを表示し、コーナー ハンドルをクリックします。  
  
2.  プロパティ ペインで、ドキュメント マップに表示するテキストを **DocumentMapLabel** プロパティに入力するか、ラベルになる式を入力します。 たとえば、「 **Sales Chart**」のように入力します。  
  
    > [!NOTE]  
    >  [プロパティ] ペインが表示されない場合は、 **[表示]** タブの **[表示/非表示]** グループで、 **[プロパティ]** を選択します。  
  
3.  ドキュメント マップに表示するレポート アイテムごとに手順 1. と手順 2. を繰り返します。  
  
4.  **[実行]** をクリックします。 レポートが実行され、作成したラベルがドキュメント マップに表示されます。 任意のリンクをクリックすると、このレポート アイテムが配置されたレポート ページに移動します。  

  
##  <a name="AddUniqueValuesToMap"></a>   
#### <a name="to-add-unique-group-values-to-a-document-map"></a>ドキュメント マップに一意のグループ値を追加するには  
  
1.  デザイン ビューで、ドキュメント マップに表示するグループを格納するテーブル、マトリックス、または一覧を選択します。 グループ化ペインに行グループと列グループが表示されます。  
  
2.  行グループ ペインで、グループを右クリックし、 **[グループの編集]** をクリックします。 **[Tablix グループのプロパティ]** ダイアログ ボックスの **[全般]** ページが開きます。  
  
3.  **[詳細設定]** をクリックします。  
  
4.  **[ドキュメント マップ]** ボックスで、グループ式に一致する式を入力するか、選択します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  ドキュメント マップに表示するグループごとに手順 1. ～ 4. を繰り返します。  
  
7.  **[実行]** をクリックします。 レポートが実行され、グループ値がドキュメント マップに表示されます。 任意のリンクをクリックすると、このレポート アイテムが配置されたレポート ページに移動します。  
  
##  <a name="HideMapWhenViewRpt"></a>   
#### <a name="to-hide-the-document-map-when-you-view-a-report"></a>レポートを表示する場合にドキュメント マップを非表示にするには  
  
1.  Web ポータルで、ドキュメント マップのあるレポートを参照します。  
  
     たとえば、 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] サンプル レポートの場合、次の URL は、"Product Catalog" というレポートを指定しています。  
  
    ```  
    https://localhost/Reports/Pages/Report.aspx?ItemPath=%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    ```  
  
2.  サーバー上のレポート パスをコピーします。 この例のレポート パスは `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`です。  
  
3.  次の 3 つのコンポーネントで新しい URL を作成します。  
  
    -   レポート サーバー上のレポート ビューアー : `https://localhost/ReportServer/Pages/ReportViewer.aspx?`  
  
    -   手順 1. でコピーしたレポートの名前 : `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`  
  
    -   ドキュメント マップの非表示を指定するデバイス情報パラメーター : `&rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False`  
  
     次の URL は、上から順に付加された以上 3 つのコンポーネントで構成されています。  
  
    ```  
    https://localhost/ReportServer/Pages/ReportViewer.aspx?  
    %2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    &rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False  
    ```  
  
     この URL を使用するには、コピーし、すべての改行を削除します。  
  
4.  Web ポータルで URL を貼り付けてから、Enter キーを押します。 レポートが実行され、ドキュメント マップが非表示になります。  
  
> [!NOTE]  
>  サンプル レポートをダウンロードする方法の詳細については、「 [レポート ビルダーおよびレポート デザイナーのサンプル レポート](https://social.technet.microsoft.com/wiki/contents/articles/1093.reporting-services-samples-on-codeplex-sql-server-reporting-services-ssrs.aspx)」を参照してください。  
>   
  >  詳細については、[URL アクセス](../url-access-ssrs.md)に関するページを参照してください。 


その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
