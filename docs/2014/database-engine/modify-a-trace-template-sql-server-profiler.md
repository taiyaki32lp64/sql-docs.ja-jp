---
title: 変更のトレース テンプレート (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- modifying traces
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64c13b9fed062b73de7ab35ef5048ae4b68e5618
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090001"
---
# <a name="modify-a-trace-template-sql-server-profiler"></a>トレース テンプレートの変更 (SQL Server Profiler)
  このトピックでは、[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] を使用してトレース テンプレートを変更する方法について説明します。  
  
### <a name="to-modify-a-trace-template"></a>トレース テンプレートを変更するには  
  
1.  **[ファイル]** メニューの **[テンプレート]** をポイントし、 **[テンプレートのエクスポート]** をクリックします。  
  
2.  **[トレース テンプレートのプロパティ]** ダイアログ ボックスの **[全般]** タブで、サーバーの種類とテンプレート名を変更するか、そのサーバーの種類の既定のテンプレートを使用することを選択します。  
  
3.  **[イベントの選択]** タブで、グリッド コントロールを使用して、次のようにトレース ファイルに対するイベントとデータ列の追加または削除を行います。  
  
    -   イベントを追加するには、 **[イベント]** 列の適切なイベント カテゴリを展開し、イベント名を選択します。  
  
    -   イベントを追加すると、関連するすべてのデータ列が既定で含まれます。 トレースからイベントのデータ列を削除するには、そのイベントのデータ列のチェック ボックスをオフにします。  
  
    -   フィルターを追加するには、データ列名をクリックし、 **[フィルターの編集]** ダイアログ ボックスにフィルターの条件を指定します。 また、データ列名を右クリックし、 **[列フィルターの編集]** をクリックすることによっても **[フィルターの編集]** ダイアログ ボックスを起動できます。 **[OK]** をクリックしてフィルターを追加します。  
  
4.  **[保存]** をクリックするか、 **[名前を付けて保存]** をクリックして別の名前でトレース テンプレートを保存します。  
  
## <a name="see-also"></a>関連項目  
 [トレース ファイルに含めるイベントとデータ列の指定 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server プロファイラーのテンプレートと権限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
