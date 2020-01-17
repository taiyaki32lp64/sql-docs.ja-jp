---
title: 外部の画像の追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 236600f0a4ff2b77daaab2266b7e927e6858447b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106724"
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>外部の画像の追加 (レポート ビルダーおよび SSRS)
  外部の画像は、ネイティブ モードまたは SharePoint 統合モードのレポート サーバー上にあるものも、他の Web サイトにあるものもあります。 外部の画像をレポートに含める場合、その画像が存在すること、およびその画像にアクセスする権限をレポートのリーダーが持っていることを確認する必要があります。 詳細については、「[画像 &#40;レポート ビルダーおよび SSRS& #41;](images-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>外部の画像を追加するには  
  
1.  レポート デザイン ビューの **[挿入]** タブで、 **[画像]** をクリックします。  
  
2.  デザイン画面で、ボックスをクリックし、画像の目的のサイズにドラッグします。  
  
3.  **[画像のプロパティ]** ダイアログ ボックスの **[全般]** タブにある **[名前]** ボックスに名前を入力するか、既定値を受け入れます。  
  
4.  (省略可) **[ツールヒント]** ボックスに、HTML で表示されたレポートの画像の上にマウスを置いたときに表示されるテキストを入力します。  
  
5.  **[画像ソースの選択]** で、 **[外部]** を選択します。  
  
     ネイティブ モードのレポート サーバーにある画像を指定する場合は、 **[次の画像を使用]** ボックスに画像の相対パスを入力します (例: ../images/image1.jpg)。  
  
     SharePoint 統合モード、またはその他の Web サイトでレポート サーバー上の画像、入力内のイメージへの完全な URL、**このイメージを使用**ボックス-たとえば、 http://\<SharePointservername >/\<サイト >/Documents/images/image1.jpg します。  
  
     詳細については、「[外部アイテムへのパスの指定 &#40;レポート ビルダーおよび SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)」を参照してください。  
  
6.  (省略可) 画像レポート アイテムのその他のプロパティを設定するには、 **[サイズ]** 、 **[表示]** 、 **[アクション]** 、または **[罫線]** を選択します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [レポートへの画像の埋め込み &#40;レポート ビルダーおよび SSRS&#41;](embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [背景画像の追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-background-image-report-builder-and-ssrs.md)   
 [[全般] &#40;[画像のプロパティ] ダイアログ ボックス&#41; &#40;レポート ビルダーおよび SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
