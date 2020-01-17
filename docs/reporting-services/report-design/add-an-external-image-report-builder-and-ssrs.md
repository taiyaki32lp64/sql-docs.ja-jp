---
title: 外部の画像の追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ac0bc269bfe0b7b443270fcc0eb6bdcc3e09a40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582108"
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>外部の画像の追加 (レポート ビルダーおよび SSRS)
  外部の画像は、ネイティブ モードまたは SharePoint 統合モードのレポート サーバー上にあるものも、他の Web サイトにあるものもあります。 外部の画像をレポートに含める場合、その画像が存在すること、およびその画像にアクセスする権限をレポートのリーダーが持っていることを確認する必要があります。 詳細については、「[画像 &#40;レポート ビルダーおよび SSRS& #41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>外部の画像を追加するには  
  
1.  レポート デザイン ビューの **[挿入]** タブで、 **[画像]** をクリックします。  
  
2.  デザイン画面で、ボックスをクリックし、画像の目的のサイズにドラッグします。  
  
3.  **[画像のプロパティ]** ダイアログ ボックスの **[全般]** タブにある **[名前]** ボックスに名前を入力するか、既定値を受け入れます。  
  
4.  (省略可) **[ツールヒント]** ボックスに、HTML で表示されたレポートの画像の上にマウスを置いたときに表示されるテキストを入力します。  
  
5.  **[画像ソースの選択]** で、 **[外部]** を選択します。  
  
     ネイティブ モードのレポート サーバーにある画像を指定する場合は、 **[次の画像を使用]** ボックスに画像の相対パスを入力します (例: ../images/image1.jpg)。  
  
     SharePoint 統合モードのレポート サーバーまたはその他の Web サイトにある画像を指定する場合は、 **[次の画像を使用]** ボックスに画像への完全な URL を入力します (例: https://\<SharePoint サーバー名>/\<サイト>/Documents/images/image1.jpg)。  
  
     詳細については、「[外部アイテムへのパスの指定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)」を参照してください。  
  
6.  (省略可) 画像レポート アイテムのその他のプロパティを設定するには、 **[サイズ]** 、 **[表示]** 、 **[アクション]** 、または **[罫線]** を選択します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [レポートへの画像の埋め込み &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [背景画像の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)   
 [[全般] &#40;[画像のプロパティ] ダイアログ ボックス&#41; &#40;レポート ビルダーおよび SSRS&#41;](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
