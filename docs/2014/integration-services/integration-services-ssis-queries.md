---
title: Integration Services (SSIS) のクエリ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b4323715155ddb433012624f9d7a5df9bb0a29c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767664"
---
# <a name="integration-services-ssis-queries"></a>Integration Services (SSIS) のクエリ
  SQL 実行タスク、OLE DB ソース、OLE DB 変換先、および参照変換では、SQL クエリを使用できます。 SQL 実行タスクでは、SQL ステートメントによってデータベース オブジェクトとデータを作成、更新、および削除したり、ストアド プロシージャを実行したり、SELECT ステートメントを実行したりすることができます。 OLE DB ソースと参照変換の場合、通常 SQL ステートメントは SELECT ステートメントまたは EXEC ステートメントです。 EXEC ステートメントで最もよく実行するのは、結果セットを返すストアド プロシージャです。  
  
 クエリを解析して、有効かどうかを確認できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]への接続を使用するクエリを解析すると、クエリは解析後に実行されて、実行結果 (成功または失敗) が解析結果に割り当てられます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]以外のデータへの接続をクエリで使用する場合、ステートメントは解析されるだけです。  
  
 SQL ステートメントを定義するには、デザイナーに直接入力するか、ステートメントを含むファイル接続または変数を指定します。  
  
## <a name="direct-input-sql"></a>直接入力 SQL  
 クエリ ビルダーは、SQL 実行タスク、OLE DB ソース、OLE DB 変換先、および参照変換のユーザー インターフェイスで使用できます。 クエリ ビルダーを使用すると次の利点があります。  
  
-   視覚的な作業、または SQL コマンドを使用した作業  
  
     クエリ ビルダーには、クエリを視覚的に構成するグラフィカル ペインと、クエリの SQL テキストを表示するテキスト ペインがあります。 グラフィカル ペインとテキスト ペインのどちらでも作業ができます。 これらの表示はクエリ ビルダーによって同期されるため、クエリのテキストとグラフィカルな表示は常に一致します。  
  
-   関係付けられたテーブルの結合  
  
     クエリに複数のテーブルを追加する場合、クエリ ビルダーでは自動的にテーブル間の関係を認識し、適切な結合コマンドを作成します。  
  
-   データベースのクエリまたは更新  
  
     クエリ ビルダーでは、Transact-SQL SELECT ステートメントを使用してデータを返すことができます。また、データベースのレコードの更新、追加、削除を行うクエリを作成できます。  
  
-   結果の即時の表示と変更  
  
     クエリを実行したり、グリッドのレコードセットを使用して、データベースのレコードのスクロールや編集ができます。  
  
 クエリ ビルダーの視覚的な作業で作成できるのは SELECT クエリだけですが、テキスト ペインには DELETE や UPDATE ステートメントなど他の種類の SQL ステートメントを入力できます。 入力した SQL ステートメントに合わせて、グラフィカル ペインも自動的に更新されます。  
  
 また、直接入力は、タスクやデータ フロー コンポーネントのダイアログ ボックス、またはプロパティ ウィンドウにクエリを入力しても行えます。  
  
 詳細については、「 [クエリ ビルダー](../../2014/integration-services/query-builder.md)」を参照してください。  
  
## <a name="sql-in-files"></a>ファイルの SQL  
 SQL 実行タスクの SQL ステートメントを、別のファイルに格納しておくことも可能です。 たとえば、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のクエリ エディターのようなツールを使用してクエリを記述し、ファイルに保存して、パッケージを実行するときにファイルからクエリを読み込むことができます。 ファイルには、実行する SQL ステートメントとコメントのみを含めることができます。 ファイルに格納された SQL ステートメントを使用するには、ファイル名とファイルの場所を指定するファイル接続を用意する必要があります。 詳しくは「 [File Connection Manager](connection-manager/file-connection-manager.md)」をご覧ください。  
  
## <a name="sql-in-variables"></a>変数の SQL  
 SQL 実行タスクの SQL ステートメントのソースが変数の場合、クエリが格納されている変数の名前を指定します。 変数の Value プロパティにクエリのテキストを格納します。 変数の ValueType プロパティを文字列データ型に設定し、Value プロパティに SQL ステートメントを入力またはコピーします。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)」をご覧ください。  
  
  
