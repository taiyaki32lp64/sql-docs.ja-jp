---
title: ディメンション処理変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dimensionprocessingdest.f1
- sql13.dts.designer.dimprocessingtransformation.connection.f1
- sql13.dts.designer.dimprocessingtransformation.mappings.f1
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ef381f9ff470422ed85b81832b1078d6c8767dcf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292883"
---
# <a name="dimension-processing-destination"></a>ディメンション処理変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ディメンション処理変換先は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のディメンションを読み込んで処理します。 ディメンションの詳細については、「[ディメンション (Analysis Services - 多次元データ)](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data)」を参照してください。  
  
 ディメンション処理変換先には、次の機能が含まれます。  
  
-   増分処理、完全処理、または更新処理を実行するオプション。  
  
-   エラー構成。ディメンション処理がエラーを無視するか、または指定した数のエラー発生後に停止するかどうかを指定します。  
  
-   ディメンション テーブルの列への入力列のマッピング  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの処理に関する詳細については、「[処理オプションと設定 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)」を参照してください。  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>ディメンション処理変換先の構成  
 ディメンション処理変換先は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを接続して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト、または、変換先が処理するディメンションを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスに接続します。 詳しくは、「 [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)」をご覧ください。  
  
 この変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="dimension-processing-destination-editor-connection-manager-page"></a>[ディメンション処理変換先エディター] ([接続マネージャー] ページ)
  **[ディメンション処理変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスへの接続を指定できます。  
  
### <a name="options"></a>オプション  
 **Connection manager**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[Analysis Services 接続マネージャーの追加]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **利用可能なディメンションの一覧**  
 処理するディメンションを選択します。  
  
 **[処理方法]**  
 一覧で選択したディメンションに適用する処理方法を選択します。 このオプションの既定値は **[完全]** です。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[追加 (増分)]**|ディメンションの増分処理を実行します。|  
|**[完全]**|ディメンションの完全処理を実行します。|  
|**Update**|ディメンションの更新処理を実行します。|  
  
## <a name="dimension-processing-destination-editor-mappings-page"></a>[ディメンション処理変換先エディター] ([マッピング] ページ)
  **[ディメンション処理変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる入力列を変換先列にマップします。  
  
 **使用できる変換先列**  
 使用できる変換先列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる変換先列を入力列にマップします。  
  
 **入力列**  
 上の表で選択された入力列が表示されます。 **[使用できる入力列]** ボックスの一覧を使用して、マッピングを変更できます。  
  
 **変換先列**  
 使用できる変換先列を表示し、それぞれがマップされるかどうかを示します。  
  
## <a name="dimension-processing-destination-editor-advanced-page"></a>[ディメンション処理変換先エディター] ([詳細設定] ページ)
  **[ディメンション処理変換先エディター]** ダイアログ ボックスの **[詳細設定]** ページを使用すると、エラー処理を構成できます。  
  
### <a name="options"></a>オプション  
 **[既定のエラー構成を使用する]**  
 既定の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] エラー処理を使用するかどうかを指定します。 既定では、この値は **True**です。  
  
 **[キー エラー アクション]**  
 許容されないキー値を持つレコードを処理する方法を指定します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**ConvertToUnknown**|不正なキー値を **UnknownMember** に変換します。|  
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
 NULL キーが **UnknownMember** 値に変換された場合に実行する操作を指定します。 既定では、この値は **IgnoreError**です。  
  
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
 エラー ログのパスを入力するか、 **[...]** ボタンをクリックしてログの保存先を選択します。  
  
 **[...]**  
 エラー ログのパスを選択します。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
