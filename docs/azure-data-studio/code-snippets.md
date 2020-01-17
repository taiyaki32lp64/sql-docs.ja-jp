---
title: 再利用可能なコード スニペットの作成
titleSuffix: Azure Data Studio
description: Azure Data Studio で SQL コード スニペットを作成して使用する方法について学習します
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 09a8432d10a70bb8530654d76bce874f735788a6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959707"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] でコード スニペットを作成して使用し、Transact-SQL (T-SQL) スクリプトをすばやく作成する

[!INCLUDE[name-sos](../includes/name-sos-short.md)] のコード スニペットは、データベースおよびデータベース オブジェクトを簡単に作成できるようにするテンプレートです。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] には、適切な構文を迅速に生成するのに役立つ、複数の T-SQL スニペットが用意されています。 

ユーザー定義のコード スニペットを作成することもできます。

## <a name="using-built-in-t-sql-code-snippets"></a>組み込みの T-SQL コード スニペットの使用

1. 使用可能なスニペットにアクセスするには、クエリ エディターで「*sql*」と入力してリストを開きます。

   ![スニペット](media/code-snippets/sql-snippets.png)

1. 使用するスニペットを選択すると、T-SQL スクリプトが生成されます。 たとえば、*sqlCreateTable* を選択します。

   ![テーブル スニペットの作成](media/code-snippets/create-table.png)

1. 強調表示されたフィールドを特定の値で更新します。 たとえば、*TableName* と *Schema* をデータベースの値に置き換えます。

   ![テンプレート フィールドの置換](media/code-snippets/table-from-snippet.png)

   変更するフィールドが強調表示されなくなった場合 (これは、エディターの周囲でカーソルを移動したときに発生します)、変更する単語を右クリックし、 **[すべての出現箇所を変更]** を選択します。

   ![テンプレート フィールドの置換](media/code-snippets/change-all.png)

1. 選択したスニペットに必要な追加の T-SQL を更新または追加します。 たとえば、*Column1*、*Column2* を更新し、さらに列を追加します。


 
## <a name="creating-sql-code-snippets"></a>SQL コード スニペットを作成する 

独自のスニペットを定義できます。 編集するために SQL スニペット ファイルを開くには、次の操作を行います。

1. *コマンド パレット* (**Shift + Ctrl + P**) を開き、「*snip*」と入力して、 **[基本設定: ユーザー スニペットを開く]** を選択します。

   ![テンプレート フィールドの置換](media/code-snippets/user-snippets.png)

1. **[SQL]** を選択します。

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] では Visual Studio Code からそのコード スニペット機能を継承するため、この記事では SQL スニペットの使用について具体的に説明します。 詳細については、Visual Studio Code ドキュメントの「[独自のスニペットを作成する](https://code.visualstudio.com/docs/editor/userdefinedsnippets)」を参照してください。 

   ![テンプレート フィールドの置換](media/code-snippets/select-sql.png)

1. 次のコードを *sql.json* に貼り付けます。

   ```sql
   {
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   }
   ```

1. sql.json ファイルを保存します。
1. **Ctrl+N** キーをクリックして、新しいクエリ エディター ウィンドウを開きます。
2. 「**sql**」と入力すると、追加した 2 つのユーザー スニペット (*sqlCreateTable2* と *sqlSelectTop5*) が表示されます。

新しいスニペットの 1 つを選択し、テストを実行してみましょう。


## <a name="additional-resources"></a>その他のリソース

SQL エディターの詳細については、[コード エディターのチュートリアル](tutorial-sql-editor.md)に関するページを参照してください。
