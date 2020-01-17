---
title: ADO NET 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetdest.f1
- sql13.dts.designer.adonetdest.connection.f1
- sql13.dts.designer.adonetdest.mappings.f1
- sql13.dts.designer.adonetdest.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6829260583ebc3c1b0dec3fec5d3158ddbbea297
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293525"
---
# <a name="ado-net-destination"></a>ADO NET 変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ADO NET 変換先では、データベースのテーブルやビューを使用する、さまざまな [!INCLUDE[vstecado](../../includes/vstecado-md.md)]互換データベースにデータを読み込みます。 このデータを既存のテーブルやビューに読み込むことができますが、新しいテーブルを作成して、そこにデータを読み込むこともできます。  
  
 ADO NET 変換先を使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]に接続できます。 OLE DB を使用した [!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続はサポートされていません。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の詳細については、「[一般的な制限事項とガイドライン (Azure SQL Database)](https://go.microsoft.com/fwlink/?LinkId=248228)」を参照してください。  
  
## <a name="troubleshooting-the-ado-net-destination"></a>ADO NET 変換先のトラブルシューティング  
 ADO NET 変換先による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、ADO NET 変換先による外部データ ソースへのデータ保存に関するトラブルシューティングを行えます。 ADO NET 変換先による外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択します。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="configuring-the-ado-net-destination"></a>ADO NET 変換先の構成  
 この変換先は [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを使用してデータ ソースに接続します。また、この接続マネージャーでは、使用する [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロバイダーを指定します。 詳細については、「 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)」(ADO.NET 接続マネージャー) を参照してください。  
  
 ADO NET 変換先には、入力列と変換先データ ソースの列との間のマッピングが含まれています。 入力列を変換先のすべての列にマップする必要はありません。 ただし、一部の変換先列のプロパティで、入力列のマップが必要になることがあります。 マップしない場合、エラーが発生することがあります。 たとえば、変換先列で NULL 値が許容されていない場合は、入力列をその変換先列にマップする必要があります。 また、マップされる列のデータ型には互換性がある必要があります。 たとえば、 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] プロバイダーで文字列データ型の入力列を数値データ型の変換先列にマップすることがサポートされていなければ、その操作はできません。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データ型が IMAGE 型に設定された列にテキストを挿入することはサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型の詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  ADO NET 変換先では、DT_DBTIME 型に設定されている入力列を datetime 型に設定されているデータベース列にマップすることがサポートされていません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型について詳しくは、「 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」をご覧ください。  
  
 ADO NET 変換先は、1 つの標準入力と 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO NET カスタム プロパティ](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="ado-net-destination-editor-connection-manager-page"></a>[ADO NET 変換先エディター] ([接続マネージャー] ページ)
  **[ADO NET 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、変換先の [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続を選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
 **[接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換先を含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換先をダブルクリックします。  
  
3.  **[ADO NET 変換先エディター]** で、 **[接続マネージャー]** をクリックします。  
  
### <a name="static-options"></a>静的オプション  
 **Connection manager**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[テーブルまたはビューを使用する]**  
 既存のテーブルまたはビューを一覧から選択するか、 **[新規作成]** をクリックして新しいテーブルを作成します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して、新しいテーブルまたはビューを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 **プレビュー**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
 **[使用可能な場合は一括挿入を使用する]**  
 一括挿入操作のパフォーマンスを向上させるために <xref:System.Data.SqlClient.SqlBulkCopy> インターフェイスを使用するかどうかを指定します。  
  
 <xref:System.Data.SqlClient.SqlConnection> オブジェクトを返す ADO.NET プロバイダーのみが <xref:System.Data.SqlClient.SqlBulkCopy> インターフェイスの使用をサポートしています。 .NET Data Provider for SQL Server (SqlClient) は <xref:System.Data.SqlClient.SqlConnection> オブジェクトを返し、カスタム プロバイダーは <xref:System.Data.SqlClient.SqlConnection> オブジェクトを返す可能性があります。  
  
 .NET Data Provider for SQL Server (SqlClient) を使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]に接続できます。  
  
 **[使用可能な場合は一括挿入を使用する]** を選択し、 **[エラー]** オプションを **[行をリダイレクトする]** に設定した場合、変換先によってエラー出力にリダイレクトされるデータのバッチに問題のない行が含まれる可能性があります。一括操作でのエラー処理の詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。 **[エラー]** オプションの詳細については、「[[ADO NET 変換先エディター] &#40;[エラー出力] ページ&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)」を参照してください。  
  
> [!NOTE]
>  SQL Server または Sybase 変換元テーブルに ID 列が含まれる場合、SQL 実行タスクを利用し、ADO NET 変換先の前に IDENTITY_INSERT を有効にし、その後再び無効にする必要があります。 (ID 列プロパティは、列の増分値を指定します。 SET IDENTITY_INSERT ステートメントにより、変換先テーブルの ID 列に、変換元テーブルの明示的値を挿入できます。)  
> 
>   SET IDENTITY_INSERT ステートメントとデータ読み込みを正常に実行するには、次を行う必要があります。  
>       1.SQL 実行タスクと ADO NET 変換先に同じ ADO.NET 接続マネージャーを使用します。  
>       2.接続マネージャーで、**RetainSameConnection** プロパティと **MultipleActiveResultSets** プロパティを True に設定します。  
>       3.ADO.NET 変換先で、**UseBulkInsertWhenPossible** プロパティを False に設定します。   
> 
>  詳細については、「[SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)」および「[IDENTITY &#40;プロパティ&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)」を参照してください。  
  
## <a name="external-resources"></a>外部リソース  
 sqlcat.com の技術記事「[Azure SQL Database へのデータの高速な読み込み](https://go.microsoft.com/fwlink/?LinkId=244333)」  
  
## <a name="ado-net-destination-editor-mappings-page"></a>[ADO NET 変換先エディター] ([マッピング] ページ)
  **[ADO NET 変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
 **[マッピング] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換先を含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換先をダブルクリックします。  
  
3.  **[ADO NET 変換先エディター]** で、 **[マッピング]** をクリックします。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる入力列を変換先列にマップします。  
  
 **使用できる変換先列**  
 使用できる変換先列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる変換先列を入力列にマップします。  
  
 **入力列**  
 選択した入力列を表示します。 出力から列を除外するために **\<無視>** を選択することで、マッピングを削除できます。  
  
 **変換先列**  
 マップするかどうかにかかわらず、使用できる変換先列を表示します。  
  
## <a name="ado-net-destination-editor-error-output-page"></a>[ADO NET 変換先エディター] ([エラー出力] ページ)
  **[ADO NET 変換先エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを指定できます。  
  
 **[エラー出力] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換先を含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換先をダブルクリックします。  
  
3.  **[ADO NET 変換先エディター]** で、 **[エラー出力]** をクリックします。  
  
### <a name="options"></a>オプション  
 **入力または出力**  
 入力の名前を表示します。  
  
 **列**  
 使用されていません。  
  
 **Error**  
 エラーが発生した場合に、障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **関連項目:** [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 使用されていません。  
  
 **[説明]**  
 操作の説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
  
