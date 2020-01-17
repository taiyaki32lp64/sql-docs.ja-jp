---
title: トレースでのサーバー プロセス ID (SPID) のフィルター選択 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 172ba4b6cb2ed5bee84d920f8b7e0c73de3b8e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075011"
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>トレースでのサーバー プロセス ID (SPID) のフィルター選択 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、トレースでサーバー プロセス ID (SPID) をフィルター選択する方法について説明します。  
  
### <a name="to-filter-system-ids-in-a-trace"></a>トレースでシステム ID をフィルター選択するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、SQL Server のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[使用するテンプレート]** ボックスの一覧で、トレース テンプレートを選択します。  
  
4.  必要に応じて、トレース結果の保存先ファイルまたは保存先テーブルを指定します。  
  
5.  **[イベントの選択]** タブで、 **[SPID]** 列見出しをクリックして **[フィルターの編集]** ダイアログ ボックスを起動します。 このダイアログ ボックスは、列見出しを右クリックして **[列フィルターの編集]** をクリックしても表示することができます。 **[SPID]** 列が表示されていない場合は、 **[すべての列を表示する]** チェック ボックスをオンにします。  
  
6.  **[フィルターの編集]** ダイアログ ボックスで適切な比較演算子を展開し、比較の値として SPID を入力します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
