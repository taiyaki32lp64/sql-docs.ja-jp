---
title: sp_describe_cursor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor
- sp_describe_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor
ms.assetid: 0c836c99-1147-441e-998c-f0a30cd05275
author: stevestein
ms.author: sstein
ms.openlocfilehash: f82fc9006012d55902f1b5b3260dc7012fd6640a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053068"
---
# <a name="spdescribecursor-transact-sql"></a>sp_describe_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー カーソルの属性を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_describe_cursor [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
    , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
    , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @cursor_return=] *output_cursor_variable*出力  
 カーソル出力を受け取るように宣言したカーソル変数の名前です。 *output_cursor_variable*は**カーソル**ない必要があり、既定では、sp_describe_cursor の呼び出し時にいない、カーソルに関連付けをします。 返されるカーソルのスクロール可能な動的、読み取り専用カーソルです。  
  
 [ @cursor_source=] {N'local' |N'global' |N'variable'}  
 ローカル カーソル、グローバル カーソル、またはカーソル変数の名前を使用して、レポート対象のカーソルが指定されているかどうかを指定します。 パラメーターが**nvarchar (30)** します。  
  
 [ @cursor_identity=] N'*local_cursor_name*']  
 LOCAL キーワードを持つか、またはローカルを既定値が設定は、DECLARE CURSOR ステートメントによって作成されたカーソルの名前です。 *local_cursor_name*は**nvarchar (128)** します。  
  
 [ @cursor_identity=] N'*global_cursor_name*']  
 GLOBAL キーワードを持つか、またはグローバルを既定値が設定は、DECLARE CURSOR ステートメントによって作成されたカーソルの名前です。 *global_cursor_name*は**nvarchar (128)** します。  
  
 *global_cursor_name*が指定する ODBC アプリケーションによって開かれた API サーバー カーソルの名前を指定できますも SQLSetCursorName を呼び出すことによって。  
  
 [ @cursor_identity=] N'*input_cursor_variable*']  
 開いているカーソルに関連付けられたカーソル変数の名前です。 *input_cursor_variable*は**nvarchar (128)** します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="cursors-returned"></a>返されるカーソル  
 sp_describe_cursor は、その結果セットをカプセル化、 [!INCLUDE[tsql](../../includes/tsql-md.md)] **カーソル**出力パラメーター。 これにより、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ、ストアド プロシージャ、および、一度に 1 行の出力の操作をトリガーします。 つまり、プロシージャは、データベース API 関数から直接呼び出すことができません。 **カーソル**出力パラメーターは、プログラム変数にバインドする必要がありますが、データベース Api は、バインディングをサポートしていない**カーソル**パラメーターまたは変数です。  
  
 次の表に、sp_describe_cursor が返すカーソルの形式を示します。 カーソルの形式は、sp_cursor_list を使用した場合に返される形式と同じです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|カーソルを参照するために使用される名前です。 DECLARE CURSOR ステートメントに指定された名前を介してカーソルを参照すると、参照名はカーソル名と同じになります。 変数を介してカーソルを参照場合、参照名は、変数の名前です。|  
|cursor_name|**sysname**|DECLARE CURSOR ステートメントのカーソルの名前です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、カーソルがカーソル変数を設定して作成されると、cursor_name にカーソル変数の名前が返されます。 以前のバージョンの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、この出力列は、システムによって生成された名前を返します。|  
|cursor_scope|**tinyint**|1 = LOCAL<br /><br /> 2 = GLOBAL|  
|status|**int**|CURSOR_STATUS システム関数によって報告された、同じ値:<br /><br /> 1 = カーソル名または変数によって参照されたカーソルは開いています。 カーソルが状態非依存、静的、キーセットのいずれかの場合には、結果セットに少なくとも 1 行が含まれます。 カーソルが動的の場合には、結果セットに 0 行以上が含まれます。<br /><br /> 0 = カーソル名または変数によって参照されたカーソルは開いていますが、行は含まれていません。 動的カーソルがこの値を返すことはありません。<br /><br /> -1 = カーソル名または変数によって参照されたカーソルは閉じています。<br /><br /> -2 = カーソル変数にのみ適用されます。 変数に割り当てられたカーソルはありません。 おそらく、OUTPUT パラメーターによってカーソルを変数に割り当てましたが、戻る前にストアド プロシージャがカーソルを閉じました。<br /><br /> -3 = 指定された名前のカーソルまたはカーソル変数が存在しないか、またはカーソル変数にカーソルが割り当てられていません。|  
|model|**tinyint**|1 = 状態非依存 (または静的)<br /><br /> 2 = キーセット<br /><br /> 3 = 動的<br /><br /> 4 = 高速順方向|  
|コンカレンシー|**tinyint**|1 = 読み取り専用<br /><br /> 2 = スクロール ロック<br /><br /> 3 = オプティミスティック|  
|scrollable|**tinyint**|0 = 順方向専用<br /><br /> 1 = スクロール可能|  
|open_status|**tinyint**|0 = 閉じた状態<br /><br /> 1 = 開いた状態|  
|cursor_rows|**decimal(10,0)**|結果セット内の行を限定の数。 詳細については、「[@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)」を参照してください。|  
|fetch_status|**smallint**|このカーソルの最後のフェッチの状態です。 詳細については、「[@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)」を参照してください。<br /><br /> 0 = フェッチが成功しました。<br /><br /> -1 = フェッチが失敗したか、またはカーソルの境界を越えています。<br /><br /> -2 = 要求された行がありません。<br /><br /> -9 = カーソル上でフェッチは行われていません。|  
|column_count|**smallint**|カーソル結果セット内の列の数。|  
|row_count|**decimal(10,0)**|カーソル上で最後の操作によって影響を受ける行の数。 詳細については、「[@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)」を参照してください。|  
|last_operation|**tinyint**|カーソル上で最後の操作を実行します。<br /><br /> 0 = カーソル上で操作は実行されていません。<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = 挿入<br /><br /> 4 = UPDATE<br /><br /> 5 = DELETE<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|サーバーのスコープ内でカーソルの一意の値。|  
  
## <a name="remarks"></a>コメント  
 sp_describe_cursor は、カーソルがスクロール可能かどうか、更新可能かどうかなど、サーバー カーソルのグローバルな属性を説明します。 カーソルによって返される結果セットの属性の説明については、sp_describe_cursor_columns を使用します。 カーソルが参照するベース テーブルのレポートが必要な場合は、sp_describe_cursor_tables を使用します。 接続時に可視になる [!INCLUDE[tsql](../../includes/tsql-md.md)] Server カーソルのレポートが必要な場合は、sp_cursor_list を使用します。  
  
 DECLARE CURSOR ステートメントをカーソルの種類を要求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DECLARE CURSOR に含まれている SELECT ステートメントの使用をサポートできません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カーソルを SELECT ステートメントを使用してサポートの種類に暗黙的に変換します。 DECLARE CURSOR ステートメントで TYPE_WARNING を指定した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]アプリケーションへの変換が完了したこと、情報メッセージを送信します。 sp_describe_cursor は、インプリメントされたカーソルの種類を判断しと呼ばれることができます。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、グローバル カーソルを開き、`sp_describe_cursor` を使用してカーソルの属性をレポートします。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR STATIC FOR  
SELECT LastName  
FROM Person.Person;  
  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor into the cursor variable.  
EXEC master.dbo.sp_describe_cursor @cursor_return = @Report OUTPUT,  
        @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [カーソル](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;TRANSACT-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [sp_describe_cursor_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  
