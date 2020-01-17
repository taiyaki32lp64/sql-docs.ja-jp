---
title: DBCC OUTPUTBUFFER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC OUTPUTBUFFER
- OUTPUTBUFFER_TSQL
- OUTPUTBUFFER
- DBCC_OUTPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC OUTPUTBUFFER statement
- output buffers
- current output buffer
ms.assetid: e912a06d-9fde-4e26-b057-801255d79504
author: pmasl
ms.author: umajay
ms.openlocfilehash: f35532913a21ed6f90d1e940dd6346137fc3feda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039087"
---
# <a name="dbcc-outputbuffer-transact-sql"></a>DBCC OUTPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

指定した *session_id* の現在の出力バッファーを、16 進形式と ASCII 形式で返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
```sql
DBCC OUTPUTBUFFER ( session_id [ , request_id ])  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
 *session_id*  
 アクティブな各プライマリ接続に関連付けられているセッション ID を指定します。  
  
 *request_id*  
 現在のセッション内で検索する具体的な要求 (バッチ) を指定します。  
 次のクエリは *request_id* を返します。  
  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
  
 WITH  
 オプションの指定を許可します。  
  
 NO_INFOMSGS  
 重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks  
DBCC OUTPUTBUFFER では、指定したクライアント (*session_id*) に送信された結果が表示されます。 ただし、出力ストリームを含まないプロセスでは、エラー メッセージが返されます。
  
DBCC OUTPUTBUFFER で表示される結果を返したステートメントを表示するには、DBCC INPUTBUFFER を実行します。
  
## <a name="result-sets"></a>結果セット  
DBCC OUTPUTBUFFER では次の結果セットが返されます (値は変わることがあります)。
  
```sql
Output Buffer                                                              
------------------------------------------------------------------------   
01fb8028:  04 00 01 5f 00 00 00 00 e3 1b 00 01 06 6d 00 61  ..._.........m.a  
01fb8038:  00 73 00 74 00 65 00 72 00 06 6d 00 61 00 73 00  .s.t.e.r..m.a.s.  
'...'  
01fb8218:  04 17 00 00 00 00 00 d1 04 18 00 00 00 00 00 d1  ................  
01fb8228:   .  
  
(33 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールのメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
次の例では、セッション ID が `52` の、現在の出力バッファー情報を返します。
  
```sql
DBCC OUTPUTBUFFER (52);  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
