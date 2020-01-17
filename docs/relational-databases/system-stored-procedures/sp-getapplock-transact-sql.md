---
title: sp_getapplock (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_getapplock_TSQL
- sp_getapplock
dev_langs:
- TSQL
helpviewer_keywords:
- application locks
- sp_getapplock
ms.assetid: e1e85908-9f31-47cf-8af6-88c77e6f24c9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fee963f1b026090a84e58a9b0844fe040f9e9793
ms.sourcegitcommit: d0e5543e8ebf8627eebdfd1e281adb47d6cc2084
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72717258"
---
# <a name="sp_getapplock-transact-sql"></a>sp_getapplock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  アプリケーションリソースのロックを配置します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_getapplock [ @Resource = ] 'resource_name' ,  
     [ @LockMode = ] 'lock_mode'   
     [ , [ @LockOwner = ] 'lock_owner' ]   
     [ , [ @LockTimeout = ] 'value' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 [@Resource=]'*resource_name*'  
 ロックリソースを識別する名前を指定する文字列です。 アプリケーション側では、リソース名が一意になるよう管理されている必要があります。 指定した名前は内部的にハッシュされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロック マネージャーに格納できる値に変換されます。 *resource_name*は**nvarchar (255)** で、既定値はありません。 リソース文字列が**nvarchar (255)** を超える場合、 **nvarchar (255)** に切り捨てられます。  
  
 *resource_name*はバイナリ比較されます。したがって、現在のデータベースの照合順序の設定に関係なく、大文字と小文字が区別されます。  
  
> [!NOTE]  
>  アプリケーション ロックが取得されると、プレーン テキストで抽出できるのは最初の 32 文字のみとなり、残りの部分はハッシュされます。  
  
 [@LockMode=]'*lock_mode*'  
 特定のリソースに対して取得されるロックモードを指定します。 *lock_mode* は **nvarchar (32)** 、既定値はありません。 値には、 **Shared**、 **Update**、 **intentshared**、 **intentshared**、または**exclusive**を指定できます。 詳細については、「[ロックモード](../sql-server-transaction-locking-and-row-versioning-guide.md#lock_modes)」を参照してください。
  
 [@LockOwner=]'*lock_owner*'  
 ロックの所有者を指定します。これはロックが要求されたときの *lock_owner* 値です。 *lock_owner* は **nvarchar (32)** です。 この値は **Transaction** (既定値) または **Session** のいずれかです。 *Lock_owner*値が**transaction**、既定で、または明示的に指定されている場合、sp_getapplock はトランザクション内から実行する必要があります。  
  
 [@LockTimeout=]'*value*'  
 ロックのタイムアウト値をミリ秒単位で指定します。 既定値は、@@LOCK_TIMEOUTによって返される値と同じです。 ロック要求がすぐに許可されない場合に、ロックを待機するのではなく-1 のリターンコードを返す必要があることを示すには、0を指定します。  
  
 [@DbPrincipal=]'*database_principal*'  
 データベース内のオブジェクトに対する権限を持つユーザー、ロール、またはアプリケーションロールを設定します。 関数を正常に呼び出すには、関数の呼び出し元が*database_principal*、dbo、または db_owner 固定データベースロールのメンバーである必要があります。 既定値は public です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 \>= 0 (成功)、または < 0 (失敗)  
  
|ReplTest1|結果|  
|-----------|------------|  
|0|ロックが同時に許可されました。|  
|@shouldalert|互換性のない他のロックが解放されるのを待機してから、ロックが許可されました。|  
|-1|ロック要求がタイムアウトしました。|  
|-2|ロック要求が取り消されました。|  
|-3|ロック要求がデッドロックの対象になりました。|  
|-999|パラメーターの検証またはその他の呼び出しエラーを示します。|  
  
## <a name="remarks"></a>Remarks  
 リソースに配置されたロックは、現在のトランザクションまたは現在のセッションのいずれかに関連付けられます。 現在のトランザクションに関連付けられたロックは、トランザクションがコミットまたはロールバックされるときに解放されます。 セッションに関連付けられているロックは、セッションがログアウトされると解放されます。何らかの理由でサーバーがシャットダウンすると、すべてのロックが解放されます。  
  
 Sp_getapplock によって作成されたロックリソースは、セッションの現在のデータベースに作成されます。 各ロックリソースは、の結合された値によって識別されます。  
  
-   ロックリソースが格納されているデータベースのデータベース ID。  
  
-   @DbPrincipal パラメーターで指定されるデータベース プリンシパル  
  
-   @Resource パラメーターで指定されたロック名。  
  
 @DbPrincipal パラメーターで指定されるデータベース プリンシパルのメンバーだけが、そのプリンシパルを指定しているアプリケーション ロックを取得できます。 Dbo ロールと db_owner ロールのメンバーは、暗黙的にすべてのロールのメンバーと見なされます。  
  
 ロックは、sp_releaseapplock で明示的に解放できます。 アプリケーションで、同じロック リソースに対して sp_getapplock が複数回呼び出される場合は、同じ回数だけ sp_releaseapplock を呼び出して、ロックを解放する必要があります。  ロック所有者 `Transaction` によってロックが開かれると、トランザクションがコミットまたはロールバックされるときに、そのロックが解放されます。
  
 sp_getapplock が同じロック リソースに対して複数回呼び出されても、その要求で指定されるロック モードが既存のモードと異なる場合、リソースでは 2 つのロック モードが混在することになります。 このため、ロック モードは多くの場合、既存のモードと新しく要求されたモードのうち、より強力なモードに昇格します。 この強力なロック モードは、その時点より前にロックの解放呼び出しが行われた場合でも、ロックが最終的に解放されるまで保持されます。 たとえば、次の一連の呼び出しでは、リソースは `Shared` モードではなく `Exclusive` モードで保持されます。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
EXEC @result = sp_releaseapplock @Resource = 'Form1';  
COMMIT TRANSACTION;  
GO  
```  
  
 アプリケーション ロック時にデッドロックが発生すると、アプリケーション ロックを要求したトランザクションはロールバックされません。 戻り値の結果として必要になる可能性のあるロールバックは、手動で行う必要があります。 したがって、ある特定の値 (たとえば -3) が返された場合に ROLLBACK TRANSACTION または代替の操作が開始できるように、コードにはエラー チェックを含めることをお勧めします。  
  
 以下に例を示します。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
IF @result = -3  
BEGIN  
    ROLLBACK TRANSACTION;  
END  
ELSE  
BEGIN  
    EXEC @result = sp_releaseapplock @Resource = 'Form1';  
    COMMIT TRANSACTION;  
END;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、現在のデータベース ID によってリソースが限定されます。 したがって、異なるデータベース上で同じパラメーター値を使用していても sp_getapplock が実行された場合、結果は個別のリソースに対して個別にロックされます。  
  
 sys.dm_tran_locks 動的管理ビューまたは sp_lock システム ストアド プロシージャを使ってロック情報を検証するか、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使ってロックを監視してください。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、現在のトランザクションに関連付けられている共有ロックを、`Form1` データベースのリソース `AdventureWorks2012` に設定します。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
 次の例では、データベースプリンシパルとして `dbo` を指定します。  
  
```  
BEGIN TRAN;  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'AdventureWorks2012',   
     @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql &#40;  の&#41; APPLOCK_MODE](../../t-sql/functions/applock-mode-transact-sql.md)  
 [Transact-sql &#40;  の&#41; APPLOCK_TEST](../../t-sql/functions/applock-test-transact-sql.md)  
 [sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)  
  
  
