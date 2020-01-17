---
title: パーティション処理変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.partitionprocessingdest.f1
- sql13.dts.designer.partprocessingtransformation.connection.f1
- sql13.dts.designer.partprocessingtransformation.mapping.f1
- sql13.dts.designer.partprocessingtransformation.advanced.f1
helpviewer_keywords:
- partitions [Analysis Services], processing
- Partition Processing destination [Integration Services]
- destinations [Integration Services], Partition Processing
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23292c0ac898ca035bca4b499de4bfc3fe2a7ebc
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292158"
---
# <a name="partition-processing-destination"></a>パーティション処理変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  パーティション処理変換先は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のパーティションを読み込んで処理します。 パーティションの詳細については、「[パーティション (Analysis Services - 多次元データ)](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data)」を参照してください。  
  
 パーティション処理変換先には、次の機能が含まれます。  
  
-   増分処理、完全処理、または更新処理を実行するオプション。  
  
-   エラー構成。処理中のエラーを無視するか、またはエラーが指定した回数に達した場合、処理を停止するかを指定します。  
  
-   パーティション分割列への入力列のマッピング。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの処理に関する詳細については、「[処理オプションと設定 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)」を参照してください。  
  
> [!NOTE]  
>  ここで説明されているタスクは、Analysis Services テーブル モデルには適用されません。  テーブル モデルで入力列をパーティション列にマップすることはできません。 代わりに Analysis Services DDL 実行タスク [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) を使用してパーティションを処理することができます。  
  
## <a name="configuration-of-the-partition-processing-destination"></a>パーティション処理変換先の構成  
 パーティション処理変換先は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを接続して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト、または変換先が処理するキューブとパーティションを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスに接続します。 詳細については、「 [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)」を参照してください。  
  
 この変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [パーティション処理変換先のカスタム プロパティ](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="partition-processing-destination-editor-connection-manager-page"></a>[パーティション処理変換先エディター] ([接続マネージャー] ページ)
  **[パーティション処理変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスへの接続を指定できます。  
  
> [!NOTE]  
>  ここで説明されているタスクは、Analysis Services テーブル モデルには適用されません。  テーブル モデルで入力列をパーティション列にマップすることはできません。 代わりに Analysis Services DDL 実行タスク [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) を使用してパーティションを処理することができます。  
  
### <a name="options"></a>オプション  
 **Connection manager**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[Analysis Services 接続マネージャーの追加]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **利用可能なパーティションの一覧**  
 処理するパーティションを選択します。  
  
 **[処理方法]**  
 処理方法を選択します。 このオプションの既定値は **[完全]** です。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|[追加 (増分)]|パーティションの増分処理を実行します。|  
|[完全]|パーティションの完全処理を実行します。|  
|[データのみ]|パーティションの更新処理を実行します。|  
  
## <a name="partition-processing-destination-editor-mappings-page"></a>[パーティション処理変換先エディター] ([マッピング] ページ)
  **[パーティション処理変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列をパーティション列にマップできます。  
  
> [!NOTE]  
>  ここで説明されているタスクは、Analysis Services テーブル モデルには適用されません。  テーブル モデルで入力列をパーティション列にマップすることはできません。 代わりに Analysis Services DDL 実行タスク [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) を使用してパーティションを処理することができます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる入力列を変換先列にマップします。  
  
 **使用できる変換先列**  
 使用できる変換先列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる変換先列を入力列にマップします。  
  
 **入力列**  
 上の表で選択された入力列が表示されます。 **[使用できる入力列]** ボックスの一覧を使用して、マッピングを変更できます。  
  
 **変換先列**  
 マップされているかどうかに関係なく、使用できる変換先列を表示します。  
  
## <a name="partition-processing-destination-editor-advanced-page"></a>[パーティション処理変換先エディター] ([詳細設定] ページ)
  **[パーティション処理変換先エディター]** ダイアログ ボックスの **[詳細設定]** ページを使用すると、エラー処理を設定できます。  
  
> [!NOTE]  
>  ここで説明されているタスクは、Analysis Services テーブル モデルには適用されません。  テーブル モデルで入力列をパーティション列にマップすることはできません。 代わりに Analysis Services DDL 実行タスク [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) を使用してパーティションを処理することができます。  
  
### <a name="options"></a>オプション  
 **[既定のエラー構成を使用する]**  
 既定の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] エラー処理を使用するかどうかを指定します。 既定では、この値は **True**です。  
  
 **[キー エラー アクション]**  
 許容されないキー値を持つレコードを処理する方法を指定します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**ConvertToUnknown**|不正なキー値を不明な値に変換します。|  
|**DiscardRecord**|レコードを破棄します。|  
  
 **[エラーを無視する]**  
 エラーを無視することを指定します。  
  
 **[エラー時に停止する]**  
 エラーが発生した場合に処理を停止することを指定します。  
  
 **[エラー数]**  
 **[エラー時に停止する]** を選択した場合は、処理を停止するエラーのしきい値を指定します。  
  
 **[エラー時のアクション]**  
 **[エラー時に停止する]** を選択した場合は、エラーのしきい値に達した場合に実行する操作を指定します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**StopProcessing**|処理を停止します。|  
|**StopLogging**|ログ記録エラーを停止します。|  
  
 **[見つからないキー]**  
 見つからないキーのエラーに対する操作を指定します。 既定では、この値は **[ReportAndContinue]** です。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**IgnoreError**|エラーを無視して処理を続行します。|  
|**[ReportAndContinue]**|エラーを報告して処理を続行します。|  
|**ReportAndStop**|エラーを報告して処理を停止します。|  
  
 **[重複キー]**  
 重複キーのエラーに対する操作を指定します。 既定では、この値は **IgnoreError**です。  
  
|Value|[説明]|  
|-----------|-----------------|  
|**IgnoreError**|エラーを無視して処理を続行します。|  
|**[ReportAndContinue]**|エラーを報告して処理を続行します。|  
|**ReportAndStop**|エラーを報告して処理を停止します。|  
  
 **[不明な種類に変換された NULL キー]**  
 NULL キーが不明な値に変換された場合に実行する操作を指定します。 既定では、この値は **IgnoreError**です。  
  
|Value|[説明]|  
|-----------|-----------------|  
|**IgnoreError**|エラーを無視して処理を続行します。|  
|**[ReportAndContinue]**|エラーを報告して処理を続行します。|  
|**ReportAndStop**|エラーを報告して処理を停止します。|  
  
 **[許可されていない NULL キー]**  
 NULL キーが許可されていない場合に NULL キーが検出されたときに実行する操作を指定します。 既定では、この値は **[ReportAndContinue]** です。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**IgnoreError**|エラーを無視して処理を続行します。|  
|**[ReportAndContinue]**|エラーを報告して処理を続行します。|  
|**ReportAndStop**|エラーを報告して処理を停止します。|  
  
 **[エラー ログのパス]**  
 エラー ログのパスを入力するか、 **(...)** 参照ボタンを使用してログの保存先を選択します。  
  
 **[...]**  
 エラー ログのパスを選択します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../integration-services/integration-services-error-and-message-reference.md)   
