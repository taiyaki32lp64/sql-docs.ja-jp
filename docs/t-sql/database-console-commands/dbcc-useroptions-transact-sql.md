---
title: DBCC USEROPTIONS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC USEROPTIONS
- DBCC_USEROPTIONS_TSQL
- USEROPTIONS_TSQL
- USEROPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC USEROPTIONS statement
- active SET options
- SET statement, active SET options
ms.assetid: 565ab112-7af1-4c18-a579-07cdb332f539
author: pmasl
ms.author: umajay
ms.openlocfilehash: dc8f12ae745acd0410fb309dc4c3dc9b65e7a382
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040449"
---
# <a name="dbcc-useroptions-transact-sql"></a>DBCC USEROPTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

現在の接続でアクティブになっている (設定されている) SET オプションを返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC USEROPTIONS  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
NO_INFOMSGS  
重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。
  
## <a name="result-sets"></a>結果セット  
DBCC USEROPTIONS は、SET オプションの名前の列とオプションの値の列を返します (値とエントリは状況に応じて異なります)。

```sql

Set Option                   Value`  
---------------------------- ---------------------------`  
textsize                     64512 
language                     us_english 
dateformat                   mdy  
datefirst                    7 
lock_timeout                 -1 
quoted_identifier            SET 
arithabort                   SET 
ansi_null_dflt_on            SET 
ansi_warnings                SET 
ansi_padding                 SET 
ansi_nulls                   SET 
concat_null_yields_null      SET 
isolation level              read committed  
(13 row(s) affected) 
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```  
  
## <a name="remarks"></a>Remarks  
READ_COMMITTED_SNAPSHOT データベース オプションが ON に設定され、トランザクション分離レベルが "READ COMMITTED" に設定されている場合、DBCC USEROPTIONS は、"READ COMMITTED スナップショット" の分離レベルを報告します。 実際の分離レベルは READ COMMITTED です。
  
## <a name="permissions"></a>アクセス許可  
ロール **public** のメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
次の例は、現在の接続のアクティブな SET オプションを返します。
  
```sql  
DBCC USEROPTIONS;  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
  
  
