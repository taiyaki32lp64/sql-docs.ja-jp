---
title: APPLOCK_TEST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPLOCK_TEST_TSQL
- APPLOCK_TEST
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- APPLOCK_TEST function
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- testing application locks
ms.assetid: 4ea33d04-f8e9-46ff-ae61-985bd3eaca2c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f71a288994afb76d1237f303edfc926116f5962e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040336"
---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、ロックを取得せずに指定されたロック所有者の特定のアプリケーション リソースのロックを許可できるかどうかについての情報を返します。 APPLOCK_TEST はアプリケーション ロック関数であり、現在のデータベース上で動作します。 データベースはアプリケーション ロックのスコープです。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>引数  
**'** *database_principal* **'**  
データベース内のオブジェクトに対するアクセス許可を許可されるユーザー、ロール、またはアプリケーション ロールです。 関数を正常に呼び出すには、関数の呼び出し元が *database_principal*、dbo、または、db_owner 固定データベース ロールのメンバーである必要があります。
  
**'** *resource_name* **'**  
クライアント アプリケーションによって指定されたロック リソース名を指定します。 アプリケーション側では、リソース名が一意になるよう管理されている必要があります。 指定した名前は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロック マネージャーが内部的に保存できる値に内部的にハッシュされます。  *resource_name* は **nvarchar (255**) であり、既定値はありません。 *resource_name* はバイナリ比較し、現在のデータベースの照合順序の設定に関係なく大文字小文字を区別します。
  
**'** *lock_mode* **'**  
特定のリソースに対して取得するロック モード。 *lock_mode* は **nvarchar (32)** であり、既定値はありません。 *lock_mode* は、次のいずれかの値をとります:**Shared**、**Update**、**IntentShared**、**IntentExclusive**、**Exclusive**。
  
**'** *lock_owner* **'**  
ロックの所有者を指定します。これはロックが要求されたときの *lock_owner* 値です。 *lock_owner* は **nvarchar (32)** , 、値には、いずれかを指定して **トランザクション** (既定値) または **セッション**です。 既定値または **Transaction** を明示的に指定した場合、APPLOCK_TEST はトランザクション内から実行する必要があります。
  
## <a name="return-types"></a>戻り値の型
**smallint**
  
## <a name="return-value"></a>戻り値
指定された所有者にロックを許可できない場合は 0、ロックを許可できる場合は 1 です。
  
## <a name="function-properties"></a>関数のプロパティ
**非決定的**
  
**インデックス不可**
  
**並列不可**
  
## <a name="examples"></a>使用例  
セッションが異なる 2 つのユーザー (**ユーザー A** と**ユーザー B**) の次のシーケンスを実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントです。
  
**ユーザー A** が次のステートメントを実行します。
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
次に、**ユーザー B** が次のステートメントを実行します。
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
次に、**ユーザー A** が次のステートメントを実行します。
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
次に、**ユーザー B** が次のステートメントを実行します。
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
次に、**ユーザー A** と**ユーザー B** の両方が次のステートメントを実行します。
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>参照
[APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
