---
title: トレース ファイルに含めるイベントとデータ列の指定 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- adding events
- traces [SQL Server], data columns
- deleting events
- removing events
- traces [SQL Server], events
ms.assetid: 7da715a3-2f03-4063-b6a4-20fd7b44e675
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33e11dde29a9f2b016f5f70fa3c12bd728928f93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267417"
---
# <a name="specify-events-and-data-columns-for-a-trace-file-sql-server-profiler"></a>トレース ファイルに含めるイベントとデータ列の指定 (SQL Server Profiler)
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用してトレースに含めるイベント クラスとデータ列を指定する方法について説明します。  
  
### <a name="to-specify-events-and-data-columns-for-a-trace"></a>トレースに含めるイベントとデータ列を指定するには  
  
1.  **[トレースのプロパティ]** または **[トレース テンプレートのプロパティ]** ダイアログ ボックスで、 **[イベントの選択]** タブをクリックします。  
  
     **[イベントの選択]** タブにはグリッド コントロールがあります。 グリッド コントロールは、トレース可能な各イベント クラスを含んでいるテーブルです。 このテーブルには、各イベント クラスが 1 行で表示されます。 表示されるイベント クラスは、接続しているサーバーの種類とバージョンによって多少異なります。 イベント クラスは、グリッドの **[イベント]** 列で識別され、イベント カテゴリ別に分類されています。 残りの列には、各イベント クラスに対応するデータ列が表示されます。  
  
2.  **[イベントの選択]** タブで、グリッド コントロールを使用して、トレース ファイルに対するイベントとデータ列の追加または削除を行います。  
  
3.  トレースからイベントを削除するには、各イベント クラスの **[Events]** 列のチェック ボックスをオフにします。  
  
4.  トレースにイベントを含めるには、各イベント クラスの **[Events]** 列のチェック ボックスをオンにするか、イベントに対応するデータ列のチェック ボックスをオンにします。  
  
> [!IMPORTANT]  
>  このトレースをシステム モニターやパフォーマンス モニターのデータと関連付ける場合は、 **Start Time** データ列と **End Time** データ列の両方をトレースに含める必要があります。  
  
 イベント クラスを含める場合、イベントに対応するイベント クラスのチェック ボックスをオンにしていると、関連するデータ列もすべてトレースに含まれます。 特定の列のチェック ボックスをオンにしている場合は、その列だけがトレースに含まれます。  
  
1.  イベント クラスからデータ列を削除するには、イベント クラス行のデータ列のチェック ボックスをオフにするか、列ヘッダーを右クリックして、 **[列の選択解除]** をクリックします。  
  
2.  必要に応じて、トレースにフィルターを適用します。 詳細については、「[トレース内のイベントへのフィルターの適用 &#40;SQL Server Profiler&#41;](filter-events-in-a-trace-sql-server-profiler.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
