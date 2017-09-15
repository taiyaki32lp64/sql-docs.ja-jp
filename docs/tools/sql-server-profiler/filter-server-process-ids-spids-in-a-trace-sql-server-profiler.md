---
title: "トレース (SQL Server Profiler) でサーバー プロセス Id (Spid) をフィルター処理 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 33c0ad1e5302b48f1a77070f1f967f07d15b1fdb
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>トレースでのサーバー プロセス ID (SPID) のフィルター選択 (SQL Server Profiler)
  このトピックでは、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して、トレースでサーバー プロセス ID (SPID) をフィルター選択する方法について説明します。  
  
### <a name="to-filter-system-ids-in-a-trace"></a>トレースでシステム ID をフィルター選択するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]**をクリックし、SQL Server のインスタンスに接続します。  
  
     **[トレースのプロパティ]**ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]**チェック ボックスがオンになっている場合、 **[トレースのプロパティ]**ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]**メニューの **[オプション]**をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[使用するテンプレート]**ボックスの一覧で、トレース テンプレートを選択します。  
  
4.  必要に応じて、トレース結果の保存先ファイルまたは保存先テーブルを指定します。  
  
5.  **[イベントの選択]**タブで、 **[SPID]**列見出しをクリックして **[フィルターの編集]** ダイアログ ボックスを表示します。 このダイアログ ボックスは、列見出しを右クリックして **[列フィルターの編集]**をクリックしても表示することができます。 **[SPID]** 列が表示されていない場合は、 **[すべての列を表示する]** チェック ボックスをオンにします。  
  
6.  **[フィルターの編集]** ダイアログ ボックスで適切な比較演算子を展開し、比較の値として SPID を入力します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  