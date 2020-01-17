---
title: エラー処理 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e0924c4ac6d2ddd4e14b35794b9c03ac7fb2e136
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835652"
---
# <a name="error-handling"></a>エラー処理
  Oracle CDC インスタンスでは、単一の Oracle ソース データベース (Oracle RAC クラスターは単一のデータベースと見なされます) から変更を検出し、対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに含まれる CDC データベースの変更テーブルにコミット済みの変更を書き込みます。  
  
 CDC インスタンスでは、 **cdc.xdbcdc_state**というシステム テーブルで状態を管理します。 このテーブルをクエリすると、CDC インスタンスの状態をいつでも確認することができます。 cdc.xdbcdc_state テーブルの詳細については、「 [cdc.xdbcdc_state](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_state)」をご覧ください。  
  
 次の表は、xdbcdc_state テーブルで示される CDC インスタンスの状態について説明したものです。  
  
 各状態について、cdc.xdbcdc_state テーブル内の対応する列で次の 2 つのことが示されます。  
  
-   インスタンスがアクティブでない (Windows プロセスで現在処理されていない) ことを示します。 **[active]** 列の値が 1 の場合は、この Oracle CDC インスタンスを処理する Oracle CDC Service のサブプロセスが実行されています。  
  
-   **[error]** 列の値が 0 の場合、Oracle CDC インスタンスがエラー状態ではないことを示します。 **[error]** 列の値が 1 の場合は、エラーが発生しており、Oracle CDC インスタンスで変更を処理できません。  
  
     **[error]** 列の値が 1 で、 **[active]** 列の値も 1 の場合は、Oracle CDC インスタンスで回復可能なエラーが発生しています。このエラーは自動的に解決できます。 [error] 列の値が 1 で、[active] 列の値が 0 の場合は、通常、処理を再開する前に手動で問題を解決する必要があります。  
  
 次の表に、Oracle CDC インスタンスの状態テーブルで報告されるさまざまな状態コードを示します。  
  
|状態|Active 状態コード|Error 状態コード|説明|  
|------------|------------------------|-----------------------|------------------|  
|ABORTED|0|1|Oracle CDC インスタンスが実行されていません。 ABORTED 副状態は、ACTIVE だった Oracle CDC インスタンスが予期せず停止したことを示します。<br /><br /> ABORTED 副状態になるのは、実行されていない Oracle CDC インスタンスの状態が ACTIVE になっていることが Oracle CDC Service のメイン インスタンスで検出された場合です。|  
|[error]|0|1|Oracle CDC インスタンスが実行されていません。 ERROR 状態は、回復できないエラーが発生したために ACTIVE だった CDC インスタンスが無効になったことを示します。 ERROR 状態には、次の副状態コードがあります。<br /><br /> MISCONFIGURED: 回復できない構成エラーが検出されました。<br /><br /> PASSWORD-REQUIRED: Change Data Capture Designer for Oracle by Attunity のパスワードが設定されていないか、構成されているパスワードが無効です。 サービスの非対称キーのパスワードが変更されたことが原因として考えられます。|  
|RUNNING|1|0|CDC インスタンスが実行されていて、変更レコードが処理されています。 RUNNING 状態には、次の副状態コードがあります。<br /><br /> IDLE: すべての変更レコードが処理され、対象の制御 ( **_CT**) テーブルに格納されました。 制御テーブルにアクティブなトランザクションはありません。<br /><br /> PROCESSING: 制御 ( **_CT**) テーブルにまだ書き込まれていない、処理中の変更レコードがあります。|  
|STOPPED|0|0|CDC インスタンスが実行されていません。 STOP 副状態は、ACTIVE だった CDC インスタンスが適切に停止されたことを示します。|  
|SUSPENDED|1|1|CDC インスタンスが実行されていますが、回復可能なエラーにより処理が中断されています。 SUSPENDED 状態には、次の副状態コードがあります。<br /><br /> DISCONNECTED: ソース Oracle データベースとの接続を確立できません。 接続が回復すると処理が再開されます。<br /><br /> STORAGE: 記憶領域がいっぱいです。 記憶領域に空きができると処理が再開されます。 この状態は、状態テーブルを更新できないために表示されない場合があります。<br /><br /> LOGGER: ロガーは Oracle に接続されていますが、一時的な問題が発生しており、Oracle トランザクション ログを読み取ることができません。|  
|DATAERROR|○|○|この状態コードは、 **xdbcdc_trace** テーブルにのみ使用されます。 **xdbcdc_state** テーブルには表示されません。 この状態のトレース レコードは、Oracle のログ レコードに問題があることを示します。 問題があるログ レコードは、 **[data]** 列に BLOB として格納されます。 DATAERROR 状態には、次の副状態コードがあります。<br /><br /> BADRECORD: アタッチされたログ レコードを解析できませんでした。<br /><br /> CONVERT-ERROR: 一部の列のデータをキャプチャ テーブル内の対象の列に変換できませんでした。 この状態は、変換エラーについてのトレース レコードを生成するように構成で指定されている場合にのみ表示されます。|  
  
 Oracle CDC Service の状態は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されるため、データベース内の状態の値にサービスの実際の状態が反映されていない場合もあります。 最も一般的なシナリオは、サービスと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の間の接続が失われ、なんらかの理由で再開できない場合です。 この場合、 **cdc.xdbcdc_state** に最新の状態が格納されなくなります。 最終更新のタイムスタンプ (UTC) から 1 分以上経過していれば、古い状態を示していると考えられます。 この場合は、Windows イベント ビューアーを使用して、サービスの状態に関する詳しい情報を確認してください。  
  
## <a name="error-handling"></a>エラー処理  
 ここでは、Oracle CDC Service でのエラーの処理方法について説明します。  
  
### <a name="logging"></a>ログの記録  
 Oracle CDC Service では、次のいずれかにエラー情報を出力します。  
  
-   Windows イベント ログ。エラーのログ記録で、Oracle CDC Service のライフ サイクル イベント (開始、停止、対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続や再接続) を示すために使用されます。  
  
-   MSXDBCDC.dbo.xdbcdc_trace テーブル。Oracle CDC Service のメイン プロセスで、一般的なログ記録とトレースに使用されます。  
  
-   \<cdc-database>.cdc.xdbcdc_trace テーブル。Oracle CDC インスタンスで、一般的なログ記録とトレースに使用されます。 つまり、特定の Oracle CDC インスタンスに関連するエラーは、そのインスタンスのトレース テーブルに記録されます。  
  
 Oracle CDC Service で情報が記録される状況は次のとおりです。  
  
-   サービス コントロール マネージャーによって開始または停止された。  
  
-   関連付けられている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続できない (エラーの発生後に接続が正常に確立された場合も含む)。  
  
-   Oracle CDC Service インスタンスの起動時にエラーが発生した。  
  
-   Oracle CDC インスタンスが中止されたことが検出された。  
  
-   予期しないエラーが発生した。  
  
 CDC インスタンスで情報が記録される状況は次のとおりです。  
  
-   有効または無効になった。  
  
-   エラーが発生した。  
  
-   回復可能なエラーから回復した。  
  
 さらに、トレース テーブルを使用して、トラブルシューティングのための詳細なトレース情報が記録されます。  
  
### <a name="handling-source-oracle-connection-errors"></a>ソース Oracle との接続エラーの処理  
 Oracle CDC Service では、ソース Oracle データベースとの固定接続が必要です。 サービスの構成とは関係がない接続エラー (ネットワーク エラーなど) の多くは、一時的なエラーと見なされます。 したがって、Oracle CDC Service と Oracle データベースの間の接続を確立できない場合 (起動時か作業中に切断された後)、サービスの状態は SUSPENDED/DISCONNECTED になり、定期的に接続が再試行されます。 この場合、接続が再確立されると処理が続行されます。  
  
 それ以外に、一時的なエラーでない接続エラーもあります (たとえば、資格情報が正しくない、必要な特権がない、データベースのアドレスが正しくないなど)。 それらのエラーが発生した場合は、Oracle CDC Service の状態は ERROR/MISCONFIGURED または ERROR/PASSWORD-REQUIRED になり、サービスが無効になります。 この場合、処理を再開するには、基になるエラーを解決してから、CDC Oracle インスタンスを手動で再び有効にする必要があります。  
  
 一時的なエラーかどうかが明確でない場合は、一時的なエラーと想定して対処することをお勧めします。  
  
### <a name="handling-target-sql-server-connection-errors"></a>対象の SQL Server との接続エラーの処理  
 Oracle CDC Service では、対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの固定接続が必要です。 この接続は次の目的に使用されます。  
  
-   この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを実行する同じ名前のサービスがほかにないことを確認する。  
  
-   有効または無効にする Oracle CDC インスタンスを確認し、そのサブプロセスを開始 (または停止) する。  
  
 対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとの接続を確立し、この名前で実行されている Oracle CDC Service がこのサービスだけであることを確認したら、有効にする Oracle CDC インスタンスを確認し、それらによるプロセスの処理を開始することができます (その後、無効になったらそれらのプロセスを停止します)。 Oracle CDC インスタンスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続を使用して、CDC Oracle インスタンスの CDC データベースと連携します。  
  
 対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続できなかった場合のエラーの処理方法は、そのエラーが一時的なエラーであるかどうかによって異なります。  
  
 一時的でない既知のエラー (資格情報が正しくない、必要な特権がない、接続情報が正しくないなど) の場合は、Windows イベント ログにエラーが記録され、サービスが停止します ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続できないため、トレース テーブルには書き込まれません)。 この場合は、エラーを解決し、Oracle CDC Windows サービスを再起動する必要があります。  
  
 一時的なエラーや予期しないエラーの場合は、操作が繰り返し再試行され、相当な時間が経過してもエラーが解決しないと、CDC Service の CDC インスタンスのサブプロセスが停止されて、最初の接続試行に戻ります (この時点で、指定された CDC サービスの制御が既に別のコンピューターの Oracle CDC Service に移っている場合もあります)。  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>対象の SQL Server の記憶領域に空きがない場合のエラーの処理  
 Oracle CDC Service では、新しい変更データを対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC データベースに挿入できないことを検出した場合、イベント ログに警告を書き込み、トレース レコードの挿入を試行します (この操作も同じ理由で失敗する可能性があります)。 処理が成功するまで、この操作が一定の間隔で再試行されます。  
  
### <a name="handling-oracle-cdc-errors"></a>Oracle CDC のエラーの処理  
 Oracle CDC インスタンスでは、Oracle トランザクション ログを読み取って処理します。 CDC の処理でエラーが発生すると、 **cdc.xdbcdc_state** テーブルで報告されます。ユーザーは、報告されたエラーに基づいて手動で対処する必要があります。  
  
 たとえば、Oracle CDC インスタンスがアクティブにならない時間がしばらく続き、必要な Oracle トランザクション ログ ファイルを使用できなくなったとします。 この場合、Oracle CDC インスタンスで処理を再開するには、必要なログを Oracle DBA で復元する必要があります。  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>Oracle CDC インスタンスの予期しないエラーの処理  
 Oracle CDC Service では、CDC インスタンスのサブプロセスを監視しています。 CDC インスタンスのサブプロセスが中止されると、MSXDBCDC.dbo.xdbcdc_databases テーブルでそのサブプロセスが無効になり、cdc.xdbcdc_state の状態が ABORTED に更新されます。 この場合、詳細な分析のために、標準の Windows エラー報告ダイアログ ボックスでこのエラーが報告されます。  
  
## <a name="see-also"></a>参照  
 [Attunity の Change Data Capture Designer for Oracle](change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC インスタンス](the-oracle-cdc-instance.md)  
