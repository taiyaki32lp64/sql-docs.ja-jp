---
title: ADO NET ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ade0d29ed20bb8b39d9ac2a1762977abe24d8f65
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293515"
---
# <a name="ado-net-source"></a>ADO NET ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ADO NET ソースは .NET プロバイダーのデータを呼び出し、そのデータをデータ フローで使用できるようにします。  
  
 ADO NET 変換元を使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]に接続できます。 OLE DB を使用した [!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続はサポートされていません。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の詳細については、「[一般的な制限事項とガイドライン (Azure SQL Database)](https://go.microsoft.com/fwlink/?LinkId=248228)」を参照してください。  
  
## <a name="data-type-support"></a>データ型のサポート  
 ソースは、特定の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型にマップされないデータ型を DT_NTEXT [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型に変換します。 この変換はデータ型が **System.Object**である場合でも行われます。  
  
 DT_NTEXT データ型から DT_WSTR データ型に、または DT_WSTR データ型から DT_NTEXT データ型に変更できます。 データ型を変更するには、ADO NET ソースの **[詳細エディター]** ダイアログ ボックスで **DataType** プロパティを設定します。 詳細については、「 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)」(共通プロパティ) を参照してください。  
  
 ADO NET ソースの後にデータ変換の変換を使用することによって、DT_NTEXT データ型を DT_BYTES データ型または DT_STR データ型に変換することもできます。 詳細については、「 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、日付データ型 DT_DBDATE、DT_DBTIME2、DT_DBTIMESTAMP2、および DT_DBTIMESTAMPOFFSET は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定の日付データ型にマップされます。 ADO NET ソースを構成して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用する日付データ型を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が使用する日付データ型に変換できます。 このような日付データ型を変換する ADO NET ソースを構成するには、 **接続マネージャーの** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロパティを **[最新]** に設定します ( **Type System Version** プロパティは、 **[接続マネージャー]** ダイアログ ボックスの **[すべて]** ページにあります。 **[接続マネージャー]** ダイアログ ボックスを開くには、 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを右クリックし、 **[編集]** をクリックします)。  
  
> [!NOTE]  
>  **接続マネージャーの** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロパティが **[SQL Server 2005]** に設定されていると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日付データ型は DT_WSTR に変換されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 接続マネージャーで、プロバイダーを .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) と指定すると、システムはユーザー定義データ型 (UDT) は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バイナリ ラージ オブジェクト (BLOB) に変換されます。 UDT データ型の変換時には、次の規則が適用されます。  
  
-   データが大きくない UDT の場合、データは DT_BYTES に変換されます。  
  
-   データが大きくない UDT の場合、データベースの列の **[長さ]** プロパティは -1 または 8,000 バイトより大きい値に設定され、データは DT_IMAGE に変換されます。  
  
-   データが大きい UDT の場合、データは DT_IMAGE に変換されます。  
  
    > [!NOTE]  
    >  ADO NET ソースがエラー出力を使用するように構成されていない場合、データは DT_IMAGE 列に 8,000 バイトのチャンク単位でストリームされます。 ADO NET ソースがエラー出力を使用するように構成されている場合、バイトの配列全体が DT_IMAGE 列に渡されます。 エラー出力を使用するコンポーネントを構成する方法の詳細については、「 [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md)」(データのエラー処理) を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型、サポートされるデータ型変換、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を含む特定のデータベース間でのデータ型マッピングの詳細については、「 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型をマネージド データ型にマッピングする方法については、「[データ フロー内のデータ型の処理](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)」を参照してください。  
  
## <a name="ado-net-source-troubleshooting"></a>ADO NET ソースのトラブルシューティング  
 ADO NET ソースによる外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、ADO NET ソースによる外部データ ソースからのデータ読み込みに関するトラブルシューティングを行うことができます。 ADO NET ソースによる外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択します。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="ado-net-source-configuration"></a>ADO NET ソースの構成  
 ADO NET ソースを構成するには、結果セットを定義する SQL ステートメントを使用します。 たとえば、 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] データベースに接続し、SQL ステートメント `SELECT * FROM Production.Product` を使用する ADO NET ソースは、 **Production.Product** テーブルのすべての行を抽出し、データセットを下流コンポーネントに提供します。  
  
> [!NOTE]  
>  SQL ステートメントを使用して、一時テーブルから結果を返すストアド プロシージャが呼び出す場合は、WITH RESULT SETS オプションを使用して結果セットのメタデータを定義します。  
  
> [!NOTE]  
>  SQL ステートメントを使用してストアド プロシージャを実行する際に、パッケージが次のエラーで失敗した場合は、EXEC ステートメントの前に **SET FMTONLY OFF** ステートメントを追加すると、エラーを解決できることがあります。  
>   
>  **列 <column_name> がデータ ソースに見つかりません。**  
  
 ADO NET ソースは [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを使用してデータ ソースに接続します。この接続マネージャーは .NET プロバイダーを指定します。 詳細については、「 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)」(ADO.NET 接続マネージャー) を参照してください。  
  
 ADO NET ソースは、1 つの標準出力と 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO NET カスタム プロパティ](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>[ADO NET 変換元エディター] ([接続マネージャー] ページ)
  **[ADO NET 変換元エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、変換元の [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
 ADO NET 変換元の詳細については、「 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)」を参照してください。  
  
 **[接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換元を含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換元をダブルクリックします。  
  
3.  **[ADO NET 変換元エディター]** で、 **[接続マネージャー]** をクリックします。  
  
### <a name="static-options"></a>静的オプション  
 **ADO.NET 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|[テーブルまたはビュー]|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] データ ソースのテーブルまたはビューからデータを取得します。|  
|[SQL コマンド]|SQL クエリを使用して、 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データ ソースからデータを取得します。|  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 **プレビュー** では、最大で 200 行を表示できます。  
  
> [!NOTE]  
>  データをプレビューするときに、CLR ユーザー定義型を含む列にはデータが表示されません。 その代わりに、\<値が大きすぎて表示できません> または System.Byte[] が値として表示されます。 前者は、 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロバイダーを使用してデータ ソースにアクセスする場合に表示されます。後者は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client プロバイダーを使用している場合に表示されます。  
  
### <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
#### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[テーブル名またはビュー名]**  
 データ ソースで使用できるテーブルまたはビューの一覧から、テーブルまたはビューの名前を選択します。  
  
#### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成するか、 **[参照]** をクリックしてクエリ テキストを含むファイルを指定します。  
  
 **[クエリの作成]**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
## <a name="ado-net-source-editor-columns-page"></a>[ADO NET 変換元エディター] ([列] ページ)
  **[ADO NET 変換元エディター]** ダイアログ ボックスの **[列]** ページを使用すると、出力列をそれぞれの外部 (変換元) 列にマップできます。  
  
 ADO NET 変換元の詳細については、「 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)」を参照してください。  
  
 **[列] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換元を含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換元をダブルクリックします。  
  
3.  **[ADO NET 変換元エディター]** で、 **[列]** をクリックします。  
  
### <a name="options"></a>オプション  
 **使用できる外部列**  
 データ ソース内の使用できる外部列の一覧を表示します。 このテーブルを使用して列を追加または削除することはできません。  
  
 **[外部列]**  
 ここで表示される外部 (変換元) 列の順序は、この変換元のデータを使用するコンポーネントを構成するときの列の表示順に反映されます。  
  
 **出力列**  
 各出力列の一意な名前を表示します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 指定された名前は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
## <a name="ado-net-source-editor-error-output-page"></a>[ADO NET 変換元エディター] ([エラー出力] ページ)
  **[ADO NET 変換元エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択したり、エラー出力列のプロパティを設定したりできます。  
  
 ADO NET 変換元の詳細については、「 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)」を参照してください。  
  
 **[エラー出力] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換元を含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換元をダブルクリックします。  
  
3.  **[ADO NET 変換元エディター]** で、 **[エラー出力]** をクリックします。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[ADO NET 変換元エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択した外部 (変換元) 列を表示します。  
  
 **Error**  
 エラーが発生した場合に、障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **関連項目:** [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 切り捨てが発生したときの処理方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を指定します。  
  
 **[説明]**  
 エラーの説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="see-also"></a>参照  
 [DataReader 変換先](../../integration-services/data-flow/datareader-destination.md)   
 [ADO NET 変換先](../../integration-services/data-flow/ado-net-destination.md)   
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
