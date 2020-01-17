---
title: データ フロー タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataflowtask.f1
helpviewer_keywords:
- data flow task [Integration Services]
- performance [Integration Services]
- data flow [Integration Services], performance
- data flow [Integration Services], Data Flow task
- Integration Services, performance
ms.assetid: c27555c4-208c-43c8-b511-a4de2a8a3344
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: eab0ef5519aea7f563104d61146ed5f441d15981
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832457"
---
# <a name="data-flow-task"></a>[データ フロー タスク]
  データ フロー タスクは、変換元と変換先との間でデータを移動するデータ フロー エンジンをカプセル化して、データの移動時にユーザーがデータを変換、クリーンアップ、および変更できるようにします。 データ フロー タスクをパッケージの制御フローに追加すると、パッケージでデータの抽出、変換、および読み込みを行うことができます。  
  
 データ フローは 1 つ以上のデータ フロー コンポーネントで構成されますが、通常は、データを抽出する変換元、データを変更、ルーティング、または集約する変換、およびデータを読み込む変換先のデータ フロー コンポーネントが連結されてセットになっています。  
  
 実行時に、データ フロー タスクはデータ フローから実行プランを作成し、データ フロー エンジンはそのプランを実行します。 データ フローを含まないデータ フロー タスクも作成できますが、データ フロー タスクは少なくとも 1 つのデータ フローを含む場合にのみ実行されます。  
  
 テキスト ファイルのデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに一括挿入するには、データ フロー タスクとデータ フローの代わりに、一括挿入タスクを使用できます。 ただし、一括挿入タスクではデータの変換はできません。 詳細については、「 [一括挿入タスク](bulk-insert-task.md)」を参照してください。  
  
## <a name="multiple-flows"></a>複数のフロー  
 データ フロー タスクには、複数のデータ フローを含めることができます。 タスクが複数のデータのセットをコピーする場合で、データのコピー順序が重要でない場合は、データ フロー タスクにデータ フローを複数含める方が便利です。 たとえば、5 つのデータ フローを作成し、各データ フローで、フラット ファイルからデータ ウェアハウスのスター スキーマ内のそれぞれ別のディメンション テーブルにデータをコピーできます。  
  
 ただし、1 つのデータ フロー タスク内に複数のデータ フローが含まれる場合、実行順序はデータ フロー エンジンによって決定されます。 したがって、順序が重要である場合、パッケージは複数のデータ フロー タスクを使用して、各タスクにつきデータ フローを 1 つずつ含める必要があります。 次に、優先順位制約を適用して、タスクの実行順序を制御できます。  
  
 次の図は、複数のデータ フローが含まれるデータ フロー タスクを示しています。  
  
 ![データ フロー](../media/mw-dts-09.gif "データ フロー")  
  
## <a name="log-entries"></a>ログ エントリ  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] では、すべてのタスクで利用可能な一連のログ イベントを提供しています。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] では、多くのタスクにカスタム ログ エントリも提供しています。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。 データ フロー タスクには、次のカスタム ログ エントリが含まれています。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`BufferSizeTuning`|データ フロー タスクでバッファーのサイズが変更されたことを示します。 このログ エントリはサイズ変更の理由を説明し、一時的な新しいバッファー サイズを表示します。|  
|`OnPipelinePostEndOfRowset`|`ProcessInput` メソッドの最終呼び出しで設定される、行セットの終了シグナルがコンポーネントに通知されたことを示します。 エントリは、データ フロー内で入力を処理するコンポーネントごとに書き込まれます。 このエントリには、コンポーネント名が含まれます。|  
|`OnPipelinePostPrimeOutput`|コンポーネントが `PrimeOutput` メソッドの最終呼び出しを完了したことを示します。 データ フローによっては、複数のログ エントリが書き込まれる場合があります。 コンポーネントがソースの場合、このログ エントリは、コンポーネントが行の処理を完了したことを意味します。|  
|`OnPipelinePreEndOfRowset`|コンポーネントがまもなくの最後の呼び出しで設定される行セットの終了シグナルを受信することを示します、`ProcessInput`メソッド。 エントリは、データ フロー内で入力を処理するコンポーネントごとに書き込まれます。 このエントリには、コンポーネント名が含まれます。|  
|`OnPipelinePrePrimeOutput`|コンポーネントに、`PrimeOutput` メソッドからの呼び出しが通知されたことを示します。 データ フローによっては、複数のログ エントリが書き込まれる場合があります。|  
|`OnPipelineRowsSent`|`ProcessInput` メソッドの呼び出しによってコンポーネント入力に指定された行数を報告します。 ログ エントリにはコンポーネント名が含まれます。|  
|`PipelineBufferLeak`|バッファー マネージャーの終了後もバッファーを保持しているコンポーネントに関する情報を提供します。 バッファーが保持されたままの場合、バッファー リソースは解放されていないので、メモリ リークが発生する可能性があります。 このログ エントリは、コンポーネントの名前とバッファーの ID を含みます。|  
|`PipelineComponentTime`|主要な 5 つの処理手順 (Validate、PreExecute、PostExecute、ProcessInput、および ProcessOutput) それぞれにおいてコンポーネントが費やした時間 (ミリ秒) を報告します。|  
|`PipelineExecutionPlan`|データ フローの実行プランを報告します。 この実行プランでは、バッファーをコンポーネントに送信する方法に関する情報を提供します。 この情報は、PipelineExecutionTrees ログ エントリと組み合わせて、データ フロー タスク内での実行内容を示します。|  
|`PipelineExecutionTrees`|データ フロー内のレイアウトの実行ツリーを報告します。 データ フロー エンジンのスケジューラは、このツリーを使用して、データ フローの実行プランを構築します。|  
|`PipelineInitialization`|タスクに関する初期化情報を提供します。 この情報には、BLOB データの一時的な保存に使用するディレクトリ、既定のバッファー サイズ、およびバッファー内の行数が含まれます。 データ フロー タスクの構成によっては、複数のログ エントリが書き込まれる場合があります。|  
  
 これらのログ エントリには、パッケージを実行するたびに、データ フロー タスクの実行に関する豊富な情報が記録されます。 パッケージを繰り返し実行するうちに情報が蓄積され、タスクが実行する処理、パフォーマンスに影響する問題、タスクが処理するデータ量などに関する重要な履歴情報が得られます。  
  
 これらのログ エントリを使用してデータ フローのパフォーマンスを監視し、向上させる方法の詳細については、次のいずれかのトピックを参照してください。  
  
-   [パフォーマンス カウンター](../performance/performance-counters.md)  
  
-   [データ フロー パフォーマンス機能](../data-flow/data-flow-performance-features.md)  
  
### <a name="sample-messages-from-a-data-flow-task"></a>データ フロー タスクからのサンプル メッセージ  
 次の表は、ごく単純なパッケージでのログ エントリのサンプル メッセージの一覧です。 このパッケージは、OLE DB ソースを使用してテーブルからデータを抽出し、並べ替え変換を使用してデータを並べ替え、さらに OLE DB 変換先を使用してデータを別のテーブルに書き込みます。  
  
|ログ エントリ|Messages|  
|---------------|--------------|  
|`BufferSizeTuning`|`Rows in buffer type 0 would cause a buffer size greater than the configured maximum. There will be only 9637 rows in buffers of this type.`<br /><br /> `Rows in buffer type 2 would cause a buffer size greater than the configured maximum. There will be only 9497 rows in buffers of this type.`<br /><br /> `Rows in buffer type 3 would cause a buffer size greater than the configured maximum. There will be only 9497 rows in buffers of this type.`|  
|`OnPipelinePostEndOfRowset`|`A component will be given the end of rowset signal. : 1180 : Sort : 1181 : Sort Input`<br /><br /> `A component will be given the end of rowset signal. : 1291 : OLE DB Destination : 1304 : OLE DB Destination Input`|  
|`OnPipelinePostPrimeOutput`|`A component has returned from its PrimeOutput call. : 1180 : Sort`<br /><br /> `A component has returned from its PrimeOutput call. : 1 : OLE DB Source`|  
|`OnPipelinePreEndOfRowset`|`A component has finished processing all of its rows. : 1180 : Sort : 1181 : Sort Input`<br /><br /> `A component has finished processing all of its rows. : 1291 : OLE DB Destination : 1304 : OLE DB Destination Input`|  
|`OnPipelinePrePrimeOutput`|`PrimeOutput will be called on a component. : 1180 : Sort`<br /><br /> `PrimeOutput will be called on a component. : 1 : OLE DB Source`|  
|`OnPipelineRowsSent`|`Rows were provided to a data flow component as input. :  : 1185 : OLE DB Source Output : 1180 : Sort : 1181 : Sort Input : 76`<br /><br /> `Rows were provided to a data flow component as input. :  : 1308 : Sort Output : 1291 : OLE DB Destination : 1304 : OLE DB Destination Input : 76`|  
|`PipelineComponentTime`|`The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`<br /><br /> `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`<br /><br /> `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`<br /><br /> `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`<br /><br /> `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`<br /><br /> `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`<br /><br /> `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`<br /><br /> `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`|  
|`PipelineExecutionPlan`|`SourceThread0`<br /><br /> `Drives: 1`<br /><br /> `Influences: 1180 1291`<br /><br /> `Output Work List`<br /><br /> `CreatePrimeBuffer of type 1 for output ID 11.`<br /><br /> `SetBufferListener: "WorkThread0" for input ID 1181`<br /><br /> `CreatePrimeBuffer of type 3 for output ID 12.`<br /><br /> `CallPrimeOutput on component "OLE DB Source" (1)`<br /><br /> `End Output Work List`<br /><br /> `End SourceThread0`<br /><br /> `WorkThread0`<br /><br /> `Drives: 1180`<br /><br /> `Influences: 1180 1291`<br /><br /> `Input Work list, input ID 1181 (1 EORs Expected)`<br /><br /> `CallProcessInput on input ID 1181 on component "Sort" (1180) for view type 2`<br /><br /> `End Input Work list for input 1181`<br /><br /> `Output Work List`<br /><br /> `CreatePrimeBuffer of type 4 for output ID 1182.`<br /><br /> `SetBufferListener: "WorkThread1" for input ID 1304`<br /><br /> `CallPrimeOutput on component "Sort" (1180)`<br /><br /> `End Output Work List`<br /><br /> `End WorkThread0`<br /><br /> `WorkThread1`<br /><br /> `Drives: 1291`<br /><br /> `Influences: 1291`<br /><br /> `Input Work list, input ID 1304 (1 EORs Expected)`<br /><br /> `CallProcessInput on input ID 1304 on component "OLE DB Destination" (1291) for view type 5`<br /><br /> `End Input Work list for input 1304`<br /><br /> `Output Work List`<br /><br /> `End Output Work List`<br /><br /> `End WorkThread1`|  
|`PipelineExecutionTrees`|`begin execution tree 0`<br /><br /> `output "OLE DB Source Output" (11)`<br /><br /> `input "Sort Input" (1181)`<br /><br /> `end execution tree 0`<br /><br /> `begin execution tree 1`<br /><br /> `output "OLE DB Source Error Output" (12)`<br /><br /> `end execution tree 1`<br /><br /> `begin execution tree 2`<br /><br /> `output "Sort Output" (1182)`<br /><br /> `input "OLE DB Destination Input" (1304)`<br /><br /> `output "OLE DB Destination Error Output" (1305)`<br /><br /> `end execution tree 2`|  
|`PipelineInitialization`|`No temporary BLOB data storage locations were provided. The buffer manager will consider the directories in the TEMP and TMP environment variables.`<br /><br /> `The default buffer size is 10485760 bytes.`<br /><br /> `Buffers will have 10000 rows by default`<br /><br /> `The data flow will not remove unused components because its RunInOptimizedMode property is set to false.`|  
  
 ログ イベントの多くは複数のエントリを書き込み、多数のログ エントリのメッセージに複雑なデータが含まれています。 メッセージ テキストを解析することで、複雑なメッセージの内容をより簡単に理解して伝えられるようになります。 ログの場所によっては、Transact-SQL ステートメントまたはスクリプト コンポーネントを使用して、複雑なテキストを列、またはより有効なその他の形式に分けることができます。  
  
 たとえば、次の表に含まれるメッセージ "行がデータ フロー コンポーネントに入力として指定されました。 :  : 1185 : OLE DB ソースの出力 : 1180 : 並べ替え : 1181 : 並べ替えの入力 : 76" は、列へと解析されています。 このメッセージは、OLE DB ソースから並べ替え変換に行が送信されるときに `OnPipelineRowsSent` イベントによって書き込まれました。  
  
|[列]|説明|値|  
|------------|-----------------|-----------|  
|**PathID**|OLE DB ソースと並べ替え変換の間のパスの `ID` プロパティの値です。|1185|  
|**PathName**|パスの `Name` プロパティの値です。|OLE DB ソースの出力|  
|**ComponentID**|値、`ID`並べ替え変換のプロパティ。|1180|  
|**ComponentName**|並べ替え変換の `Name` プロパティの値です。|並べ替え|  
|**InputID**|並べ替え変換に対する入力の `ID` プロパティの値です。|1181|  
|**InputName**|並べ替え変換に対する入力の `Name` プロパティの値です。|並べ替えの入力|  
|**RowsSent**|並べ替え変換の入力に送信された行数です。|76|  
  
## <a name="configuration-of-the-data-flow-task"></a>データ フロー タスクの構成  
 プロパティを設定するには、 **[プロパティ]** ウィンドウで行うか、またはプログラムによって設定します。  
  
 プロパティを **[プロパティ]** ウィンドウで設定する方法の詳細については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-data-flow-task"></a>プログラムによるデータ フロー タスクの構成  
 プログラムによってデータ フロー タスクをパッケージに追加して、データ フローのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   [プログラムによるデータ フロー タスクの追加](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 technet.microsoft.com のビデオ「 [Balanced Data Distributor](https://go.microsoft.com/fwlink/?LinkID=226278&clcid=0x409)」  
  
  
