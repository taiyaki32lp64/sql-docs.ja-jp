---
title: DBCC HELP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC HELP
- DBCC_HELP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC statement syntax information
- DBCC HELP statement
ms.assetid: 306092c6-4354-4e47-928b-606124fbdc6e
author: pmasl
ms.author: umajay
ms.openlocfilehash: eaad7e6f3e66bb39ec43f402c531b7f89bdcf980
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251386"
---
# <a name="dbcc-help-transact-sql"></a>DBCC HELP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

指定された DBCC コマンドに関する構文情報を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC HELP ( 'dbcc_statement' | @dbcc_statement_var | '?' )  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
 *dbcc_statement* |  *\@dbcc_statement_var*  
 構文情報を取得する DBCC コマンドの名前を指定します。 DBCC コマンドの "DBCC" より後の部分のみを指定します (たとえば、DBCC CHECKDB ではなく CHECKDB と指定します)。  
  
 ?  
 ヘルプ情報を取得できるすべての DBCC コマンドを返します。  
  
 WITH NO_INFOMSGS  
 重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
## <a name="result-sets"></a>結果セット  
DBCC HELP は、指定された DBCC コマンドの構文を示す結果セットを返します。
  
## <a name="permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールのメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
### <a name="a-using-dbcc-help-with-a-variable"></a>A. DBCC HELP と変数  
次の例では、DBCC `CHECKDB` に関する構文情報を返します。
  
```sql  
DECLARE @dbcc_stmt sysname;  
SET @dbcc_stmt = 'CHECKDB';  
DBCC HELP (@dbcc_stmt);  
GO  
```  
  
### <a name="b-using-dbcc-help-with-the--option"></a>B. DBCC HELP と ? オプション  
次の例は、ヘルプ情報を取得できるすべての DBCC ステートメントを返します。
  
```sql  
DBCC HELP ('?');  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
