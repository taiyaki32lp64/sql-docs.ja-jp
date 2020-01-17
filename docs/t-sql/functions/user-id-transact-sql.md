---
title: USER_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USER_ID
- USER_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- USER_ID function
- identification numbers [SQL Server]
- IDs [SQL Server], databases
- users [SQL Server], database ID numbers
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
ms.assetid: 67fd29bc-eda9-4d4d-b148-5d3659181a43
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1b8b1b0b5a9254382490272bd92405f52ed90a3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927605"
---
# <a name="userid-transact-sql"></a>USER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベース ユーザーの ID 番号を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して [DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md) 代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>引数  
 *user*  
 使用するユーザー名を指定します。 *ユーザー* は **nchar**です。 場合、 **char** 値を指定すると、暗黙的に変換されます **nchar**です。 かっこが必要です。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 ときに *ユーザー* は省略すると、現在のユーザーと見なされます。 パラメーターに NULL が含まれていると、NULL が返されます。EXECUTE AS の後で USER_ID が呼び出されると、USER_ID は権限を借用したコンテキストの ID を返します。  
  
 特定のデータベース ユーザーにマップされない Windows プリンシパルがグループのメンバーシップでデータベースにアクセスした場合、USER_ID では 0 (public の ID) が返されます。 このプリンシパルがスキーマを指定せずにオブジェクトを作成した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では Windows プリンシパルにマップされた暗黙のユーザーとスキーマが作成されます。 このときに作成されたユーザーを使用して、データベースに接続することはできません。 暗黙のユーザーにマップされた Windows プリンシパルが USER_ID を呼び出すと、暗黙のユーザーの ID が返されます。  
  
 USER_ID は、選択リストの中、WHERE 句の中、また式を使える所ならどこにでも使用できます。 詳細については、「[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、`AdventureWorks2012` ユーザー `Harold` の ID 番号が返されます。  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID &#40;Transact-SQL&#41;](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
