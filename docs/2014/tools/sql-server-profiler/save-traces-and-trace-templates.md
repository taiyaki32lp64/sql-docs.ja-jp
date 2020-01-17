---
title: トレースとトレース テンプレートの保存 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- exporting trace templates
- importing trace templates
- SQL Server Profiler, templates
ms.assetid: 957e6bf8-e7a3-4a59-a1cd-0a41538a8158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4baca63080a3f67c1f9e54a8a0aa955a27029df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267428"
---
# <a name="save-traces-and-trace-templates"></a>トレースとトレース テンプレートの保存
  トレース ファイルの保存とトレース テンプレートの保存は、区別して考えることが重要です。 トレース ファイルを保存すると、キャプチャされたイベント データが特定の場所に保存されます。 トレース テンプレートを保存すると、特定のデータ列、イベント クラス、フィルターなどのトレースの定義が保存されます。  
  
## <a name="saving-traces"></a>トレースの保存  
 キャプチャしたイベント データの分析や再生を後で行う必要がある場合、データをファイルまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存します。 トレース ファイルは、次の用途に使用します。  
  
-   トレース ファイルまたはトレース テーブルから、データベース エンジン チューニング アドバイザーへの入力として使用するワークロードを生成します。  
  
-   トレース ファイルを使用してイベントをキャプチャし、そのトレース ファイルを分析のためにサポート プロバイダーに送信します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクエリ処理ツールを使用して、データにアクセスしたり、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]でデータを表示したりします。 ただし、トレース テーブルに直接アクセスできるのは、 **sysadmin** 固定サーバー ロールのメンバーとテーブルの作成者だけです。  
  
> [!NOTE]  
>  トレース データをテーブルにキャプチャすると、ファイルにキャプチャする場合と比べて操作に時間がかかります。 テーブルにキャプチャする代わりに、トレース データをファイルにキャプチャしておき、このトレース ファイルを開き、トレースをトレース テーブルとして保存する方法があります。  
  
 トレース ファイルを使用する場合、キャプチャしたイベント データ (トレース定義ではない) は [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] により [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレース (\*.trc) ファイルに保存されます。 この拡張子は、トレース ファイルを保存するときに、他の拡張子が指定されているかどうかに関係なくファイル名の終わりに自動的に付加されます。 たとえば、 **Trace.dat**という名前のトレース ファイルを指定すると、作成されるファイルの名前は **Trace.dat.trc**になります。  
  
> [!IMPORTANT]  
>  SHOWPLAN 権限、ALTER TRACE 権限、または VIEW SERVER STATE 権限を持つユーザーは、プラン表示出力にキャプチャされたクエリを表示できます。 これらのクエリには、パスワードなどの機密情報が含まれている場合があります。 したがって、これらの権限は、機密情報を表示することが認められているユーザー (たとえば **db_owner** 固定データベース ロールのメンバーや **sysadmin** 固定サーバー ロールのメンバー) のみに付与することをお勧めします。 また、プラン表示ファイルまたはプラン表示関連のイベントを含むトレース ファイルのみを保存すること、保存先は NTFS ファイル システムが使用されている場所とすること、および機密情報を表示する権限を持つユーザーのみにアクセスを制限することをお勧めします。  
  
## <a name="saving-templates"></a>テンプレートの保存  
 トレースのテンプレート定義には、トレースの作成に使用するイベント クラス、データ列、フィルター、およびその他のすべてのプロパティ (キャプチャしたイベント データは除く) が含まれています。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] にはシステム テンプレートがあらかじめ定義されていて、これを使用することでトレースの一般的な作業、およびデータベース エンジン チューニング アドバイザーで物理的なデータベース デザインをチューニングするためのワークロードを作成するなどの特定の作業を行うことができます。 ユーザー定義テンプレートを作成して保存することもできます。  
  
### <a name="importing-and-exporting-templates"></a>テンプレートのインポートとエクスポート  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して、サーバー間でテンプレートのインポートとエクスポートを行うことができます。 テンプレートをエクスポートすると、既存のテンプレートのコピーが指定したディレクトリに移動されます。 テンプレートをインポートすると、指定したテンプレートのコピーが作成されます。 インポートまたはエクスポートしたテンプレートは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で表示したときにテンプレート名の後に "(ユーザー)" という語が付いて、システム テンプレートと区別されます。 あらかじめ定義されているシステム テンプレートを上書きしたり、直接変更したりすることはできません。  
  
### <a name="analyzing-performance-with-templates"></a>テンプレートを使用したパフォーマンスの分析  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を頻繁に監視する場合は、テンプレートを使用してパフォーマンスを分析してください。 テンプレートを使用すれば、同一のイベント データを毎回キャプチャし、同一のトレース定義で同一のイベントを監視できます。 トレースを作成するたびにイベント クラスやデータ列を定義する必要はありません。 さらに、特定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントを監視するために、テンプレートを他のユーザーに提供できます。 たとえば、サポート プロバイダーから顧客にテンプレートを提供できます。 顧客はこのテンプレートを使用して必要なイベント データをキャプチャし、キャプチャしたデータを分析のためサポート プロバイダーに送信します。  
  
 **トレースをファイルに保存するには**  
  
 [トレース結果のファイルへの保存 &#40;SQL Server Profiler&#41;](save-trace-results-to-a-file-sql-server-profiler.md)  
  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)  
  
## <a name="see-also"></a>参照  
 [トレース結果のテーブルへの保存 &#40;SQL Server Profiler&#41;](save-trace-results-to-a-table-sql-server-profiler.md)   
 [トレース テンプレートの作成 &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)   
 [実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [トレース テンプレートのエクスポート &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)   
 [トレース テンプレートのインポート &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)  
  
  
