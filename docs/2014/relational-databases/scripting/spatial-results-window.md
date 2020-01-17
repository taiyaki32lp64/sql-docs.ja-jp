---
title: '[空間結果] ウィンドウ'
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2d5a477-6496-4d01-adee-7322ebdfadf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c554959fedba58f743f1dd37d3c97554d0f00d3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243247"
---
# <a name="spatial-results-window"></a>[空間結果] ウィンドウ
  [**空間結果**] ウィンドウには、空間データを表示するための視覚的なマッピングツールが用意されています。 空間結果を表示するには、geometry 型または geography 型のデータを含む空間列がクエリ結果に含まれている必要があります。  
  
> [!NOTE]  
>  
  **[空間結果]** ウィンドウを使用できるのは、 **[結果]** ウィンドウ内のグリッドに結果が返される場合だけです。 結果がテキストとして返されるように設定すると、このウィンドウは使用できません。  
  
## <a name="options"></a>オプション  
 **空間列の選択**  
 クエリ結果の空間列から、表示する空間列を指定します。 列は、一度に 1 つしか選択できません。  
  
 **ラベル列の選択**  
 クエリ結果に返された列から、空間データにラベルを付けるための空間列以外の列を指定します。 列は、一度に 1 つしか選択できません。  
  
 クエリで Point インスタンスのみが返される場合は、このオプションを使用できません。  
  
 **プロジェクションの選択**  
 geography 型のデータを、正距円筒図法、メルカトル図法、ロビンソン図法、ボンヌ図法という 4 つの投影法のいずれかで表示します。  
  
 このオプションは、geometry 型のデータには使用できません。  
  
 **倍率**  
 指数スケール上でマップの表示を調整します。  
  
 **グリッド線の表示**  
 座標グリッド線の表示と非表示を切り替えます。  
  
 多角形の場合、ラベルが表示されるのは、図形がラベルのテキストを保持するのに十分な大きさの場合だけです。 小さい図形にラベルを表示するには、ズームを調整します。  
  
> [!NOTE]  
>  Point インスタンスにラベルを付けることはできません。  
  
## <a name="see-also"></a>参照  
 [オブジェクトエクスプローラーでの空間データの表示](view-spatial-data-in-object-explorer.md)   
 [空間データ &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [データベースエンジンクエリエディター &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)   
 [クエリエディターとテキストエディター &#40;SQL Server Management Studio&#41;](query-and-text-editors-sql-server-management-studio.md)  
  
  
