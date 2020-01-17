---
title: トレースの停止 (SQL Server プロファイラー) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], stopping
- stopping traces
ms.assetid: 47c4f33d-63e0-4444-bec8-4c1c91f8e25c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d574d3b18b47c4860f710f933ac9ba50a54db270
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059632"
---
# <a name="stop-a-trace-sql-server-profiler"></a>トレースの停止 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、実行中のトレースを停止する方法について説明します。  
  
 トレースを停止すると、データのキャプチャも停止します。 トレースを停止した場合、トレースを再開すると、既にキャプチャしたデータは失われます。ただし、トレース ファイルまたはトレース テーブルにキャプチャしたデータが失われることはありません。 トレースを停止した後に、キャプチャしたデータをテーブルまたはファイルに保存することは可能です。 トレースを停止しても、あらかじめ選択されているすべてのトレース プロパティは保存されます。 トレースを停止した後は、名前、イベント、列、およびフィルターを変更できます。  
  
### <a name="to-stop-a-trace"></a>トレースを停止するには  
  
1.  実行中のトレースを選択します。  
  
2.  **[ファイル]** メニューの **[トレースの停止]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
