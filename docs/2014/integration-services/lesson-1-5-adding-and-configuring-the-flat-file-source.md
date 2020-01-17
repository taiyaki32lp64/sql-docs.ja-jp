---
title: 手順 5:追加と構成、フラット ファイル ソース |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32b95a5d156ae52394b7128b024c86b9a7e308b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891540"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>手順 5:フラット ファイル ソースの追加と構成
  ここでは、フラット ファイル ソースをパッケージに追加し、構成します。 フラット ファイル ソースとは、フラット ファイル接続マネージャーにより定義されるメタデータを使用するデータ フロー コンポーネントです。フラット ファイル接続マネージャーは、変換処理によってフラット ファイルから取得されるデータの形式や構造を指定します。 フラット ファイル接続マネージャーに定義されているファイル形式を使用し、1 つのフラット ファイルからデータを取得するよう、フラット ファイル ソースを定義できます。  
  
 このチュートリアルでは、使用するフラット ファイル ソースを構成します、`Sample Flat File Source Data`以前に作成した接続マネージャー。  
  
### <a name="to-add-a-flat-file-source-component"></a>フラット ファイル ソース コンポーネントを追加するには  
  
1.  開く、**データ フロー**をダブルクリックするか、デザイナー、`Extract Sample Currency Data`データ フロー タスクをクリックして、**データ フロー タブで**します。  
  
2.  **[SSIS ツールボックス]** で **[その他の変換元]** を展開し、 **[フラット ファイル ソース]** を **[データ フロー]** タブのデザイン画面にドラッグします。  
  
3.  **データ フロー**デザイン画面で、新しく追加したを右クリックして**フラット ファイル ソース**、 をクリックして**の名前を変更**、名を変更して、`Extract Sample Currency Data`します。  
  
4.  このフラット ファイル ソースをダブルクリックして、[フラット ファイル ソース エディター] ダイアログ ボックスを開きます。  
  
5.  **フラット ファイル接続マネージャー**ボックスで、`Sample Flat File Source Data`します。  
  
6.  **[列]** をクリックし、列名が正しいことを確認します。  
  
7.  **[OK]** をクリックします。  
  
8.  [フラット ファイル ソース] を右クリックし、 **[プロパティ]** をクリックします。  
  
9. [プロパティ] ウィンドウであることを確認、`LocaleID`プロパティに設定されて**英語 (米国)** します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [手順 6:追加して、参照変換を構成します。](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>参照  
 [フラット ファイル ソース](data-flow/flat-file-source.md)   
 [[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)  
  
  
