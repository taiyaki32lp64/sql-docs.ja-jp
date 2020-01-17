---
title: '[テーブル作成 SQL ステートメント] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f541ad24e87bf5bdea9ed8b8c2523a73c81daa9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768004"
---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>[テーブル作成 SQL ステートメント] (SQL Server インポートおよびエクスポート ウィザード)
  使用して、**テーブル作成 SQL ステートメント** ダイアログ ボックスが自動的に生成されたステートメントを表示したり、目的に応じて変更します。 このステートメントを変更する場合、それに関連して、列のマッピングにも変更を加えなければならない場合があります。それ以降も、編集した SQL ステートメントは手動で保守する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 このウィザードの詳細については、次を参照してください。 [SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)します。 ウィザードを正常に実行するために必要なアクセス許可と同様に、ウィザードを開始するためのオプションについては、次を参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
 SQL Server インポートおよびエクスポート ウィザードの目的は、変換元から変換先にデータをコピーすることです。 また、このウィザードでは、変換先データベースと変換先テーブルも作成できます。 ただし、複数のデータベースやテーブルまたは他の種類のデータベース オブジェクトをコピーする必要がある場合は、データベース コピー ウィザードを使用してください。 詳細については、「 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="options"></a>および  
 **SQL ステートメント**  
 自動生成された SQL ステートメントが表示され、編集できます。  
  
> [!NOTE]  
>  SQL ステートメントにキャリッジ リターンを含める場合は、<localizedText>Ctrl</localizedText> キーを押しながら <localizedText>Enter</localizedText> キーを押します。 Enter</localizedText> キーだけを押すと、ダイアログ ボックスが終了します。  
  
 **自動生成**  
 既定の SQL ステートメントを変更していた場合、 **[自動生成]** をクリックすると復元されます。  
  
  
