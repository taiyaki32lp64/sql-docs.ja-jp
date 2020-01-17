---
title: DBCC INPUTBUFFER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
author: pmasl
ms.author: umajay
ms.openlocfilehash: d0b6f9dac0cb065a9509040b5693b09b1fa9d5e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039099"
---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

クライアントから [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに最後に送信されたステートメントを表示します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
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
オプションを指定可能にします。  
  
NO_INFOMSGS  
重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
## <a name="result-sets"></a>結果セット  
DBCC INPUTBUFFER では、次の列を含む結果セットが返されます。
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar(30)**|イベントの種類。 **RPC Event** または **Language Event** になります。 前回のイベントが検出されなかった場合、出力は **No Event** になります。|  
|**パラメーター**|**smallint**|0 = テキスト<br /><br /> 1- *n* = パラメーター|  
|**EventInfo**|**nvarchar (4000)**|**EventType** が RPC の場合、**EventInfo** にはプロシージャ名だけが含まれます。 **EventType** が Language の場合は、イベントの最初の 4,000 文字だけが表示されます。|  
  
たとえば、DBCC INPUTBUFFER では、バッファー内の最後のイベントが DBCC INPUTBUFFER(11) である場合、次の結果セットが返されます。
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 以降の場合は、[sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに送信されたステートメントに関する情報を返します。

## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次のいずれかが必要です。
-   ユーザーは、**sysadmin** 固定サーバー ロールのメンバーである必要があります。  
-   ユーザーには VIEW SERVER STATE 権限が必要です。  
-   *session_id* は、コマンドが実行されるセッション ID と同じである必要があります。 セッション ID を特定するには、次のクエリを実行します。  
  
```sql
SELECT @@spid;  
```
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] の Premium 階層および Business Critical 階層では、データベースで VIEW DATABASE STATE アクセス許可が必要です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard、Basic、および General Purpose 階層の場合、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 管理者アカウントが必要です。
  
## <a name="examples"></a>使用例  
次の例では、前の接続で長いトランザクションが実行されている間に、2 番目の接続で `DBCC INPUTBUFFER` を実行します。
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  
