---
title: '[ADO NET 変換先エディター] ([接続マネージャー] ページ) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.connection.f1
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: faeb72f875fd5427536ddd72db03ca71a25b293e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154030"
---
# <a name="ado-net-destination-editor-connection-manager-page"></a>[ADO NET 変換先エディター] ([接続マネージャー] ページ)
  **[ADO NET 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、変換先の [!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続を選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
 ADO NET 変換先の詳細については、「 [ADO NET Destination](data-flow/ado-net-destination.md)」を参照してください。  
  
 **[接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換先を含む [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換先をダブルクリックします。  
  
3.  **[ADO NET 変換先エディター]** で、 **[接続マネージャー]** をクリックします。  
  
## <a name="static-options"></a>静的オプション  
 **接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **新規**  
 **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[テーブルまたはビューを使用する]**  
 既存のテーブルまたはビューを一覧から選択するか、 **[新規作成]** をクリックして新しいテーブルを作成します。  
  
 **新規**  
 **[テーブルの作成]** ダイアログ ボックスを使用して、新しいテーブルまたはビューを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト (Blob) データ (SQL Server)](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 **プレビュー**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
 **[使用可能な場合は一括挿入を使用する]**  
 一括挿入操作のパフォーマンスを向上させるために <xref:System.Data.SqlClient.SqlBulkCopy> インターフェイスを使用するかどうかを指定します。  
  
 <xref:System.Data.SqlClient.SqlConnection> オブジェクトを返す ADO.NET プロバイダーのみが <xref:System.Data.SqlClient.SqlBulkCopy> インターフェイスの使用をサポートしています。 .NET Data Provider for SQL Server (SqlClient) は <xref:System.Data.SqlClient.SqlConnection> オブジェクトを返し、カスタム プロバイダーは <xref:System.Data.SqlClient.SqlConnection> オブジェクトを返す可能性があります。  
  
 .NET Data Provider for SQL Server (SqlClient) を使用して [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]に接続できます。  
  
 **[使用可能な場合は一括挿入を使用する]** を選択し、 **[エラー]** オプションを **[行をリダイレクトする]** に設定した場合、変換先によってエラー出力にリダイレクトされるデータのバッチに問題のない行が含まれる可能性があります。一括操作でのエラー処理の詳細については、「 [データのエラー処理](data-flow/error-handling-in-data.md)」を参照してください。 **[エラー]** オプションの詳細については、「[[ADO NET 変換先エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/ado-net-destination-editor-error-output-page.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] または Sybase のソース テーブルに ID 列が含まれている場合は、ADO NET 変換先の前と後に SQL 実行タスクを使用して SET IDENTITY_INSERT ステートメントを実行する必要があります。 ID 列プロパティは、列の増分値を指定します。 SET IDENTITY_INSERT ステートメントを使用することで、ID 列に明示的な値を挿入できます。 同じデータベース接続で CREATE TABLE ステートメントと SET IDENTITY ステートメントを実行するには、`RetainSameConnection` 接続マネージャーの [!INCLUDE[vstecado](../includes/vstecado-md.md)] プロパティを `True` に設定します。 また、SQL 実行タスクと ADO NET 変換先に同じ [!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーを使用します。  
>   
>  詳細については、「[SET IDENTITY_INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-identity-insert-transact-sql)」および「[IDENTITY &#40;プロパティ&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)」を参照してください。  
  
## <a name="external-resources"></a>外部リソース  
 sqlcat.com の技術記事「[Azure SQL Database へのデータの高速な読み込み](https://go.microsoft.com/fwlink/?LinkId=244333)」  
  
## <a name="see-also"></a>参照  
 [[ADO NET 変換先エディター] &#40;[マッピング] ページ&#41;](../../2014/integration-services/ado-net-destination-editor-mappings-page.md)   
 [[ADO NET 変換先エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/ado-net-destination-editor-error-output-page.md)   
 [ADO.NET 接続マネージャー](connection-manager/ado-net-connection-manager.md)   
 [SQL 実行タスク](control-flow/execute-sql-task.md)  
  
  
