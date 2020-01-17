---
title: レポート サーバー実行ログと ExecutionLog3 ビュー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- logs [Reporting Services], execution
- execution logs [Reporting Services]
ms.assetid: a7ead67d-1404-4e67-97e7-4c7b0d942070
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 649795e5e142563b64014f2ccf970f0df5de134b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103471"
---
# <a name="report-server-execution-log-and-the-executionlog3-view"></a>レポート サーバー実行ログと ExecutionLog3 ビュー
  レポート サーバー実行ログには、サーバー上で実行するレポート、またはネイティブ モードのスケールアウト配置や SharePoint ファーム内の複数のサーバー上で実行するレポートに関する情報が含まれます。 レポート実行ログを使用して、レポートを要求する頻度、最も多く使用される出力形式、および各処理フェーズでかかる処理時間 (単位はミリ秒) を調査できます。 このログには、レポートのデータセット クエリの実行にかかった時間とデータの処理にかかった時間に関する情報が記録されます。 レポート サーバー管理者は、ログの情報を確認して実行時間が長いタスクを特定し、レポート作成者に対して改善の余地があるレポートの領域 (データセットや処理) について提案することができます。  
  
 SharePoint モード用に構成されたレポート サーバーでは、SharePoint ULS ログも利用できます。 詳細については、「 [SharePoint トレース ログの Reporting Services イベントをオンにする (ULS)](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)  
  
##  <a name="bkmk_top"></a> ログ情報の表示  
 レポート サーバーは、レポート実行に関するデータのログを内部データベース テーブルに記録します。 このテーブルの情報は SQL Server ビューで参照できます。  
  
 レポート サーバー実行ログはレポート サーバー データベースに格納されます。このデータベースの既定の名前は **ReportServer**です。 実行ログの情報は、SQL ビューに表示されます。 より新しいリリースで追加された "2" および "3" のビューには、新しいフィールドが追加されています。また、以前のリリースよりもわかりやすい名前に変更されたフィールドもあります。 古いビューも引き続き利用できるため、それらに依存するカスタム アプリケーションへの影響はありません。 ExecutionLog などの古いビューに依存していない場合は、最新のビューである ExecutionLog**3**を使用することをお勧めします。  
  
 このトピックの内容  
  
-   [SharePoint モードのレポート サーバーの構成設定](#bkmk_sharepoint)  
  
-   [ネイティブ モードのレポート サーバーの構成設定](#bkmk_native)  
  
-   [ログのフィールド (ExecutionLog3)](#bkmk_executionlog3)  
  
-   [AdditionalInfo フィールド](#bkmk_additionalinfo)  
  
-   [ログのフィールド (ExecutionLog2)](#bkmk_executionlog2)  
  
-   [ログのフィールド (ExecutionLog)](#bkmk_executionlog)  
  
##  <a name="bkmk_sharepoint"></a> SharePoint モードのレポート サーバーの構成設定  
 レポート実行のログ記録の有効と無効の切り替えは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションのシステム設定で行うことができます。  
  
 既定では、ログ エントリが 60 日間保持されます。 この期間を超えるエントリは、毎日午前 2 時に 削除されます。 長期間使用しているインストールでは、使用可能な情報は常に 60 日分のみになります。  
  
 記録される行数またはエントリの種類に制限を設定することはできません。  
  
 **実行のログ記録を有効にするには**  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  構成する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの名前をクリックします。  
  
3.  **[システム設定]** をクリックします。  
  
4.  **[ログ記録]** セクションで **[実行のログ記録を有効にする]** を選択します。  
  
5.  **[OK]** をクリックします。  
  
 **詳細ログを有効にするには**  
  
 前の手順の説明に従ってログ記録を有効にしてから、次の手順を実行する必要があります。  
  
1.  **サービス アプリケーションの** [システム設定] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ページで、 **[ユーザー定義]** セクションを探します。  
  
2.  **ExecutionLogLevel** を **verbose**に変更します。 このフィールドはテキスト入力フィールドで、有効な値は **verbose** と **normal**の 2 つです。  
  
##  <a name="bkmk_native"></a> ネイティブ モードのレポート サーバーの構成設定  
 レポート実行のログ記録の有効と無効の切り替えは、SQL Server Management Studio の [サーバーのプロパティ] ページで行うことができます。 詳細プロパティの **EnableExecutionLogging** を使用します。  
  
 既定では、ログ エントリが 60 日間保持されます。 この期間を超えるエントリは、毎日午前 2 時に 削除されます。 長期間使用しているインストールでは、使用可能な情報は常に 60 日分のみになります。  
  
 記録される行数またはエントリの種類に制限を設定することはできません。  
  
 **実行のログ記録を有効にするには**  
  
1.  SQL Server Management Studio を管理者特権で起動します。 たとえば、Management Studio のアイコンを右クリックし、[管理者として実行] をクリックします。  
  
2.  目的のレポート サーバーに接続します。  
  
3.  サーバー名を右クリックし、 **[プロパティ]** をクリックします。 [プロパティ] オプションが無効になっている場合は、SQL Server Management Studio を管理者特権で実行したことを確認してください。  
  
4.  **[ログ記録]** ページをクリックします。  
  
5.  **[レポート実行のログ記録を有効にする]** を選択します。  
  
 **詳細ログを有効にするには**  
  
 前の手順の説明に従ってログ記録を有効にしてから、次の手順を実行する必要があります。  
  
1.  **[サーバーのプロパティ]** ダイアログ ボックスで、 **[詳細設定]** ページをクリックします。  
  
2.  **[ユーザー定義]** セクションで、 **ExecutionLogLevel** を **verbose**に変更します。 このフィールドはテキスト入力フィールドで、有効な値は **verbose** と **normal**の 2 つです。  
  
##  <a name="bkmk_executionlog3"></a> ログのフィールド (ExecutionLog3)  
 このビューの XML ベースの **AdditionalInfo** 列内に追加のパフォーマンス診断ノードが追加されました。 AdditionalInfo 列には、他の 1 つ以上の情報のフィールドから成る XML 構造が格納されています。 ExecutionLog3 ビューから行を取得する Transact-SQL ステートメントの例を次に示します。 この例では、レポート サーバー データベースの名前が **ReportServer**であることを前提にしています。  
  
```  
Use ReportServer  
select * from ExecutionLog3 order by TimeStart DESC  
```  
  
 次の表に、レポート実行ログに取得されるデータを示します。  
  
|[列]|説明|  
|------------|-----------------|  
|InstanceName|要求を処理したレポート サーバー インスタンスの名前。 レポート サーバーが複数ある環境では、InstanceName のディストリビューションを分析することで、ネットワーク負荷分散を監視し、要求がレポート サーバー間で想定どおりに分散されているかどうかを確認することができます。|  
|ItemPath|レポートまたはレポート アイテムの格納場所のパス。|  
|UserName|ユーザー識別子。|  
|[ExecutionID]|要求に関連付けられた内部識別子。 同じユーザー セッションの要求は、同じ実行 ID を共有します。|  
|RequestType|有効値は次のとおりです。<br />**対話型**<br />**サブスクリプション**<br /><br /> <br /><br /> RequestType=Subscription でフィルター処理したログ データを TimeStart で並べ替えて分析すると、サブスクリプションが集中している時間が見つかることがあります。この情報を基に、レポートのサブスクリプションの一部を別の時間に変更することができます。|  
|形式|表示形式。|  
|Parameters|レポート実行に使用するパラメーター値。|  
|ItemAction|有効値は次のとおりです。<br /><br /> **Render**<br /><br /> **Sort**<br /><br /> **BookMarkNavigation**<br /><br /> **DocumentNavigation**<br /><br /> **GetDocumentMap**<br /><br /> **Findstring**<br /><br /> **実行**<br /><br /> **RenderEdit**|  
|TimeStart|レポート処理の期間を示す開始時刻と終了時刻。|  
|TimeEnd||  
|TimeDataRetrieval|データの取得にかかった時間 (単位はミリ秒)。|  
|TimeProcessing|レポートの処理にかかった時間 (単位はミリ秒)。|  
|TimeRendering|レポートの表示にかかった時間 (単位はミリ秒)。|  
|ソース|レポート実行のソース。 有効値は次のとおりです。<br /><br /> **Live**<br /><br /> **キャッシュ**:たとえば、データセットのクエリでライブ実行されませんが、キャッシュされた実行を示します。<br /><br /> **スナップショット**<br /><br /> **履歴**<br /><br /> **アドホック**:レポートのドリルスルーに基づくモデル動的に生成されたレポートまたはレポート サーバーの処理とレンダリングを使用するクライアントでプレビューされているレポート ビルダーのレポートのいずれかを示します。<br /><br /> **セッション**:既に確立されたセッション内のフォロー アップ要求を示します。  たとえば、最初の要求がページ 1 の表示であり、フォローアップ要求は現在のセッション状態での Excel へのエクスポートである場合などが考えられます。<br /><br /> **Rdce**:レポート定義カスタマイズ拡張機能を示します。 RDCE カスタム拡張機能では、レポート実行時にレポート定義を処理エンジンに渡す前に動的にカスタマイズできます。|  
|状態|状態 (rsSuccess またはエラー コード。複数のエラーが発生する場合は、最初のエラーのみ記録)。|  
|ByteCount|表示されるレポートのサイズ (バイト単位)。|  
|RowCount|クエリから返される行数。|  
|AdditionalInfo|実行に関する追加情報を格納する XML プロパティ バッグ。 内容は行ごとに異なります。|  
  
##  <a name="bkmk_additionalinfo"></a> AdditionalInfo フィールド  
 AdditionalInfo フィールドは、実行に関する追加情報を格納する XML プロパティ バッグ (構造) です。 内容はログの行ごとに異なります。  
  
 次の表は、標準と詳細の両方のログの AddtionalInfo フィールドの内容の例です。  
  
 **AddtionalInfo の標準ログの例**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>147</ConnectionOpenTime>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>642</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>63</ExecuteReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>157</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>60</ExecuteReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 **AdditionalInfo の詳細ログの例**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>127</ConnectionOpenTime>  
      <DataSource>  
        <Name>DataSource1</Name>  
        <DataExtension>SQL</DataExtension>  
      </DataSource>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>33</ExecuteReaderTime>  
          <DataReaderMappingTime>30</DataReaderMappingTime>  
          <DisposeDataReaderTime>1</DisposeDataReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>1</ExecuteReaderTime>  
          <DataReaderMappingTime>0</DataReaderMappingTime>  
          <DisposeDataReaderTime>0</DisposeDataReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 AdditionalInfo フィールドに表示されるプロパティの一部を次に示します。  
  
-   **ProcessingEngine**:1 = SQL Server 2005、2 = 新しいオンデマンド処理エンジン。 ほとんどのレポートでこの値が 1 になっている場合は、レポートを設計し直す方法を調べて、効率が向上した新しいオンデマンド処理エンジンを使用することをお勧めします。  
  
     `<ProcessingEngine>2</ProcessingEngine>`  
  
-   **ScalabilityTime**:処理エンジンでスケール関連の操作の実行にかかった時間 (単位はミリ秒)。 値が 0 の場合は、スケール操作に特に時間はかからず、要求時にメモリ不足にならなかったことを示します。  
  
    ```  
    <ScalabilityTime>  
        <Processing>0</Processing>  
    </ScalabilityTime>  
    ```  
  
-   **EstimatedMemoryUsageKB**:特定の要求について各コンポーネントで消費される最大メモリ量の推定値 (単位は KB)。  
  
    ```  
    <EstimatedMemoryUsageKB>  
        <Processing>38</Processing>  
    </EstimatedMemoryUsageKB>  
    ```  
  
-   **DataExtension**:レポートで使用されているデータ拡張機能またはデータ ソースの種類。 数値は、そのデータ ソースが使用されている回数を示します。  
  
    ```  
    <DataExtension>  
       <DAX>2</DAX>  
    </DataExtension>  
    ```  
  
-   **ExternalImages**値 (ミリ秒) です。 このデータはパフォーマンスに関する問題の診断に使用できます。 外部 Web サーバーからイメージを取得するのに時間がかかり、レポートの実行全体が遅くなる場合があります。 追加される[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]します。  
  
    ```  
    <ExternalImages>  
        <Count>3</Count>  
        <ByteCount>9268</ByteCount>  
        <ResourceFetchTime>9</ResourceFetchTime>  
    </ExternalImages>  
    ```  
  
-   **接続**:複数のレベルから成る構造体。 追加される[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]します。  
  
    ```  
    <Connections>  
        <Connection>  
          <ConnectionOpenTime>127</ConnectionOpenTime>  
          <DataSource>  
            <Name>DataSource1</Name>  
            <DataExtension>SQL</DataExtension>  
          </DataSource>  
          <DataSets>  
            <DataSet>  
              <Name>DataSet1</Name>  
              <RowsRead>16</RowsRead>  
              <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>33</ExecuteReaderTime>  
              <DataReaderMappingTime>30</DataReaderMappingTime>  
              <DisposeDataReaderTime>1</DisposeDataReaderTime>  
            </DataSet>  
            <DataSet>  
              <Name>DataSet2</Name>  
              <RowsRead>3</RowsRead>  
              <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>1</ExecuteReaderTime>  
              <DataReaderMappingTime>0</DataReaderMappingTime>  
              <DisposeDataReaderTime>0</DisposeDataReaderTime>  
            </DataSet>  
          </DataSets>  
        </Connection>  
    </Connections>  
  
    ```  
  
##  <a name="bkmk_executionlog2"></a> ログのフィールド (ExecutionLog2)  
 このビューにはフィールドがいくつか追加されたほか、一部のフィールドの名前が変更されています。 ExecutionLog2 ビューから行を取得する Transact-SQL ステートメントの例を次に示します。 この例では、レポート サーバー データベースの名前が **ReportServer**であることを前提にしています。  
  
```  
Use ReportServer  
select * from ExecutionLog2 order by TimeStart DESC  
```  
  
 次の表に、レポート実行ログに取得されるデータを示します。  
  
|[列]|説明|  
|------------|-----------------|  
|InstanceName|要求を処理したレポート サーバー インスタンスの名前。|  
|ReportPath|レポートのパス構造。  たとえば、"test" というレポートがレポート マネージャーのルート フォルダーにある場合、ReportPath は "/test" となります。<br /><br /> "test" という名前のレポートがレポート マネージャー "samples" フォルダーに保存されている場合は、ReportPath は "/Samples/test/" となります。|  
|UserName|ユーザー識別子。|  
|[ExecutionID]||  
|RequestType|要求の種類 (ユーザーまたはシステム)。|  
|形式|表示形式。|  
|Parameters|レポート実行に使用するパラメーター値。|  
|ReportAction|有効値は次のとおりです。Render, Sort, BookMarkNavigation, DocumentNavigation, GetDocumentMap, Findstring|  
|TimeStart|レポート処理の期間を示す開始時刻と終了時刻。|  
|TimeEnd||  
|TimeDataRetrieval|データの取得、レポートの処理、レポートの表示にかかった時間 (単位はミリ秒)。|  
|TimeProcessing||  
|TimeRendering||  
|ソース|レポート実行のソース (1 = 実行中、2 = キャッシュ、3 = スナップショット、4 = 履歴)。|  
|Status|状態 (rsSuccess またはエラー コード。複数のエラーが発生する場合は、最初のエラーのみ記録)。|  
|ByteCount|表示されるレポートのサイズ (バイト単位)。|  
|RowCount|クエリから返される行数。|  
|AdditionalInfo|実行に関する追加情報を格納する XML プロパティ バッグ。|  
  
##  <a name="bkmk_executionlog"></a> ログのフィールド (ExecutionLog)  
 ExecutionLog ビューから行を取得する Transact-SQL ステートメントの例を次に示します。 この例では、レポート サーバー データベースの名前が **ReportServer**であることを前提にしています。  
  
```  
Use ReportServer  
select * from ExecutionLog order by TimeStart DESC  
  
```  
  
 次の表に、レポート実行ログに取得されるデータを示します。  
  
|[列]|説明|  
|------------|-----------------|  
|InstanceName|要求を処理したレポート サーバー インスタンスの名前。|  
|ReportID|レポート識別子。|  
|UserName|ユーザー識別子。|  
|RequestType|有効値は次のとおりです。<br /><br /> True = サブスクリプション要求<br /><br /> False = 対話型の要求|  
|形式|表示形式。|  
|Parameters|レポート実行に使用するパラメーター値。|  
|TimeStart|レポート処理の期間を示す開始時刻と終了時刻。|  
|TimeEnd||  
|TimeDataRetrieval|データの取得、レポートの処理、レポートの表示にかかった時間 (単位はミリ秒)。|  
|TimeProcessing||  
|TimeRendering||  
|Source|レポート実行のソース。 有効値は次のとおりです。(1 = 実行中、2 = キャッシュ、3 = スナップショット、4 = 履歴、5 = アドホック、6 = セッション、7 = RDCE)。|  
|状態|有効値: rsSuccess、rsProcessingAborted、またはエラー コード。 複数のエラーが発生した場合は、最初のエラーだけが記録されます。|  
|ByteCount|表示されるレポートのサイズ (バイト単位)。|  
|RowCount|クエリから返される行数。|  
  
## <a name="see-also"></a>参照  
 [SharePoint トレース ログの Reporting Services イベントをオンにする (ULS)](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)   
 [Reporting Services のログ ファイルとソース](../report-server/reporting-services-log-files-and-sources.md)   
 [エラーとイベントのリファレンス (Reporting Services)](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
