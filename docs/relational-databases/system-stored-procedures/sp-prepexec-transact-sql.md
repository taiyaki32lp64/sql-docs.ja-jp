---
title: sp_prepexec (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
author: stevestein
ms.author: sstein
ms.openlocfilehash: 670b64cb107610fe8b5506654b9e655b0da5fb16
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794716"
---
# <a name="sp_prepexec-transact-sql"></a>sp_prepexec (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パラメーター化[!INCLUDE[tsql](../../includes/tsql-md.md)]されたステートメントを準備して実行します。 sp_prepexec は、sp_prepare と sp_execute の関数を組み合わせたものです。 このアクションは、ID = 13 によって表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>引数  
 *handle*  
 生成されたハンドル識別子です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *handle*は、 **int**戻り値を持つ必須パラメーターです。  
  
 *params*  
 パラメーター化されたステートメントを指定します。 変数の*params*定義は、ステートメントのパラメーターマーカーに置き換えられます。 *params*は、 **ntext**、 **nchar**、または**nvarchar**の入力値を呼び出す必須のパラメーターです。 ステートメントがパラメーター化されていない場合は、NULL 値を入力します。  
  
 *stmt*  
 カーソル結果セットを定義します。 *Stmt*パラメーターは必須であり、 **ntext**、 **nchar**、または**nvarchar**の入力値に対してを呼び出します。  
  
 *bound_param*  
 追加パラメーターをオプションで使用することを示します。 *bound_param*は、使用する追加パラメーターを指定するために、任意のデータ型の入力値を呼び出します。  
  
## <a name="examples"></a>使用例  
 次の例では、単純なステートメントを準備して実行します。  
  
```  
Declare @Out int;  
EXEC sp_prepexec @Out output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
          @P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @Out;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_execute &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
