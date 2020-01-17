---
title: ユーザー定義関数 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1ce64f821edd68dceaa1809a62a6b894ded6a868
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211697"
---
# <a name="user-defined-functions"></a>ユーザー定義関数
  プログラミング言語の関数と同様、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のユーザー定義関数は、パラメーターを受け取り複雑な計算などの処理を実行してその結果を値として返すルーチンです。 戻り値は、単一のスカラー値または結果セットになります。  
  
 **このトピックの内容**  
  
 [ユーザー定義関数の利点](#Benefits)  
  
 [関数の種類](#FunctionTypes)  
  
 [ガイドライン](#Guidelines)  
  
 [関数で有効なステートメント](#ValidStatements)  
  
 [スキーマ バインド関数](#SchemaBound)  
  
 [パラメーターを指定します。](#Parameters)  
  
 [関連タスク](#Tasks)  
  
##  <a name="Benefits"></a> ユーザー定義関数の利点  
 次に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でユーザー定義関数を使用する利点を示します。  
  
-   モジュール プログラミングが可能になります。  
  
     関数を作成してからデータベースに保存すると、プログラムの中で何度でも呼び出せます。 ユーザー定義関数は、プログラムのソース コードとは切り離して変更できます。  
  
-   実行が高速になります。  
  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数を使用すると、ストアド プロシージャと同様に、プランがキャッシュされ、これを再利用して繰り返し実行することで、[!INCLUDE[tsql](../../includes/tsql-md.md)] コードのコンパイル コストを削減できます。 つまり、ユーザー定義関数は、使用するたびに解析し直したり、最適化し直す必要がないので、実行時間が短縮されます。  
  
     計算や文字列の操作、ビジネス ロジックの場合は CLR 関数を使用することで、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数に比べてかなり高いパフォーマンスが得られます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数は、データ アクセスの多いロジックに適しています。  
  
-   ネットワーク トラフィックが減少します。  
  
     1 つのスカラー式で表現できない複雑な制約に基づいてデータをフィルター選択する操作を、1 つの関数として表現できます。 このような関数を WHERE 句で使用すれば、クライアントに送信される数や行を削減できます。  
  
> [!NOTE]  
>  クエリの [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数は、1 つのスレッドでのみ実行できます (直列実行プラン)。  
  
##  <a name="FunctionTypes"></a> 関数の種類  
 スカラー関数  
 ユーザー定義のスカラー関数は、RETURNS 句で定義された型の単一のデータ値を返します。 インライン スカラー関数の場合、スカラー値は単一ステートメントの結果であり、関数の本体がありません。 複数ステートメントを持つスカラー関数の場合、BEGIN...END ブロックで定義された関数本体に、単一の値を返す一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが含まれています。 この関数の戻り値には、`text`、`ntext`、`image`、`cursor`、および `timestamp` 以外の任意のデータ型を指定できます。  
  
 テーブル値関数  
 ユーザー定義テーブル値関数は、`table` データ型を返します。 インライン テーブル値関数の場合、テーブルは単一の SELECT ステートメントの結果セットであり、関数の本体がありません。  
  
 システム関数  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、さまざまな操作を実行するために使用できる多数のシステム関数が用意されています。 システム関数は変更できません。 詳細については、「[組み込み関数 &#40;Transact-SQL&#41;](/sql/t-sql/functions/functions)」、「[システム ストアド関数 &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/system-functions-for-transact-sql)」、および「[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views)」を参照してください。  
  
##  <a name="Guidelines"></a> ガイドライン  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントが取り消されて、モジュール (トリガーやストアド プロシージャ) 内の次のステートメントが続行されるようなエラーについては、関数内では扱いが異なります。 関数内では、このようなエラーによって関数自体の実行が停止されます。 そのため、次に関数を呼び出したステートメントも取り消されることになります。  
  
 BEGIN...END ブロック内のステートメントは、副作用を伴いません。 関数の副作用とは、データベース テーブルの変更など、その関数の有効範囲外のリソースの状態を永続的に変更してしまうことです。 関数内のステートメントが変更できる内容は、ローカル カーソルまたはローカル変数など、その関数に対してローカルなオブジェクトの変更のみです。 データベース テーブルの変更、関数に対してローカルではないカーソルの操作、電子メールの送信、カタログ変更、ユーザーへ返す結果セットの生成などの操作は、関数では実行できません。  
  
> [!NOTE]  
>  CREATE FUNCTION ステートメントの実行時に、存在しないリソースに対する副作用がもたらされる場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってステートメントが実行されます。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では関数は呼び出されても実行されません。  
  
 クエリで指定した関数が実際に実行される回数は、オプティマイザーで作成された実行プランによって異なります。 WHERE 句のサブクエリによって起動された関数がその一例です。 サブクエリとその関数が実行された回数は、オプティマイザーが選択したアクセス パスの違いによって変わります。  
  
##  <a name="ValidStatements"></a> 関数で有効なステートメント  
 関数では、次の種類のステートメントが有効です。  
  
-   関数に対してローカルなデータ変数やカーソルを定義するために使用できる DECLARE ステートメント。  
  
-   関数に対してローカルなオブジェクトへの値の代入。たとえば、SET を使用してスカラー変数やテーブルのローカル変数に値を代入します。  
  
-   ローカル カーソルを参照するカーソル操作。ローカル カーソルとは、関数内で宣言され、開かれ、閉じられ、割り当てが解除されるカーソルです。 クライアントにデータを返す FETCH ステートメントは使用できません。 INTO 句を使用してローカル変数に値を代入する FETCH ステートメントのみを使用できます。  
  
-   TRY...CATCH ステートメントを除く、フロー制御ステートメント。  
  
-   選択リストに、関数に対してローカルな変数に値を代入する式が含まれる、SELECT ステートメント。  
  
-   関数に対してローカルなテーブル変数を変更する INSERT、UPDATE、および DELETE の各ステートメント。  
  
-   拡張ストアド プロシージャを呼び出す EXECUTE ステートメント。  
  
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
  
 Transact-SQL ユーザー定義関数では、次の非決定的な組み込み関数を使用できません。  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 決定的および非決定的な組み込みシステム関数の一覧については、「[決定的関数と非決定的関数](../user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
##  <a name="SchemaBound"></a> スキーマ バインド関数  
 CREATE FUNCTION は、SCHEMABINDING 句をサポートしています。この句は、テーブル、ビュー、およびその他のユーザー定義関数など、参照対象オブジェクトのスキーマにその関数をバインドします。 スキーマ バインド関数によって参照されるオブジェクトを変更または削除しようとすると、失敗します。  
  
 CREATE FUNCTION に SCHEMABINDING を指定するには、次の条件を満たしている必要があります。  
  
-   CREATE 関数が参照するすべてのビューとユーザー定義関数が、スキーマにバインドされている必要があります。  
  
-   この関数が参照するすべてのオブジェクトが、その関数と同じデータベースに含まれている必要があります。 対象となるオブジェクトは、1 つまたは 2 つの要素で構成される名前を使用して参照する必要があります。  
  
-   関数内のすべての参照対象オブジェクト (テーブル、ビュー、およびユーザー定義関数) に REFERENCES 権限を所持している必要があります。  
  
 ALTER FUNCTION を使用して、スキーマ バインドを削除できます。 関数を再定義するには、ALTER FUNCTION ステートメントを使用します。WITH SCHEMABINDING は指定しないでください。  
  
##  <a name="Parameters"></a> パラメーターを指定します。  
 ユーザー定義関数は、0 個またはそれ以上の入力パラメーターを受け取り、スカラー値またはテーブルのいずれかを返します。 1 つの関数では、最大で 1,024 個の入力パラメーターを受け取ることができます。 関数のパラメーターが既定値を持つ場合は、既定値を得るために、関数を呼び出すときに DEFAULT キーワードを指定する必要があります。 この動作はユーザー定義ストアド プロシージャ内の既定値を持つパラメーターとは異なります。ユーザー定義ストアド プロシージャの場合は、パラメーターを省略すると既定値が暗黙的に使用されます。 ユーザー定義関数では、出力パラメーターがサポートされません。  
  
##  <a name="Tasks"></a> 関連タスク  
  
|||  
|-|-|  
|**タスクの説明**|**トピック**|  
|Transact-SQL ユーザー定義関数を作成する方法について説明します。|[ユーザー定義関数の作成 &#40;データベース エンジン&#41;](../user-defined-functions/create-user-defined-functions-database-engine.md)|  
|CLR 関数を作成する方法について説明します。|[CLR 関数の作成](../user-defined-functions/create-clr-functions.md)|  
|ユーザー定義集計関数を作成する方法について説明します。|[ユーザー定義集計の作成](../user-defined-functions/create-user-defined-aggregates.md)|  
|Transact-SQL ユーザー定義関数を変更する方法について説明します。|[ユーザー定義関数の変更](../user-defined-functions/user-defined-functions.md)|  
|ユーザー定義関数を削除する方法について説明します。|[ユーザー定義関数の削除](../user-defined-functions/delete-user-defined-functions.md)|  
|ユーザー定義関数を実行する方法について説明します。|[ユーザー定義関数の実行](../user-defined-functions/execute-user-defined-functions.md)|  
|ユーザー定義関数の名前を変更する方法について説明します。|[ユーザー定義関数名の変更](../user-defined-functions/rename-user-defined-functions.md)|  
|ユーザー定義関数の定義を表示する方法について説明します。|[ユーザー定義関数の表示](view-user-defined-functions.md)|  
  
  
