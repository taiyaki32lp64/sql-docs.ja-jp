---
title: トレース結果のテーブルへの保存 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8571f7273cc2667040ffffc8ffbfb0df4e2a6ef6
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792688"
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>トレース結果のテーブルへの保存 (SQL Server Profiler)
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
  
6.  **[テーブル]** ボックスの一覧で、トレース結果用のテーブルの名前を入力または選択します。 **[OK]** をクリックします。  
  
7.  **トレースのプロパティ**ダイアログ ボックスで、**設定行の最大数 (1000)** を保存する行の最大数を指定する チェック ボックス。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
