---
title: フォルダーの作成、削除、または変更 (レポート マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing folders
- modifying folders
- deleting folders
- folders [Reporting Services], creating
- folders [Reporting Services], deleting
- folders [Reporting Services], modifying
ms.assetid: d62159a8-ec67-4e28-a9f1-05a9250065bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef4aa341c8f89afbd099cd26fc8352425e6ac8ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103921"
---
# <a name="create-delete-or-modify-a-folder-report-manager"></a>フォルダーの作成、削除、または変更 (レポート マネージャー)
  フォルダーを作成すると、レポート サーバーにパブリッシュするアイテムを整理して管理できます。 フォルダーを作成することには、関心のあるレポートをユーザーが見つけやすくなるという利点があります。 コンテンツ マネージャーは、権限を適用するためのフレームワークとしてフォルダーを利用できます。 特定のフォルダーに対してロールの割り当てを作成することで、開発中のレポートや限定されたユーザーのみを対象としたレポートへのアクセスを制限できます。  
  
### <a name="to-create-a-folder"></a>フォルダーを作成するには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md) を開始します。  
  
2.  レポート マネージャーで、[ホーム] フォルダーを選択し、 **[新しいフォルダー]** をクリックします。 既存のフォルダーの下にフォルダーを作成する場合は、 **[コンテンツ]** ページでそのフォルダーに移動し、クリックして開きます。 次に **[新しいフォルダー]** をクリックします。  
  
     **[新しいフォルダー]** ページが開きます。  
  
3.  フォルダー名を入力します。 フォルダー名にはスペースを使用できますが、URL エンコードに使用される予約文字 (; ? :など) は使用できません : \@ & = + , $ / * \< > |. フォルダー名を続けて入力して、同時に複数のフォルダーを作成することはできません。  
  
4.  必要に応じて、説明を入力します。  
  
5.  **[コンテンツ]** ページの既定の表示でフォルダーを非表示にする場合は、 **[リスト ビューで非表示にする]** をオンにします。 このフォルダーは、 **[コンテンツ]** ページの **[詳細の表示]** をクリックした場合にのみ表示されるようになります。  
  
6.  **[OK]** をクリックします。  
  
### <a name="to-delete-a-folder"></a>フォルダーを削除するには  
  
1.  レポート マネージャーで、 **[コンテンツ]** ページに移動し、変更するアイテムを探します。  
  
2.  アイテムの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[削除]** をクリックします。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-modify-or-delete-a-folder"></a>フォルダーを変更または削除するには  
  
1.  レポート マネージャーで、 **[コンテンツ]** ページに移動し、変更するアイテムを探します。  
  
2.  アイテムの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[管理]** をクリックします。 [全般プロパティ] ページが開きます。  
  
4.  フォルダーの場所を変更するには、 **[移動]** をクリックします。 移動先のフォルダーの場所を入力するか、ツリーから移動先のフォルダーを選択し、 **[OK]** をクリックします。  
  
5.  または、以下の方法でフォルダーのプロパティを変更します。  
  
    -   フォルダーについて表示するテキストを変更するには、名前または説明を入力します。  
  
    -   **[コンテンツ]** ページの既定の表示でフォルダーを表示するには、 **[リスト ビューで非表示にする]** をオフにします。  
  
6.  フォルダーとフォルダーの内容を削除するには、 **[削除]** をクリックします。  
  
7.  **[適用]** をクリックして変更を保存します。  
  
## <a name="see-also"></a>関連項目  
 [[新しいフォルダー] ページ &#40;レポート マネージャー&#41;](../new-folder-page-report-manager.md)   
 [[コンテンツ] ページ &#40;レポート マネージャー&#41;](../contents-page-report-manager.md)   
 [レポートの検索、表示、管理 &#40;レポート ビルダーおよび SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
