---
title: Transact-SQL スクリプトの再生 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 62ca5b9038a8c5cfd7590ed2754691266a691c5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906083"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Transact-SQL スクリプトの再生 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  パフォーマンスの問題に対して考えられる解決策をテストする場合、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを再生し、変更を加える前と加えた後のパフォーマンスを比較します。  
  
### <a name="to-replay-a-transact-sql-script"></a>Transact-SQL スクリプトを再生するには  
  
1.  **[ファイル]** メニューの **[開く]** をポイントし、 **[スクリプト ファイル]** をクリックします。  
  
2.  [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルを選択して開きます。 再生に必要なイベントが [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトに含まれていることを確認してください。 詳細については、「 [再生を実行するための必要条件](../../tools/sql-server-profiler/replay-requirements.md)」を参照してください。  
  
3.  **[再生]** メニューの **[開始]** をクリックし、スクリプトを再生するサーバーに接続します。  
  
4.  **[構成の再生]** ダイアログ ボックスで設定を確認し、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [トレースの再生](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
