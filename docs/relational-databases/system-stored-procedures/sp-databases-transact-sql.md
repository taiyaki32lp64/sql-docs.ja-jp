---
title: sp_databases (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
author: stevestein
ms.author: sstein
ms.openlocfilehash: c338fb8057c2d58727f18e0bb69e2fa825e71559
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108332"
---
# <a name="spdatabases-transact-sql"></a>sp_databases (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インスタンス内に存在しているデータベースの一覧、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]またはデータベース ゲートウェイを介して外部からアクセスします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|データベースの名前です。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に格納されている、この列はデータベース名を表す、 **sys.databases**カタログ ビューです。|  
|**DATABASE_SIZE**|**int**|キロバイト単位でのデータベースのサイズ。|  
|**「解説」**|**varchar(254)**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]、このフィールドは常に NULL を返します。|  
  
## <a name="remarks"></a>コメント  
 返されるデータベース名は、現在のデータベース状況を変更するために USE ステートメントでパラメーターとして使えます。  
  
 **sp_databases**を持たないと同等で開いているデータベースの接続 (ODBC)。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE DATABASE、または ALTER ANY DATABASE、または VIEW ANY DEFINITION アクセス許可が必要ですし、データベースへのアクセス許可が必要です。 VIEW ANY DEFINITION 権限を拒否できません。  
  
## <a name="examples"></a>使用例  
 次の例を実行する`sp_databases`します。  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;TRANSACT-SQL&#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
