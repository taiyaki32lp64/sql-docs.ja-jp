---
title: トレーステンプレートの変更 |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- modifying trace templates
- SQL Server Profiler, templates
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 55a7cdf539a675fd6d3c86ace8cc837ed1e92358
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074873"
---
# <a name="modify-trace-templates"></a>トレース テンプレートの変更
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を実行しているローカル コンピューター上のファイルに保存されたテンプレートは変更することができます。 また、それらのファイルから派生したテンプレートも変更できます。 既存のテンプレートを変更する場合は、 **[トレースのプロパティ]** ダイアログ ボックスの **[イベントの選択]** タブで、最初にプロパティを設定したときと同じ順序で、イベント クラスやデータ列などのテンプレートのプロパティを編集します。 イベント クラスとデータ列は追加または削除することができ、フィルターは変更することができます。 テンプレートを変更すると、ユーザー固有のテンプレートが作成されます。元のシステム テンプレートは変更されません。 詳細については、「 [トレースとトレース テンプレートの保存](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)」を参照してください。  
  
 トレースを作成したときに使用した元のテンプレートを覚えていない (または保存していなかった) 場合や、後日同じトレースを実行する場合など、既存のトレース ファイルからテンプレートを派生させる必要が生じることがあります。 既存のトレースを使用する場合、プロパティを参照できますが、変更できません。 プロパティを変更するには、トレースを停止または一時停止する必要があります。 詳細については、「[トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)」および「[実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)」を参照してください。  
  
## <a name="to-modify-a-trace-template"></a>トレース テンプレートを変更するには  
  
1.  **[ファイル]** メニューの **[テンプレート]** をポイントし、 **[テンプレートのエクスポート]** をクリックします。  
  
2.  **[トレース テンプレートのプロパティ]** ダイアログ ボックスの **[全般]** タブで、サーバーの種類とテンプレート名を変更するか、そのサーバーの種類の既定のテンプレートを使用することを選択します。  
  
3.  **[イベントの選択]** タブで、グリッド コントロールを使用して、次のようにトレース ファイルに対するイベントとデータ列の追加または削除を行います。  
  
    -   イベントを追加するには、 **[イベント]** 列の適切なイベント カテゴリを展開し、イベント名を選択します。  
  
    -   イベントを追加すると、関連するすべてのデータ列が既定で含まれます。 トレースからイベントのデータ列を削除するには、そのイベントのデータ列のチェック ボックスをオフにします。  
  
    -   フィルターを追加するには、データ列名をクリックし、 **[フィルターの編集]** ダイアログ ボックスにフィルターの条件を指定します。 また、データ列名を右クリックし、 **[列フィルターの編集]** をクリックすることによっても **[フィルターの編集]** ダイアログ ボックスを起動できます。 **[OK]** をクリックしてフィルターを追加します。  
  
4.  **[保存]** をクリックするか、 **[名前を付けて保存]** をクリックして別の名前でトレース テンプレートを保存します。  
  
## <a name="next-steps"></a>次の手順  
[トレースを開始する](../../tools/sql-server-profiler/start-a-trace.md)  
[トレースを作成する](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
[Transact-SQL を使用して既存のトレースを変更する](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
[SQL Server Profiler を使用してトレース ファイルに含めるイベントとデータ列を指定する](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
[sp-trace-setevent-transact-sql](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
