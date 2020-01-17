---
title: SET CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_CONTEXT_INFO_TSQL
- SET CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- context information [SQL Server]
- CONTEXT_INFO option
- SET CONTEXT_INFO statement
ms.assetid: a0b7b9f3-dbda-4350-a274-bd9ecd5c0a74
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 79fc54e65b6e014575b5942a573c4077e8a9c5d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041810"
---
# <a name="set-contextinfo-transact-sql"></a>SET CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  128 バイト以内のバイナリ情報を現在のセッションまたは接続に関連付けます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET CONTEXT_INFO { binary_str | @binary_var }  
```  
  
## <a name="arguments"></a>引数  
 *binary_str*  
 現在のセッションまたは接続に関連付ける、**binary** 定数、または暗黙的に **binary** に変換できる定数を指定します。  
  
 **@** *binary_var*  
 現在のセッションまたは接続に関連付けるコンテキスト値を保持するための、**varbinary** または **binary** 変数を指定します。  
  
## <a name="remarks"></a>Remarks  
 現在のセッションのコンテキスト情報を取得するには、CONTEXT_INFO 関数を使用することをお勧めします。 セッションのコンテキスト情報は、次のシステム ビューの **context_info** 列にも格納されます。  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 SET CONTEXT_INFO は、ユーザー定義関数では指定できません。 値を保持するビューでは NULL 値が許可されないため、SET CONTEXT_INFO に NULL 値は指定できません。  
  
 SET CONTEXT_INFO には、定数または変数名以外の式を指定できません。 コンテキスト情報を関数呼び出しの結果に設定するには、最初に、**binary** または **varbinary** 型の変数に関数呼び出しの結果を格納する必要があります。  
  
 ストアド プロシージャまたはトリガーの中で SET CONTEXT_INFO を実行する場合は、他の SET ステートメントの場合とは異なり、コンテキスト情報に設定された新しい値がストアド プロシージャまたはトリガーの終了後も保持されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-setting-context-information-by-using-a-constant"></a>A. 定数を使用してコンテキスト情報を設定する  
 次の例では、`SET CONTEXT_INFO` に値を設定し、結果を表示します。 `sys.dm_exec_sessions` のクエリを実行するには SELECT および VIEW SERVER STATE の権限が必要ですが、CONTEXT_INFO 関数を使用するのにこれらの権限は必要ありません。  
  
```  
SET CONTEXT_INFO 0x01010101;  
GO  
SELECT context_info   
FROM sys.dm_exec_sessions  
WHERE session_id = @@SPID;  
GO  
```  
  
### <a name="b-setting-context-information-by-using-a-function"></a>B. 関数を使用してコンテキスト情報を設定する  
 次の例では、関数の出力を使用してコンテキスト値を設定します。最初に、**binary** 変数に関数からの値を格納する必要があります。  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  
