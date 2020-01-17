---
title: トレース (SQL Server Profiler) を一時停止 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4961b68d46f8e4f1627c28c05ab2efb609d9f90d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240473"
---
# <a name="pause-a-trace-sql-server-profiler"></a>トレースの一時停止 (SQL Server Profiler)
  トレースを一時停止すると、トレースを再開するまで、それ以上のイベント データはキャプチャされません。  
  
 トレースを一時停止すると、トレースを再開するまで、それ以上のイベント データはキャプチャされません。 トレースを再開すると、トレース操作が再開されます。 キャプチャを再開しても、それ以前にキャプチャしたデータが失われることはありません。 トレースを再開すると、その時点から、データのキャプチャが再開されます。 トレースを一時停止している間は、名前、イベント、列、およびフィルターを変更することができます。 ただし、トレース データの送信先またはサーバー接続は変更できません。  
  
### <a name="to-pause-a-trace"></a>トレースを一時停止するには  
  
1.  実行中のトレースを含んでいるウィンドウを選択します。  
  
2.  **[ファイル]** メニューの **[トレースの一時停止]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
