---
title: オブジェクト エクスプローラーでの空間データの表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: facb39a333d148bad2f50c2d87899c308f155168
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252721"
---
# <a name="view-spatial-data-in-object-explorer"></a>オブジェクト エクスプローラーでの空間データの表示
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  クエリ エディターの **[空間結果]** ウィンドウには、 **[結果]** ウィンドウにグリッド形式で表示されるデータに加えて、空間データ結果を表示するための視覚的なマッピング ツールが用意されています。 **[空間結果]** ウィンドウに空間データを表示するには、geometry 型または geography 型のデータを含む空間データ列が少なくとも 1 つクエリ結果に含まれている必要があります。  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>[空間結果] ウィンドウに空間データを表示するには  
  
1.  クエリ エディターで、 **[空間結果]** タブをクリックします。  
  
    > [!NOTE]  
    >  クエリ結果に空間データが含まれていない場合、または結果がテキストとして返されるように指定した場合、このウィンドウは使用できません。  
  
2.  **[空間列の選択]** の一覧から、表示する列を選択します。 テーブル内に空間列が 1 つしかない場合は、この列が一覧の既定のオプションです。  
  
3.  **[ラベル列の選択]** の一覧から、データ ラベルとして使用する、空間列以外の列を選択します。  
  
4.  **[投影の選択]** の一覧から、geography 型のデータに使用する投影法を選択します。 既定の投影法は正距円筒図法です。その他に、メルカトル図法、ロビンソン図法、およびボンヌ図法という投影法を使用できます。  
  
    > [!NOTE]  
    >  空間列に geometry 型のデータが含まれている場合、 **[投影の選択]** は使用できません。  
  
5.  **[ズーム]** スライダーを調整して、マップされた要素の視覚的なサイズを大きくします。 多角形の場合、ラベルが表示されるのは、図形がラベルのテキストを保持するのに十分な大きさの場合だけです。  
  
## <a name="see-also"></a>参照  
 [[空間結果] ウィンドウ](../../relational-databases/scripting/spatial-results-window.md)   
 [データベース エンジン クエリ エディター &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)   
 [クエリおよびテキスト エディター &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
