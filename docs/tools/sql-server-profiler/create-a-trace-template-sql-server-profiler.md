---
title: トレーステンプレートを作成する (SQL Server プロファイラー) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- saving trace template
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 90e0563fac5a8ff1619abb946d7b35207d47f706
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223764"
---
# <a name="create-a-trace-template-sql-server-profiler"></a>トレース テンプレートの作成 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して新しいトレース テンプレートを作成する方法について説明します。  
  
### <a name="to-create-a-trace-template"></a>トレース テンプレートを作成するには  
  
1.  **[ファイル]** メニューの **[テンプレート]** をポイントし、 **[新しいテンプレート]** をクリックします。  
  
2.  **[トレース テンプレートのプロパティ]** ダイアログ ボックスで、 **[サーバーの種類の選択]** ボックスの一覧でサーバーの種類を選択します。  
  
3.  **[新しいテンプレート名]** ボックスにテンプレート名を入力します。  
  
4.  必要に応じて、 **[既存のテンプレートを基に新しいテンプレートを作成する]** をクリックし、一覧からテンプレートを選択します。  
  
     すべてのイベント、データ列、フィルターは、最初、選択したテンプレートで指定されたとおりに設定されています。  
  
5.  必要に応じて、 **[選択したサーバーの種類に対する既定のテンプレートとして使用する]** をクリックします。  
  
6.  **[イベントの選択]** タブで、イベント、データ列、またはフィルターの追加、削除、変更を行います。  
  
7.  **[イベントの選択]** タブで、グリッド コントロールを使用して、次のようにトレース ファイルに対するイベントとデータ列の追加または削除を行います。  
  
    -   イベントを追加するには、 **[イベント]** 列の適切なイベント カテゴリを展開し、イベント名を選択します。  
  
    -   イベントを追加すると、関連するすべてのデータ列が既定で含まれます。 トレースからイベントのデータ列を削除するには、そのイベントのデータ列のチェック ボックスをオフにします。  
  
    -   フィルターを追加するには、データ列名をクリックし、 **[フィルターの編集]** ダイアログ ボックスにフィルターの条件を指定します。 また、データ列名を右クリックし、 **[列フィルターの編集]** をクリックすることによっても **[フィルターの編集]** ダイアログ ボックスを起動できます。 **[OK]** をクリックしてフィルターを追加します。  
  
8.  **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [トレース ファイルに含めるイベントとデータ列の指定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server プロファイラーのテンプレートと権限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
