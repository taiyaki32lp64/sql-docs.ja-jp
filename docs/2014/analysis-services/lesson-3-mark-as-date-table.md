---
title: レッスン 4:日付テーブルとしてマーク |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26877c4892b050cbf9c8dcc6553530dff513f8fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078786"
---
# <a name="lesson-4-mark-as-date-table"></a>レッスン 4:日付テーブルとしてマーク
  「レッスン 2。DimDate をという名前のディメンション テーブルをインポートしたデータを追加します。 レッスン 3 で、DimDate テーブルが変更されます。単純な Date に、列の名前を変更します。 このモデルでは、このテーブルは Date という名前になりましたが、実際は日付と時刻のデータが含まれた*日付テーブル*になります。  
  
 計算でタイム インテリジェンス関数を使用する場合は必ず、少し後でメジャーを作成することになるので、 *Date table* と、そのテーブル内で一意の識別子である *Date column* を含む日付テーブル プロパティを指定する必要があります。 他のテーブルと日付テーブルの間で有効なリレーションシップを作成できます。これは、DAX のタイム インテリジェンス機能を使用して計算するために必要です。  
  
 このレッスンでは、インポートされ名前を変更された Date テーブルを *日付テーブル* 、Date テーブルの Date 列を *日付列* (一意識別子) として設定します。 日付が、混乱の種類、名前のすべての使用をすぐに理解しています。  
  
 このレッスンを完了するまでに時間を推定するには。**3 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 3:列名の変更](rename-columns.md)します。  
  
### <a name="to-set-mark-as-date-table"></a>日付テーブルとして設定する  
  
1.  モデル デザイナーで、 **Date** テーブル (タブ) をクリックします。  
  
2.  **[テーブル]** メニュー、 **[日付]** **[日付テーブルとしてマーク]** の順にクリックします。  
  
3.  **[日付テーブルとしてマーク]** ダイアログ ボックスの **[日付]** ボックスの一覧で、一意の識別子として **[Date]** 列を選択します。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。[レッスン 5: リレーションシップの作成](lesson-4-create-relationships.md)です。  
  
  
