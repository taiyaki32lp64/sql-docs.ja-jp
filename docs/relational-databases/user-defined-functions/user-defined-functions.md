---
title: ユーザー定義関数 | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
- UDF
- TVF
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a659583df74cdc2e5100fcc25aa25e90af3bf22
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843839"
---
# <a name="user-defined-functions"></a>ユーザー定義関数
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  プログラミング言語の関数と同様、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のユーザー定義関数は、パラメーターを受け取り複雑な計算などの処理を実行してその結果を値として返すルーチンです。 戻り値は、単一のスカラー値または結果セットになります。  
   
##  <a name="Benefits"></a> ユーザー定義関数  
ユーザー定義関数 (UDF) を使用する理由とは? 
  
-   モジュール プログラミングが可能になります。  
  
     関数を作成してからデータベースに保存すると、プログラムの中で何度でも呼び出せます。 ユーザー定義関数は、プログラムのソース コードとは切り離して変更できます。  
  
-   実行が高速になります。  
  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数を使用すると、ストアド プロシージャと同様に、プランがキャッシュされ、これを再利用して繰り返し実行することで、[!INCLUDE[tsql](../../includes/tsql-md.md)] コードのコンパイル コストを削減できます。 つまり、ユーザー定義関数は、使用するたびに解析し直したり、最適化し直す必要がないので、実行時間が短縮されます。  
  
     計算や文字列の操作、ビジネス ロジックの場合は CLR 関数を使用することで、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数に比べてかなり高いパフォーマンスが得られます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数は、データ アクセスの多いロジックに適しています。  
  
-   ネットワーク トラフィックが減少します。  
  
     1 つのスカラー式で表現できない複雑な制約に基づいてデータをフィルター選択する操作を、1 つの関数として表現できます。 このような関数を WHERE 句で使用すれば、クライアントに送信される数や行を削減できます。  
  
> [!IMPORTANT]
> クエリの [!INCLUDE[tsql](../../includes/tsql-md.md)] UDF は、1 つのスレッドでのみ実行できます (直列実行プラン)。 そのため、UDF を使用すると、並列クエリ処理が禁止されます。 並列クエリ処理の詳細については、「[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing)」をご覧ください。
  
##  <a name="FunctionTypes"></a> 関数の種類  
**スカラー関数**  
 ユーザー定義のスカラー関数は、RETURNS 句で定義された型の単一のデータ値を返します。 インライン スカラー関数の場合、返されるスカラー値は単一ステートメントの結果です。 複数ステートメントを持つスカラー関数の場合、関数本体に、単一の値を返す一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含めることができます。 戻り値の型は、 **text**、 **ntext**、 **image**、 **cursor**、 **timestamp**を除く各種のデータ型になります。 
 **[使用例。](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)**
  
**テーブル値関数**  
 ユーザー定義テーブル値関数は、**table** データ型を返します。 インライン テーブル値関数の場合、テーブルは単一の SELECT ステートメントの結果セットであり、関数の本体がありません。 **[使用例。](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)**
  
**システム関数**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、さまざまな操作を実行するために使用できる多数のシステム関数が用意されています。 システム関数は変更できません。 詳細については、「[組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)」、「[システム ストアド関数 &#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-category-transact-sql.md)」、および「[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)」を参照してください。  
  
##  <a name="Guidelines"></a> ガイドライン  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントが取り消されて、モジュール (トリガーやストアド プロシージャ) 内の次のステートメントが続行されるようなエラーについては、関数内では扱いが異なります。 関数内では、このようなエラーによって関数自体の実行が停止されます。 そのため、次に関数を呼び出したステートメントも取り消されることになります。  
  
 `BEGIN...END` ブロック内のステートメントは、副作用を伴いません。 関数の副作用とは、データベース テーブルの変更など、その関数の有効範囲外のリソースの状態を永続的に変更してしまうことです。 関数内のステートメントが変更できる内容は、ローカル カーソルまたはローカル変数など、その関数に対してローカルなオブジェクトの変更のみです。 データベース テーブルの変更、関数に対してローカルではないカーソルの操作、電子メールの送信、カタログ変更、ユーザーへ返す結果セットの生成などの操作は、関数では実行できません。  
  
> [!NOTE]
> `CREATE FUNCTION` ステートメントの実行時に、存在しないリソースに対する副作用が `CREATE FUNCTION` ステートメントによってもたらされる場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってステートメントが実行されます。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では関数は呼び出されても実行されません。  
  
 クエリで指定した関数が実際に実行される回数は、オプティマイザーで作成された実行プランによって異なります。 `WHERE` 句のサブクエリによって起動された関数がその一例です。 サブクエリとその関数が実行された回数は、オプティマイザーが選択したアクセス パスの違いによって変わります。  
 
> [!IMPORTANT]   
> ユーザー定義関数のその他の情報とパフォーマンスに関する考慮事項については、「[ユーザー定義関数の作成 (データベース エンジン)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)」を参照してください。 
  
##  <a name="ValidStatements"></a> 関数で有効なステートメント  
関数では、次の種類のステートメントが有効です。  
  
-   関数に対してローカルなデータ変数やカーソルを定義するために使用できる `DECLARE` ステートメント。  
  
-   関数に対してローカルなオブジェクトへの値の代入。たとえば、`SET` を使用してスカラー変数やテーブルのローカル変数に値を代入します。  
  
-   ローカル カーソルを参照するカーソル操作。ローカル カーソルとは、関数内で宣言され、開かれ、閉じられ、割り当てが解除されるカーソルです。 クライアントにデータを返す `FETCH` ステートメントは使用できません。 `INTO` 句を使用してローカル変数に値を代入する FETCH ステートメントのみを使用できます。  
  
-   `TRY...CATCH` ステートメントを除く、フロー制御ステートメント。  
  
-   選択リストに、関数に対してローカルな変数に値を代入する式が含まれる、`SELECT` ステートメント。  
  
-   関数に対してローカルなテーブル変数を変更する `UPDATE`、`INSERT`、`DELETE` の各ステートメント。  
  
-   拡張ストアド プロシージャを呼び出す `EXECUTE` ステートメント。  
  
### <a name="built-in-system-functions"></a>組み込みシステム関数  
 Transact-SQL ユーザー定義関数では、次の非決定的な組み込み関数を使用できます。  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数では、次の非決定論的な組み込み関数を使用**できません**。  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 決定的および非決定的な組み込みシステム関数の一覧については、「[決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
##  <a name="SchemaBound"></a> スキーマ バインド関数  
 `CREATE FUNCTION` は、`SCHEMABINDING` 句をサポートしています。この句は、テーブル、ビュー、およびその他のユーザー定義関数など、参照対象オブジェクトのスキーマにその関数をバインドします。 スキーマ バインド関数によって参照されるオブジェクトを変更または削除しようとすると、失敗します。  
  
 [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) に `SCHEMABINDING` を指定するには、次の条件を満たしている必要があります。  
  
-   CREATE 関数が参照するすべてのビューとユーザー定義関数が、スキーマにバインドされている必要があります。  
  
-   この関数が参照するすべてのオブジェクトが、その関数と同じデータベースに含まれている必要があります。 対象となるオブジェクトは、1 つまたは 2 つの要素で構成される名前を使用して参照する必要があります。  
  
-   関数内のすべての参照対象オブジェクト (テーブル、ビュー、ユーザー定義関数) に `REFERENCES` 権限を所持している必要があります。  
  
 `ALTER FUNCTION` を使用してスキーマ バインドを削除できます。 関数を再定義するには、`ALTER FUNCTION` ステートメントを使用します。`WITH SCHEMABINDING` は指定しないでください。  
  
##  <a name="Parameters"></a> パラメーターの指定  
 ユーザー定義関数は、0 個またはそれ以上の入力パラメーターを受け取り、スカラー値またはテーブルのいずれかを返します。 1 つの関数では、最大で 1,024 個の入力パラメーターを受け取ることができます。 関数のパラメーターが既定値を持つ場合は、既定値を得るために、関数を呼び出すときに DEFAULT キーワードを指定する必要があります。 この動作はユーザー定義ストアド プロシージャ内の既定値を持つパラメーターとは異なります。ユーザー定義ストアド プロシージャの場合は、パラメーターを省略すると既定値が暗黙的に使用されます。 ユーザー定義関数では、出力パラメーターがサポートされません。  
  
##  <a name="Tasks"></a> 他の例について  
  
|||  
|-|-|  
|**タスクの説明**|**トピック**|  
|Transact-SQL ユーザー定義関数を作成する方法について説明します。|[ユーザー定義関数の作成 &#40;データベース エンジン&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|CLR 関数を作成する方法について説明します。|[CLR 関数の作成](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|ユーザー定義集計関数を作成する方法について説明します。|[ユーザー定義集計の作成](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|Transact-SQL ユーザー定義関数を変更する方法について説明します。|[ユーザー定義関数の変更](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|ユーザー定義関数を削除する方法について説明します。|[ユーザー定義関数の削除](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|ユーザー定義関数を実行する方法について説明します。|[ユーザー定義関数の実行](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|ユーザー定義関数の名前を変更する方法について説明します。|[ユーザー定義関数名の変更](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|ユーザー定義関数の定義を表示する方法について説明します。|[ユーザー定義関数の表示](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  
