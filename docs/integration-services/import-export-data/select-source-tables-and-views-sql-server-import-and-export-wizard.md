---
title: '[コピー元のテーブルおよびビューを選択] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3d3019419538c05efc28ceabc5324d373500f65c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285131"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>[コピー元のテーブルおよびビューを選択]\(SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  テーブル全体をコピーするか、クエリを入力するかを指定した後に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードには **[コピー元のテーブルおよびビューを選択]** が表示されます。 このページでは、コピーする既存のテーブルとビューを選択します。 それから、新規または既存のコピー先テーブルにコピー元テーブルをマッピングします。 必要に応じて、個々の列のマッピングも確認し、サンプル データをプレビューします。

> [!TIP]
> 複数の SQL Server データベース、またはテーブルとビュー以外の SQL Server データベース オブジェクトをコピーする必要がある場合は、インポートおよびエクスポート ウィザードではなく、データベース コピー ウィザードを使います。 詳細については、「 [データベース コピー ウィザードの使用](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>スクリーンショット - テーブルをコピーする場合  
 次のスクリーンショットでは、 **[テーブルのコピーまたはクエリの指定]** ページで **[1 つ以上のテーブルまたはビューからデータをコピーする]** オプションを以前に選択したときに表示される、ウィザードの **[コピー元のテーブルおよびビューを選択]** ページの例を示します。 この一覧には、データ ソースで使用可能なすべてのテーブルとビューが表示されます。
 
この例では、 **[変換元]** の一覧には AdventureWorks サンプル データベース内のすべてのテーブルが含まれます。 選択された行は、ユーザーが **Sales.Customer** テーブルを新しい **Sales.CustomerNew** テーブルにコピーすることを示します。 
   
 ![インポートおよびエクスポート ウィザードの [テーブルの選択] ページ](../../integration-services/import-export-data/media/select-tables1.png "インポートおよびエクスポート ウィザードの [テーブルの選択] ページ")
  
## <a name="screen-shot---if-you-provided-a-query"></a>スクリーンショット - クエリを指定した場合  
 次のスクリーンショットは、 **[テーブルのコピーまたはクエリの指定]** ページの **[転送するデータを指定するためのクエリを記述する]** オプションを選択した後に表示される、ウィザードの **[コピー元のテーブルおよびビューを選択]** ページの例を示しています。 **[変換元]** の一覧には 1 つの行だけが含まれ、`[Query]` という名前の項目は **[基になるクエリの指定]** ページで指定したクエリを表します。
 
この例では、ユーザーがクエリ結果を **Sales.CustomerNew** テーブルにコピーします。  
    
 ![インポートおよびエクスポート ウィザードの [テーブルの選択] ページ](../../integration-services/import-export-data/media/select-tables2.png "インポートおよびエクスポート ウィザードの [テーブルの選択] ページ")  

## <a name="select-source-and-destination-tables"></a>変換元のテーブルと変換先のテーブルの選択 
**ソース**  
チェック ボックスを使用して、コピー先にコピーできるテーブルとビューを一覧から選択します。 既定では、データ ソースのデータが変更なくコピーされます。 新しい変換先テーブルを作成する場合、新しいテーブルのスキーマつまり列とそのプロパティの一覧も、データ ソースから変更なしにコピーされます。

クエリを指定した場合は、一覧には `[Query]` という名前の項目が 1 つだけ含まれます。 

**変換先**  
 変換元の各テーブルまたはクエリの一覧で変換先テーブルを選択するか、ウィザードで作成する新しいテーブルの名前を入力します。 既存の変換先テーブルを選択する場合、そのテーブルの列とデータ型は変換元テーブルと互換性がある必要があります。  

> [!NOTE]
> この時点でウィザードを一時停止し、外部ツール (  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]など) を使用して変換先データベースに新しいテーブルを手動で作成した場合、新しいテーブルは使用可能な変換先テーブルの一覧にすぐには表示されません。 変換先テーブルの一覧を最新の情報に更新するには、 **[変換先の選択]** ページに戻り、変換先データベースを再度選択して、使用可能なテーブルとビューの一覧を最新の情報に更新してから、もう一度 **[コピー元のテーブルおよびビューを選択]** ページに進みます。  

## <a name="optionally-review-column-mappings-and-preview-data"></a>必要に応じて、列マッピングとプレビュー データをレビューします。
**マッピングの編集**   
必要に応じて、 **[マッピングの編集]** をクリックして、選択したテーブルに対する **[列マッピング]** ダイアログ ボックスを表示します。 **[列マッピング]** ダイアログ ボックスを使用して、次のことを行います。
-   変換元と変換先の間の個々の列のマッピングを確認します。
-   列のサブセットのみをコピーするには、コピーしない列について **[無視]** を選択します。

詳細については、「 [列マッピング](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)」を参照してください。  

**プレビュー**  
必要に応じて、 **[プレビュー]** をクリックして、 **[データのプレビュー]** ダイアログ ボックスで、最大 200 行のサンプル データをプレビューします。 プレビューで、コピーしたいデータがウィザードによってコピーされることを確認します。 詳細については、 [データのプレビュー](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)に関するページを参照してください。  
  
データをプレビューした後で、ウィザードの前のページで選択したオプションを変更してもかまいません。 これらの変更を行うには、 **[コピー元のテーブルおよびビューを選択]** ページに戻り、 **[戻る]** をクリックし、選択の変更が可能な前のページに戻ります。  

## <a name="select-source-and-destination-tables-for-excel"></a>Excel の変換元のテーブルと変換先のテーブルの選択

> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。

### <a name="excel-source-tables"></a>Excel の変換元テーブル
Excel データ ソースの変換元テーブルとビューの一覧には、2 種類の Excel オブジェクトがあります。
-   **ワークシート**。 ワークシート名の末尾にはドル記号 ($) が付きます (例: **'Sheet1$'** )。
-   **名前付き範囲** 名前付き範囲 (ある場合) は名前別に表示されます。

特定の名前のない範囲のセル (たとえば、 **[Sheet1$A1:B4]** ) との間でデータの読み込みを行う場合、クエリを記述する必要があります。 **[テーブルのコピーまたはクエリの指定]** ページに戻り、 **[転送するデータを指定するためのクエリを記述する]** を選択します。

### <a name="excel-destination-tables"></a>Excel 変換先テーブル
Excel にデータをエクスポートする場合、変換先として、次の 3 つのうちいずれかを指定できます。
-   **ワークシート。** ワークシートを指定するには、シート名の末尾に $ 文字を付加し、文字列を区切り文字で囲みます (例: **[Sheet1$]** )。
-   **名前付き範囲。** 名前付き範囲を指定するには、範囲名をそのまま使用します (例: **MyDataRange**)。
-   **名前のない範囲。** 名前のないセルの範囲を指定するには、シート名の末尾に $ 文字を付加し、範囲の指定を追加し、文字列を区切り文字で囲みます (例: **[Sheet1$A1:B4]** )。

> [!TIP]
> 変換元または変換先として Excel を使用する場合、 **[列マッピング]** ページで **[マッピングの編集]** をクリックし、データ型マッピングを確認することをお勧めします。 

## <a name="whats-next"></a>次の操作  
 変換先テーブルにコピーおよびマップする既存のテーブルおよびビューを選択した後に表示されるのは、 **[パッケージの保存および実行]** ページです。 このページでは、コピー操作をすぐに実行するかどうかを指定します。 構成によっては、ウィザードによって作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを保存して、それをカスタマイズし、後から再利用することができます。 詳細については、 [パッケージの保存および実行](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)に関するページを参照してください。
 
 ## <a name="see-also"></a>参照
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)



