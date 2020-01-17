---
title: トレースを実行するための Transact-SQL スクリプトの作成 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], running
- scripts [SQL Server], traces
ms.assetid: 6b0e2519-998d-40d5-b8ba-5e6a773f91a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 948ef7eb5fdfeabdbb2ba3829e172f7c9f4028da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255813"
---
# <a name="create-a-transact-sql-script-for-running-a-trace-sql-server-profiler"></a>トレースを実行するための Transact-SQL スクリプトの作成 (SQL Server Profiler)
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、既存のトレース ファイルまたはトレース テーブルから Transact-SQL スクリプトを作成する方法について説明します。  
  
### <a name="to-create-a-transact-sql-script-to-run-a-trace"></a>トレースを実行するための Transact-SQL スクリプトを作成するには  
  
1.  トレース ファイルまたはトレース テーブルを開きます。 詳細については、「 [トレース ファイルを開く &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) や [トレース テーブルを開く &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)に付属の定義済みチューニング テンプレートを使用します。  
  
2.  **[ファイル]** メニューで **[エクスポート]** 、 **[トレース定義のスクリプト]** の順にポイントし、トレースするサーバーに対応するバージョンをクリックします。  
  
3.  **[名前を付けて保存]** ダイアログ ボックスで、スクリプト ファイルの名前を入力し、 **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server プロファイラーのテンプレートと権限](sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
