---
title: トレース結果のテーブルへの保存 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9191c2ab44f4152a54211a1a66a5d843c0d6c12c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928758"
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>トレース結果のテーブルへの保存 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、トレース結果をデータベース テーブルに保存する方法について説明します。  
  
### <a name="to-save-trace-results-to-a-table"></a>トレース結果をテーブルに保存するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレース名]** ボックスにトレースの名前を入力し、 **[テーブルに保存]** チェック ボックスをオンにします。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで、トレース テーブルを格納する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続します。  
  
4.  **[キャプチャ先テーブル]** ダイアログ ボックスで、 **[データベース]** ボックスの一覧からデータベースを選択します。  
  
5.  **[所有者]** ボックスの一覧で、トレースの所有者を選択します。  
  
6.  **[テーブル]** ボックスの一覧で、トレース結果用のテーブルの名前を入力または選択します。 クリックして **OK.**  
  
7.  **[トレースのプロパティ]** ダイアログ ボックスで、 **[最大行数の設定 (1000 行単位)]** チェック ボックスをオンにして、保存する最大行数を指定します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
