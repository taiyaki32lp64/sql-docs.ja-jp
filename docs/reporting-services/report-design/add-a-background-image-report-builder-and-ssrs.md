---
title: 背景画像の追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c777fefb-8695-44a7-b5cd-a18c587583f2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5472406acc011ea654ff4eb73bc25c73c0475e04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575108"
---
# <a name="add-a-background-image-report-builder-and-ssrs"></a>背景画像の追加 (レポート ビルダーおよび SSRS)
  四角形、テキスト ボックス、一覧、マトリックス、テーブル、グラフの一部などのレポート アイテム、またはページ ヘッダー、ページ フッター、レポート本文などのレポート セクションに背景画像を追加できます。 背景画像は、レポート デザイン画面で選択された任意のアイテムでプロパティ ペインに **[BackgroundImage]** が表示されるものに対して定義できます。 他の画像と同様に、背景画像は、レポート サーバー上の画像、データセット フィールドからの画像、またはレポート定義に埋め込まれた画像などへの URL である場合があります。 レポートに埋め込まれた画像を使用するには、その画像をデザイン画面に追加する前に、それをレポート定義に追加する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-the-report-definition"></a>レポート定義に画像を埋め込むには  
  
1.  レポート データ ペインで **[画像]** ノードを右クリックし、 **[画像の追加]** をクリックします。  
  
    > [!NOTE]  
    >  レポート データ ペインが表示されていない場合は、 **[表示]** タブの **[レポート データ]** をクリックします。  
  
2.  レポート定義に埋め込む画像に移動し、 **[OK]** をクリックします。  
  
### <a name="to-add-a-background-image"></a>背景画像を追加するには  
  
1.  レポート デザイン ビューで、背景画像を追加するレポート アイテムを選択します。  
  
2.  プロパティ ペインが表示されていない場合は、 **[表示]** タブの **[プロパティ]** を選択します。  
  
3.  プロパティ ペインで、 **[BackgroundImage]** を展開し、次の操作を行います。  
  
    -   埋め込まれた画像を追加する場合  
  
         **[ソース]** を **[埋め込み]** に設定します。  
  
         **[値]** に、レポートに埋め込まれている画像の名前を設定します。  
  
    -   外部の画像を追加する場合  
  
         **[ソース]** を **[外部]** に設定します。  
  
         **[値]** に画像への有効なパスを設定します。 これは、ネイティブ モードまたは SharePoint 統合モードのレポート サーバー上にあるものも、他の Web サイトにあるものもあります。 詳細については、「[外部の画像の追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)」を参照してください。  
  
    -   レポート アイテムの接続先データベースのフィールドに格納されている画像を追加する場合  
  
         **[ソース]** を **[データベース]** に設定します。  
  
         **[値]** に、レポート データセット内のフィールドの名前を設定します。 詳細については、「[データバインド画像の追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md)」を参照してください。  
  
         **[MIMEType]** 、またはファイル形式には、画像に適切な MIME の種類を選択します (bmp など)。  
  
        > [!NOTE]  
        >  **[Source]** プロパティが **[Database]** に設定されている場合にのみ、[MIMEType] が適用されます。 **[Source]** プロパティが **[External]** または **[Embedded]** に設定されている場合、 **[MIMEType]** の値は無視されます。  
  
    -   **[BackgroundRepeat]** で、式、 **[Default]** 、 **[Repeat]** 、 **[RepeatX]** または **[RepeatY]** 、または **[Clip]** を選択します。  
  
         グラフ内の背景画像の場合は、 **[BackgroundRepeat]** を **[Default]** 、 **[Repeat]** 、 **[Fit]** 、および **[Clip]** に設定できますが、 **[RepeatX]** または **[RepeatY]** には設定できません。  
  
## <a name="see-also"></a>参照  
 [画像 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [[全般] ([画像のプロパティ] ダイアログ ボックス) (レポート ビルダーおよび SSRS)](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
