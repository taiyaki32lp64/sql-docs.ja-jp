---
title: オブジェクト エクスプローラーでの空間データの表示
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5ac09bdbc05f406d8d7925af1c9a45346913151
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242954"
---
# <a name="view-spatial-data-in-object-explorer"></a>オブジェクト エクスプローラーでの空間データの表示
  クエリエディターの [**空間結果**] ウィンドウには、[**結果**] ウィンドウにグリッド形式で表示されるデータに加えて、空間データの結果を表示するための視覚的なマッピングツールが用意されています。 
  **[空間結果]** ウィンドウに空間データを表示するには、geometry 型または geography 型のデータを含む空間データ列が少なくとも 1 つクエリ結果に含まれている必要があります。  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>[空間結果] ウィンドウに空間データを表示するには  
  
1.  クエリ エディターで、 **[空間結果]** タブをクリックします。  
  
    > [!NOTE]  
    >  クエリ結果に空間データが含まれていない場合、または結果がテキストとして返されるように指定した場合、このウィンドウは使用できません。  
  
2.  
  **[空間列の選択]** の一覧から、表示する列を選択します。 テーブル内に空間列が 1 つしかない場合は、この列が一覧の既定のオプションです。  
  
3.  
  **[ラベル列の選択]** の一覧から、データ ラベルとして使用する、空間列以外の列を選択します。  
  
4.  
  **[投影の選択]** の一覧から、geography 型のデータに使用する投影法を選択します。 既定の投影法は正距円筒図法です。その他に、メルカトル図法、ロビンソン図法、およびボンヌ図法という投影法を使用できます。  
  
    > [!NOTE]  
    >  空間列に geometry データが含まれている場合、 **Select プロジェクション**は使用できません。  
  
5.  
  **[ズーム]** スライダーを調整して、マップされた要素の視覚的なサイズを大きくします。 多角形の場合、ラベルが表示されるのは、図形がラベルのテキストを保持するのに十分な大きさの場合だけです。  
  
## <a name="see-also"></a>参照  
 [空間結果ウィンドウ](spatial-results-window.md)   
 [データベースエンジンクエリエディター &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)   
 [クエリエディターとテキストエディター &#40;SQL Server Management Studio&#41;](query-and-text-editors-sql-server-management-studio.md)  
  
  
