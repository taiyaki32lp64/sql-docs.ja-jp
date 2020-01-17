---
title: sp_cursor_list (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_list
- sp_cursor_list_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_list
ms.assetid: 7187cfbe-d4d9-4cfa-a3bb-96a544c7c883
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5adcaab96bfe9af3945b479e4bff5180ca8140d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108579"
---
# <a name="spcursorlist-transact-sql"></a>sp_cursor_list (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  接続に対して現在開いているサーバー カーソルの属性を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursor_list [ @cursor_return = ] cursor_variable_name OUTPUT   
     , [ @cursor_scope = ] cursor_scope  
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @cursor_return= ] *cursor_variable_name*OUTPUT  
 宣言されているカーソル変数の名前を指定します。 *cursor_variable_name*は**カーソル**、既定値はありません。 カーソルはスクロール可能、動的、読み取り専用カーソルのいずれかです。  
  
 [ @cursor_scope= ] *cursor_scope*  
 レポートするカーソルのレベルを指定します。 *cursor_scope*は**int**, で、既定値はありませんはこれらの値のいずれかを指定します。  
  
|値|説明|  
|-----------|-----------------|  
|1|すべてのローカル カーソルをレポートします。|  
|2|すべてのグローバル カーソルをレポートします。|  
|3|ローカル カーソルとグローバル カーソルの両方をレポートします。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 sp_cursor_list は、結果セットとしてではなく、[!INCLUDE[tsql](../../includes/tsql-md.md)] カーソル出力パラメーターとしてレポートを返します。 これにより、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ、ストアド プロシージャ、および、一度に 1 行の出力の操作をトリガーします。 また、データベース API 関数からプロシージャを直接呼び出すことができなくなります。 カーソル出力パラメーターはプログラム変数にバインドする必要がありますが、データベース API では、カーソル パラメーターまたは変数のバインドがサポートされません。  
  
 以下は、sp_cursor_list から返されるカーソルの形式です。 このカーソルの形式は、sp_describe_cursor から返される形式と同じです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|カーソルを参照するために使用する名前。 DECLARE CURSOR ステートメントで指定された名前を介してカーソルへの参照であった場合、参照名はカーソル名と同じになります。 変数を介してカーソルを参照すると、参照名はカーソル変数の名前になります。|  
|cursor_name|**sysname**|DECLARE CURSOR ステートメントに指定されたカーソルの名前です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、カーソル、カーソル変数を設定して、カーソルが作成された場合、 **cursor_name**カーソル変数の名前を返します。  以前のバージョンでは、この出力列にはシステムが生成した名前が返されました。|  
|cursor_scope|**smallint**|1 = LOCAL<br /><br /> 2 = GLOBAL|  
|status|**smallint**|CURSOR_STATUS システム関数によってレポートされたものと同じ値です。<br /><br /> 1 = カーソル名または変数によって参照されたカーソルは開いています。 カーソルが状態非依存、静的、キーセットのいずれかの場合には、結果セットに少なくとも 1 行が含まれます。 カーソルが動的の場合には、結果セットに 0 行以上が含まれます。<br /><br /> 0 = カーソル名または変数によって参照されたカーソルは開いていますが、行は含まれていません。 動的カーソルがこの値を返すことはありません。<br /><br /> -1 = カーソル名または変数によって参照されたカーソルは閉じています。<br /><br /> -2 = カーソル変数にのみ適用されます。 変数に割り当てられたカーソルはありません。 おそらく、OUTPUT パラメーターによってカーソルを変数に割り当てましたが、戻る前にストアド プロシージャがカーソルを閉じました。<br /><br /> -3 = 指定された名前のカーソルまたはカーソル変数が存在しないか、またはカーソル変数にカーソルが割り当てられていません。|  
|model|**smallint**|1 = 状態非依存 (または静的)<br /><br /> 2 = キーセット<br /><br /> 3 = 動的<br /><br /> 4 = 高速順方向|  
|コンカレンシー|**smallint**|1 = 読み取り専用<br /><br /> 2 = スクロール ロック<br /><br /> 3 = オプティミスティック|  
|scrollable|**smallint**|0 = 順方向専用<br /><br /> 1 = スクロール可能|  
|open_status|**smallint**|0 = 閉じた状態<br /><br /> 1 = 開いた状態|  
|cursor_rows|**int**|結果セット内の条件を満たす行の数です。 詳細については、次を参照してください。 [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)します。|  
|fetch_status|**smallint**|このカーソル上での最後のフェッチの状態です。 詳細については、次を参照してください[@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md):。<br /><br /> 0 = フェッチが成功しました。<br /><br /> -1 = フェッチが失敗したか、またはカーソルの境界を越えています。<br /><br /> -2 = 要求された行がありません。<br /><br /> -9 = カーソル上でフェッチは行われていません。|  
|column_count|**smallint**|カーソル結果セットの列数です。|  
|row_count|**smallint**|カーソルで実行された最後の操作で処理された行数です。 詳細については、次を参照してください。 [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md)します。|  
|last_operation|**smallint**|カーソル上で実行された最後の操作:<br /><br /> 0 = カーソル上で操作は実行されていません。<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = 挿入<br /><br /> 4 = UPDATE<br /><br /> 5 = DELETE<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|サーバーのスコープ内でカーソルを識別する一意の値です。|  
  
## <a name="remarks"></a>コメント  
 sp_cursor_list は、接続によってオープンされた現在のサーバー カーソルの一覧を作成し、カーソルのスクロール機能や更新機能など、各カーソルにとってグローバルな属性を示します。 sp_cursor_list によってレポートされるカーソルは次のとおりです。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソル。  
  
-   API サーバー カーソルがカーソルに名前を付ける SQLSetCursorName が呼び出される、ODBC アプリケーションによって開かれました。  
  
 カーソルによって返される結果セットの属性の説明については、sp_describe_cursor_columns を使用します。 カーソルが参照するベース テーブルのレポートが必要な場合は、sp_describe_cursor_tables を使用します。 sp_describe_cursor は、指定のカーソルに関してだけ sp_cursor_list、としては、同じ情報を報告します。  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定では public ロールに与えられています。  
  
## <a name="examples"></a>使用例  
 次の例では、グローバル カーソルを開き、`sp_cursor_list` を使用してカーソルの属性をレポートします。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a keyset-driven cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_cursor_list.  
DECLARE @Report CURSOR;  
  
-- Execute sp_cursor_list into the cursor variable.  
EXEC master.dbo.sp_cursor_list @cursor_return = @Report OUTPUT,  
      @cursor_scope = 2;  
  
-- Fetch all the rows from the sp_cursor_list output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_cursor_list.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
