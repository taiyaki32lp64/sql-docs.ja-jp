---
title: sp_trace_generateevent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: cfeacf9f3c18d3f80b7ad83a3697e33a5797ba22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096026"
---
# <a name="sptracegenerateevent-transact-sql"></a>sp_trace_generateevent (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ユーザー定義イベントを作成します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
>**注:** このストアド プロシージャは**いない**非推奨とされます。 他のすべてのトレース関連のストアド プロシージャの使用は非推奨とされます。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>引数  
`[ @eventid = ] event_id` 有効にするイベントの ID です。 *event_id*は**int**、既定値はありません。 ID は、82 ~ 91 のセットとしてユーザー定義イベントを表すからのイベント番号のいずれかを指定する必要があります[sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)します。  
  
`[ @userinfo = ] 'user_info'` イベントの理由を特定する省略可能なユーザー定義の文字列です。 *user_info*は**nvarchar (128)** 、既定値は NULL です。  
  
`[ @userdata = ] user_data` イベントの省略可能なユーザー指定のデータです。 *user_data*は**varbinary (8000)** 、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|**0**|エラーなし。|  
|**1**|不明なエラー。|  
|**3**|指定したイベントが無効です。 イベントが存在しないか、ストアド プロシージャに対して適切なものではありません。|  
|**13**|メモリ不足。 指定したアクションを実行するための十分なメモリがない場合に返されます。|  
  
## <a name="remarks"></a>コメント  
 **sp_trace_generateevent**によって実行される操作の多くは、 **xp_trace _\*** 拡張ストアド プロシージャ。 使用**sp_trace_generateevent**の代わりに**この**します。  
  
 ユーザー定義イベントの ID 番号のみで使用できる**sp_trace_generateevent**します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で他のイベント ID 番号を使用すると、エラーが発生します。  
  
 パラメーターのすべての SQL トレース ストアド プロシージャ (**sp_trace_xx**) は厳密に型指定されます。 これらのパラメーターを、引数の説明で指定されている正しいデータ型で指定しないと、このストアド プロシージャではエラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER TRACE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、サンプル テーブルで、user configurable イベントを作成します。  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.fn_trace_geteventinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)  
  
  
