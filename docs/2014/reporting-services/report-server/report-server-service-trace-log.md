---
title: Report Server Service Trace Log | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- logs [Reporting Services], trace
- traces [Reporting Services]
- system information [Reporting Services]
- versions [Reporting Services]
ms.assetid: 2fde08b2-137d-4f4b-88e5-216030216e0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d69b2a3eeb28d5fe23eb6674c8a0ca0ee7628a75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103407"
---
# <a name="report-server-service-trace-log"></a>Report Server Service Trace Log
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポート サーバーのトレース ログは、レポート サーバー Web サービス、レポート マネージャー、およびバックグラウンド処理によって実行された操作を含め、レポート サーバー サービスの操作に関する詳細な情報が記録されている ASCII テキスト ファイルです。 トレース ログ ファイルには、他のログ ファイルに記録されている冗長な情報、およびトレース ログ以外からは入手できない追加情報が含まれています。 トレース ログ情報は、レポート サーバーを含むアプリケーションをデバッグしている場合、またはイベント ログや実行ログに書き込まれた特定の問題を調査している場合に役立ちます。  
  
> [!NOTE]  
>  以前のリリースでは、複数のトレース ログ ファイル (アプリケーションごとに 1 つ) が存在しました。 次のファイルは廃止されており、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以上のバージョンでは作成されなくなりました。Reportserverwebapp _*\<タイムスタンプ >*.log、reportserver _*\<タイムスタンプ >* Reportserverservice_main _ .log、および*\<タイムスタンプ >*。 ログ。  
  
 **このトピックの内容:**  
  
-   [レポート サーバーのログ ファイルの場所](#bkmk_view_log)  
  
-   [トレースの構成設定](#bkmk_trace_configuration_settings)  
  
-   [ダンプ ファイルの場所を指定するカスタム構成設定を追加します。](#bkmk_add_custom)  
  
-   [ログ ファイル フィールド](#bkmk_log_file_fields)  
  
##  <a name="bkmk_view_log"></a> レポート サーバー のログ ファイルの場所  
 トレース ログ ファイルは `ReportServerService_<timestamp>.log` であり、以下のフォルダーにあります。  
  
 `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`  
  
 トレース ログは毎日作成され、午前 0 時 (ローカル時刻) 以降に発生する最初のエントリで始まります。また、サービスを再起動したときにも作成されます。 タイムスタンプには、協定世界時 (UTC) が使用されます。 このファイルは EN-US 形式です。 既定では、トレース ログのサイズの上限は 32 MBであり、14 日後に削除されます。  
  
 Microsoft Power Query を使用して [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ログ ファイルを表示する方法を示す短いビデオを表示します。  
  
 ![Power Query および SSRS ログに関するビデオを表示](../media/generic-video-thumbnail.png "Power Query および SSRS ログに関するビデオを表示")  
  
##  <a name="bkmk_trace_configuration_settings"></a> トレースの構成設定  
 トレース ログの動作は構成ファイル **ReportingServicesrService.exe.config** で管理されています。構成ファイルは次のフォルダー パスにあります。  
  
 `\Program Files\Microsoft SQL Server\MSRS12.<instance name>\Reporting Services\ReportServer\bin`。  
  
 次の例では、`RStrace` の設定の XML 構造を示しています。 `DefaultTraceSwitch` の値によって、ログに追加される情報の種類が決まります。 `Components` 属性を除き、`RStrace` の値は構成ファイル間で同じになります。  
  
```  
<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
```  
  
 次の表では、各設定に関する情報を示します。  
  
|設定|説明|  
|-------------|-----------------|  
|`RStrace`|エラーおよびトレースに使用される名前空間を指定します。|  
|`DefaultTraceSwitch`|ReportServerService トレース ログにレポートされる情報のレベルを指定します。 各レベルには、そのレベルより低いすべてのレベルでレポートされる情報が含まれます。 トレースを無効にすることはお勧めしません。 有効な値は、<br /><br /> 0= トレースの無効化。 ReportServerService ログ ファイルは既定で有効になります。 オフにする場合は、トレース レベルを 0 に設定します。<br /><br /> 1= 例外および再起動<br /><br /> 2= 例外、再起動、警告<br /><br /> 3= 例外、再起動、警告、状態メッセージ (既定)<br /><br /> 4= 詳細モード|  
|**FileName**|ログ ファイル名の最初の部分を指定します。 `Prefix` で指定した値が付加されて、完全な名前になります。|  
|**FileSizeLimitMb**|トレース ログのサイズの上限を指定します。 ファイルは MB 単位で測定されます。 正しい値は、0 から整数型の最大値までです。 既定値は 32 です。 0 または負の値を指定した場合、レポート サーバーでは値が 1 として扱われます。<br /><br /> トレース レベル (0 ～ 4) を設定して、ログに記録される内容を制御することにより、ファイル サイズを制御することができます。 また、トレースするコンポーネントを指定することもできます。 14 日間の有効期限が切れる前にログ ファイルが最大サイズに達すると、古いエントリが新しいエントリに置き換えられます。|  
|**KeepFilesForDays**|トレース ログ ファイルを削除するまでの保持期間を日数で指定します。 正しい値は、0 から整数型の最大値までです。 既定値は 14 です。 0 または負の値を指定した場合、レポート サーバーでは値が 1 として扱われます。|  
|`Prefix`|あるログのインスタンスを別のログのインスタンスと区別するために生成する値を指定します。 既定では、トレース ログ ファイル名にタイムスタンプの値が追加されます。 この値は、" tid, time " に設定されます。 この設定は変更しないでください。|  
|**TraceListeners**|トレース ログ コンテンツの出力先を指定します。 複数の出力先を指定する場合、各出力先をコンマで区切ってください。 有効な値は、<br /><br /> DebugWindow<br /><br /> File (既定値)<br /><br /> StdOut|  
|**TraceFileMode**|トレース ログに 24 時間データを含めるかどうかを指定します。 コンポーネントごとに、毎日 1 つ、一意のトレース ログが必要です。 この値は、"Unique (既定値)" に設定されます。 この値は変更しないでください。|  
|`Components`|トレース ログ情報の生成対象となるコンポーネントおよびトレース レベルを次の形式で指定します。<br /><br /> \<component category>:\<tracelevel><br /><br /> コンポーネントのカテゴリには次の値を設定できます。<br />特定のカテゴリに分類されないすべてのプロセスに対する通常のレポート サーバーの利用状況を追跡するには、`All` を使用します。<br />実行中のレポートまたはサブスクリプションの操作を追跡するには、`RunningJobs` を使用します。<br />ユーザーがモデルベースのレポートでアドホック データ探索を実行する場合に処理されるセマンティック クエリを追跡するには、`SemanticQueryEngine` を使用します。<br />モデルの生成を追跡するには、`SemanticModelGenerator` を使用します。<br />レポート サーバーの HTTP ログ ファイルを有効にするには、`http` を使用します。 詳しくは、「 [Report Server HTTP Log](report-server-http-log.md)」をご覧ください。<br /><br /> <br /><br /> トレース レベルの有効な値は次のとおりです。<br /><br /> 0= トレースの無効化<br /><br /> 1= 例外および再起動<br /><br /> 2= 例外、再起動、警告<br /><br /> 3= 例外、再起動、警告、状態メッセージ (既定)<br /><br /> 4= 詳細モード<br /><br /> レポート サーバーの既定値は "all:3" です。<br /><br /> コンポーネント (`all`、`RunningJobs`、`SemanticQueryEngine`、`SemanticModelGenerator`) のすべてまたは一部を指定できます。 特定のコンポーネントに関する情報を生成しない場合は、そのコンポーネントのトレースを無効にできます (たとえば "SemanticModelGenerator:0")。 `all` の場合は、トレースを無効にしないでください。<br /><br /> コンポーネントにトレース レベルを追加しない場合は、`DefaultTraceSwitch` に指定された値が使用されます。 たとえば、"all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator" と指定すると、すべてのコンポーネントで既定のトレース レベルが使用されます。<br /><br /> 各セマンティック クエリに対して生成される Transact-SQL ステートメントを表示する場合は、"SemanticQueryEngine:4" を設定できます。 Transact-SQL ステートメントは、トレース ログに記録されます。 次の例では、Transact-SQL ステートメントをログに追加する構成設定を示しています。<br /><br /> \<add name="Components" value="all,SemanticQueryEngine:4" />|  
  
##  <a name="bkmk_add_custom"></a> ダンプ ファイルの場所を指定するカスタム構成設定の追加  
 カスタム設定を追加して、Windows ワトソン博士ツールでダンプ ファイルを格納する際に使用する場所を設定できます。 カスタム設定は `Directory` です。 次の例では、この構成設定を `RStrace` セクションに指定する方法を示しています。  
  
```  
<add name="Directory" value="U:\logs\" />  
```  
  
 詳細については、 [Web サイトの](https://support.microsoft.com/?kbid=913046) サポート技術情報の記事 913046 [!INCLUDE[msCoName](../../includes/msconame-md.md)] を参照してください。  
  
##  <a name="bkmk_log_file_fields"></a> ログ ファイル フィールド  
 トレース ログでは、次のフィールドを確認できます。  
  
-   オペレーティング システム、バージョン、プロセッサ数、およびメモリなどのシステム情報  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のコンポーネント情報およびバージョン情報  
  
-   アプリケーション ログに記録されたイベント  
  
-   レポート サーバーによって生成された例外  
  
-   レポート サーバーによって記録されたリソースへの低レベルの警告  
  
-   受信 SOAP エンベロープおよび要約された送信 SOAP エンベロープ  
  
-   HTTP ヘッダー、スタック トレース、およびデバッグ トレースの情報  
  
 トレース ログの情報を確認して、レポートが配信されたかどうか、レポートの受信者、および配信の試行回数を判断できます。 また、トレース ログには、レポートの処理中に有効なレポート実行操作および環境変数も記録されます。 トレース ログには、エラーおよび例外も記録されます。 たとえば、レポートのタイムアウト エラーが見つかる場合があります (`ThreadAbortExceptions` エントリとして表示されます)。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services のログ ファイルとソース](../report-server/reporting-services-log-files-and-sources.md)   
 [エラーとイベントのリファレンス (Reporting Services)](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
