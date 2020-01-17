---
title: Web ポータルのブランド化 | Microsoft Docs
ms.date: 04/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
description: この記事では、ブランド パッケージを利用してビジネスのブランドを設定することで Web ポータルの外観を変更する方法について説明します。 CSS (カスケーディング スタイル シート) に詳しくなくても作成できるようにブランド パッケージは設計されています。
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 47fc9ba65aca128a7e812f85c5bd06ca38131cbf
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251914"
---
# <a name="branding-the-web-portal"></a>Web ポータルのブランド化

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

ビジネスのブランドを設定することで Web ポータルの外観を変更できます。 これにはブランド パッケージを使用します。 CSS (カスケーディング スタイル シート) に詳しくなくても作成できるようにブランド パッケージは設計されています。

<iframe width="560" height="315" src="https://www.youtube.com/embed/m08kLuofwFA" frameborder="0" allowfullscreen></iframe>

## <a name="creating-the-brand-package"></a>ブランド パッケージを作成する
  
Reporting Services のブランド パッケージは 3 つのアイテムから構成されており、zip ファイルとしてパッケージされています。   
  
- colors.json  
- metadata.xml  
- logo.png (任意)  
  
ファイルには上記の名前を与える必要があります。 ただし、zip ファイルの名前は自由に設定できます。  
  
### <a name="metadataxml"></a>metadata.xml
  
metadata.xml ファイルにより、ブランド パッケージの名前を設定できます。また、このファイルには、colors.json ファイルと logo.png ファイルの両方の参照エントリが含まれています。  
  
ブランド パッケージの名前を変更するには、 **SystemResourcePackage** 要素の **name** 属性を変更します。  
  
    name="Multicolored example brand"  
  
任意で、ブランド パッケージにロゴ画像を含めることができます。 このアイテムは Contents 要素内にリストアップされます。  
  
ロゴ ファイルなしの例。  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
    </Contents>  
  
ロゴ ファイルありの例。  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
      <Item key="logo" path="logo.png" />  
    </Contents>  
  
### <a name="colorsjson"></a>Colors.json
  
ブランド パッケージがアップロードされると、サーバーは colors.json ファイルから名前/値のペアを抽出し、それをマスター LESS スタイルシートである、brand.less と結合します。 この LESS ファイルが処理され、結果的に生成された CSS ファイルがクライアントに提供されます。 スタイルシートのすべての色を 6 文字の 16 進数で表現します。  
  
次のように、LESS スタイルシートには、いくつかの事前定義済み LESS 変数を参照するブロックが含まれます。  
  
    /* primary buttons */   
    .btn-primary {   
        color:@primaryButtonColor;   
        background-color:@primaryButtonBg;   
    }  
  
これは CSS 構文に似ていますが、@symbol が接頭辞として付く色値は LESS に固有のものです。 値が json ファイルにより設定される変数です。  
  
たとえば、colors.json ファイルに次の値が含まれていたとします。  
  
    "primary":"#009900",   
    "primaryContrast":"#ffffff"   
  
処理された出力では、LESS 変数の **\@primaryButtonBg** が検索され、**primary** と呼ばれる json プロパティにマッピングされていることが確認されます (この例では、#009900)。 その後、適切な CSS が出力されます。  
  
    .btn-primary {   
        color:#ffffff;   
        background-color:#009900;   
    }  
  
プライマリ ボタンはすべて濃い緑でレンダリングされ、白いテキストが付きます。  
  
Reporting Services の colors.json ファイルには 2 つのメイン カテゴリがあり、アイテムがグループ化されています。  
  
- **インターフェイス**: Reporting Services の Web ポータルに固有の項目が含まれます。  
- **テーマ**: 作成したモバイル レポートに固有の項目が含まれます。  
  
インターフェイス セクションは、以下のグループに分類されます。  
  
|セクション|[説明]|  
|---|---|  
|primary|ボタンとホバーの色。|  
|セカンダリ|タイトル バー、検索バー、左側のメニュー (表示される場合)、それらのアイテムのテキストの色。|  
|ニュートラル プライマリ|ホームとレポート領域の背景。|  
|ニュートラル セカンダリ|テキスト ボックスとフォルダー オプションの背景、設定メニュー。|  
|ニュートラル ターシャリ|サイト設定の背景。|  
|危険/警告/成功メッセージ|これらのメッセージの色。|  
|KPI (KPI)|色を good (1)、neutral (0)、neutral (-1)、none で調整します。|  
  
Mobile Report Publisher で初めてサーバーに接続するとき、それにブランド パッケージが配置されている場合、そのテーマが利用可能テーマに追加されます。アプリの右上のメニューから利用できます。  
  
![ssRSBrandingMobileReportPublisher](../reporting-services/media/ssrsbrandingmobilereportpublisher.png)  
  
その後、作成したあらゆるモバイル レポートにこのテーマを利用できます。テーマを配置した同じサーバーでなくても構いません。   
  
### <a name="using-a-logo"></a>ロゴを使用する
  
ブランド パッケージでロゴを追加する場合、Web ポータルの [サイト設定] メニューに設定した名前の代わりに Web ポータルに表示されます。  
  
ロゴのために追加するファイルには PNG ファイル形式を使用する必要があります。 ファイルの寸法はサーバーにアップロードした後に拡大されます。 約 290px x 60px になるはずです。  
   
## <a name="applying-the-brand-package-to-the-web-portal"></a>Web ポータルにブランド パッケージを適用する
  
次の手順でブランド パッケージを追加、ダウンロード、削除します。  
  
1.  右上にある **歯車** アイコンを選択します。  
  
2.  **[サイトの設定]** を選択します。  
  
    ![ssRSGearMenu](../reporting-services/media/ssrsgearmenu.png)  
  
3.  **[ブランド化]** を選択します。  
  
    ![ssRSBranding](../reporting-services/media/ssrsbranding.png)  
  
**[現在インストールされているブランド パッケージ]** には、アップロードされているパッケージの名前が表示されるか、何も表示されません。  
  
**[ブランド パッケージのアップロード]** をクリックすると、Web ポータルにパッケージが適用されます。 変更はすぐに確認できます。  
  
パッケージを **[ダウンロード]** したり、 **[削除]** したりすることもできます。 パッケージを削除すると、直後に Web ポータルが既定のブランドにリセットされます。  
  
## <a name="metadataxml-example"></a>metadata.xml 例
  
    <?xml version="1.0" encoding="utf-8"?>  
    <SystemResourcePackage xmlns="https://schemas.microsoft.com/sqlserver/reporting/2016/01/systemresourcepackagemetadata"  
        type="UniversalBrand"  
        version="2.0.2"  
        name="Multicolored example brand"  
        >  
        <Contents>  
            <Item key="colors" path="colors.json" />  
            <Item key="logo" path="logo.png" />  
        </Contents>  
    </SystemResourcePackage>  
   
## <a name="colorsjson-example"></a>colors.json 例
  
    {  
        "name":"Multicolored example brand",  
        "version":"1.0",  
        "interface":{  
            "primary":"#b31e1e",  
            "primaryAlt":"#ca0806",  
            "primaryAlt2":"#621013",  
            "primaryAlt3":"#e40000",  
            "primaryAlt4":"#e14e50",  
            "primaryContrast":"#fff",  
  
            "secondary":"#042200",  
            "secondaryAlt":"#0f4400",  
            "secondaryAlt2":"#155500",  
            "secondaryAlt3":"#217700",  
            "secondaryContrast":"#49e63c",  
  
            "neutralPrimary":"#d8edff",  
            "neutralPrimaryAlt":"#c9e6ff",  
            "neutralPrimaryAlt2":"#aedaff",  
            "neutralPrimaryAlt3":"#88c8ff",  
            "neutralPrimaryContrast":"#0a2b4c",  
  
            "neutralSecondary":"#e9d8eb",  
            "neutralSecondaryAlt":"#d9badc",  
            "neutralSecondaryAlt2":"#b06cb5",  
            "neutralSecondaryAlt3":"#a75bac",  
            "neutralSecondaryContrast":"#250a26",  
  
            "neutralTertiary":"#f79220",  
            "neutralTertiaryAlt":"#f8a54b",  
            "neutralTertiaryAlt2":"#facc9b",  
            "neutralTertiaryAlt3":"#fce3c7",  
            "neutralTertiaryContrast":"#391d00",  
  
            "danger":"#ff0000",  
            "success":"#00ff00",  
            "warning":"#ff8800",  
            "info":"#00ff",  
            "dangerContrast":"#fff",  
            "successContrast":"#fff",  
            "warningContrast":"#fff",  
            "infoContrast":"#fff",  
  
            "kpiGood":"#4fb443",  
            "kpiBad":"#de061a",  
            "kpiNeutral":"#d9b42c",  
            "kpiNone":"#333",  
            "kpiGoodContrast":"#fff",  
            "kpiBadContrast":"#fff",  
            "kpiNeutralContrast":"#fff",  
            "kpiNoneContrast":"#fff"  
           },  
           "theme":{  
            "dataPoints":[  
                "#0072c6",  
                "#f68c1f",  
                "#269657",  
                "#dd5900",  
                "#5b3573",  
                "#22bdef",  
                "#b4009e",  
                "#008274",  
                "#fdc336",  
                "#ea3c00",  
                "#00188f",  
                "#9f9f9f"  
            ],  
  
            "good":"#85ba00",  
            "bad":"#e90000",  
            "neutral":"#edb327",  
            "none":"#333",  
  
            "background":"#fff",  
            "foreground":"#222",  
            "mapBase":"#00aeef",  
            "panelBackground":"#f6f6f6",  
            "panelForeground":"#222",  
            "panelAccent":"#00aeef",  
            "tableAccent":"#00aeef",  
  
            "altBackground":"#f6f6f6",  
            "altForeground":"#000",  
            "altMapBase":"#f68c1f",  
            "altPanelBackground":"#235378",  
            "altPanelForeground":"#fff",  
            "altPanelAccent":"#fdc336",  
            "altTableAccent":"#fdc336"  
        }  
    }  

## <a name="next-steps"></a>次の手順

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
