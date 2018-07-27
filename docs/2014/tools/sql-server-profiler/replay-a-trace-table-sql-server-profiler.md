---
title: 再生トレース テーブル (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 6a0ad817-3d8d-4495-889d-c66a7ef9e8bb
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0125b1911383d735b2329594207c6560c06351bb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319902"
---
# <a name="replay-a-trace-table-sql-server-profiler"></a>トレース テーブルの再生 (SQL Server Profiler)
  再生は、保存したトレースを開いて再実行する機能です。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] には、ユーザー接続と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証をシミュレートできるマルチスレッド再生エンジンが備わっています。 再生は、アプリケーションまたはプロセスに関する問題のトラブルシューティングを行う際に役立ちます。 問題を特定して修正を実装したら、修正されたアプリケーションまたはプロセスに対して、発生する可能性のある問題を検出したトレースを実行します。 その後、元のトレースを再生し、結果を比較します。  
  
 再生を有効にするには、監視する他のイベント クラスに加えて、特定のイベント クラスをキャプチャする必要があります。 **TSQL_Replay** トレース テンプレートを使用すると、これらのイベントが既定でキャプチャされます。 詳細については、「 [再生を実行するための必要条件](replay-requirements.md)」を参照してください。  
  
### <a name="to-replay-a-trace-table"></a>トレース テーブルを再生するには  
  
1.  再生に必要なイベント クラスが含まれたトレース テーブルを開きます。  
  
2.  **[再生]** メニューの **[開始]** をクリックし、トレースを再生するサーバー インスタンスに接続します。  
  
3.  **[構成の再生]** ダイアログ ボックスの **[再生オプションの基本設定]** タブで、 **[再生サーバー]** を指定します。 **[再生サーバー]** ボックスに表示されているサーバーを変更するには、 **[変更]** をクリックします。  
  
4.  必要に応じて、再生の保存先として次のいずれかを選択します。  
  
    -   **[ファイルに保存]** : 再生の保存先となるファイルを指定します。  
  
    -   **[テーブルに保存]**: 再生の保存先となるデータベース テーブルを指定します。  
  
5.  **[トレースされた順番にイベントを再生します。このオプションはデバッグを有効にします。]** または **[複数のスレッドを使用してイベントを再生します。このオプションはパフォーマンスを最適にし、デバッグを無効にします。]** のいずれかを選択します。 次の表では、これらの設定の違いについて説明します。  
  
    |オプション|説明|  
    |------------|-----------------|  
    |**[トレースされた順番にイベントを再生します。このオプションはデバッグを有効にします。]**|記録された順番にイベントを再生します。 このオプションにより、デバッグが有効になります。|  
    |**[複数のスレッドを使用してイベントを再生します。このオプションはパフォーマンスを最適にし、デバッグを無効にします。]**|このオプションでは、複数のスレッドを使用して、順序に関係なく各イベントを再生します。 このオプションにより、パフォーマンスが最適化されます。|  
  
6.  **[再生結果を表示する]** チェック ボックスをオンにすると、実行時に再生が表示されます。  
  
7.  必要に応じて、 **[再生オプションの詳細設定]** タブをクリックし、次のオプションを指定します。  
  
    -   すべてのサーバー プロセス ID (SPID) を再生するには、 **[システム SPID を再生する]** チェック ボックスをオンにします。  
  
    -   特定の SPID に属しているプロセスに再生を制限するには、 **[1 つの SPID のみ再生する]** チェック ボックスをオンにします。 **[再生する SPID]** ボックスには、SPID を入力します。  
  
    -   特定の期間に発生したイベントを再生するには、 **[日時により再生を制限する]** チェック ボックスをオンにします。 **[開始時刻]** と **[終了時刻]** の日時を選択し、再生に含める期間を指定します。  
  
    -   再生中の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によるプロセスの管理方法を制御するには、 **[ヘルス モニター オプション]** を構成します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler の実行に必要な権限](sql-server-profiler.md)   
 [トレースを再生します。](replay-traces.md)   
 [トレース テーブルを開く &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  