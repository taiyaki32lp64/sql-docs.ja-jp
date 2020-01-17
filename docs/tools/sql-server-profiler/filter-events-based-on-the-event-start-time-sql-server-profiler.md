---
title: イベントの開始時刻に基づいたイベントのフィルター選択 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event start times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: e965579e-d006-41a3-89ec-cfd5398c67d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1e0dddb26a2ea89635f995c5d1c270d1454b3b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930006"
---
# <a name="filter-events-based-on-the-event-start-time-sql-server-profiler"></a>イベントの開始時刻に基づいたイベントのフィルター選択 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、トレース イベントをイベントの開始時刻に基づいてフィルター選択する方法について説明します。  
  
### <a name="to-filter-an-event-based-on-the-event-start-time"></a>イベントの開始時刻に基づいてイベントをフィルター選択するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[使用するテンプレート]** ボックスの一覧で、トレース テンプレートを選択します。  
  
4.  必要に応じて、トレース結果の保存先を指定します。  
  
5.  **[イベントの選択]** タブで、 **[StartTime]** 列見出しをクリックします。 また、この列見出しを右クリックし、 **[列フィルターの編集]** をクリックして **[フィルターの編集]** ダイアログ ボックスを開く方法もあります。  
  
6.  **[次の値より大きい]** または **[次の値より小さい]** を展開して、その下に表示されるフィールドに **datetime** 値を入力します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
