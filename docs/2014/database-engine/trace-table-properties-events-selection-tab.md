---
title: トレース テーブルのプロパティ (イベントの選択 タブ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetableproperties.eventsselection.f1
helpviewer_keywords:
- Trace Table Properties dialog box
ms.assetid: fa21df6a-b6b5-4b15-9104-957385821594
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 404b1d5d8467fe5840a6f53007bd55bc58cdf19f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089537"
---
# <a name="trace-table-properties-events-selection-tab"></a>[トレース テーブルのプロパティ] ([イベントの選択] タブ)
  **[トレース テーブルのプロパティ]** ダイアログ ボックスの **[イベントの選択]** タブを使用すると、トレースのイベントやデータ列プロパティを表示したり、トレースからイベントまたは列を削除したりできます。  
  
 このウィンドウを表示するには、 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] を使用してトレース テーブルを開きます。 次に、 **[ファイル]** メニューの **[プロパティ]** をクリックした後、 **[イベントの選択]** タブをクリックします。  
  
## <a name="options"></a>および  
 **[イベント]** 列  
 イベント カテゴリにより分類された、ビューによりトレースされるイベントです。 イベントのチェック ボックスをオンにするか、データ列をオンにすることでイベントを選択できます。 イベントのチェック ボックスをオンにすると、そのイベントで使用できるデータ列がすべて選択されます。 イベントのデータ列をオンにすると、イベントが選択されるだけでなく、そのほかに必要な列がすべて自動的に選択されます。 トレース ファイルまたはトレース テーブルを表示した場合、イベントのチェック ボックスやデータ列をオフにすることで、トレース ウィンドウに表示されるデータ量が減り、分析が容易になります。 列のフィルターを変更して、トレース ウィンドウに表示されるデータ量を減らすこともできます。 イベント クラスの詳細については、「 [SQL Server イベント クラスの参照](../relational-databases/event-classes/sql-server-event-class-reference.md)」を参照してください。  
  
 その他のデータ列  
 トレースされるデータ列を表示します。 トレースに含まれる各イベントでは、トレースの関連するデータ列は既定ですべてオンになっています。  
  
 フィルターを指定するには、データ列のヘッダーをクリックし、フィルター基準を入力します。 フィルター選択されるデータ列については、 **[フィルターの編集]** ダイアログ ボックスの列ラベルの左側にフィルターのアイコンが表示されます。  
  
 **[すべてのイベントを表示する]**  
 表示できるイベントをすべて表示します。 既定では、 **[イベントの選択]** グリッドで選択されている行だけが表示されます。 このチェック ボックスをオフにすると、 **[イベントの選択]** グリッドで選択されていないイベントがすべて非表示になります。 **[すべてのイベントを表示する]** がオンで、トレース ファイルまたはトレース テーブルを表示している場合、トレースに記録されたすべてのイベントがトレース ウィンドウに表示されます。  
  
 **[すべての列を表示]**  
 表示できるデータ列をすべて表示します。 既定では、選択されているデータ列だけが表示されます。 このチェック ボックスをオフにすると、 **[イベントの選択]** グリッドで選択されていないデータ列がすべて非表示になります。  
  
 **列フィルター**  
 **[フィルターの編集]** ダイアログ ボックスを起動します。ここでは、データ列のラベルの左側にフィルターのアイコンが表示されます。 このダイアログ ボックスを使用して、データ列のフィルターを編集できます。  
  
 **[列の構成]**  
 **[イベント]** およびトレースするデータ列を選択した後、 **[列の構成]** をクリックすると、トレース結果のウィンドウの列が並べ替えられます。  
  
## <a name="see-also"></a>参照  
 [トレース テーブルを開く &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [SQL Server プロファイラーのテンプレートと権限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
