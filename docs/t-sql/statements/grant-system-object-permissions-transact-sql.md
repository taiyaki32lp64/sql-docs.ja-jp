---
title: GRANT (システム オブジェクトの権限の許可) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], system objects
- system objects [SQL Server]
- GRANT statement, system objects
ms.assetid: 9d4e89f4-478f-419a-8b50-b096771e3880
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cd783ac6f5f6d8c7a9e561614dbe2c06053f758a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050671"
---
# <a name="grant-system-object-permissions-transact-sql"></a>GRANT (システム オブジェクトの権限の許可) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  システム ストアド プロシージャ、拡張ストアド プロシージャ、関数、ビューなどのシステム オブジェクトに対する権限を許可します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GRANT { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>引数  
 [ sys.] .  
 sys 修飾子は、カタログ ビューおよび動的カタログ ビューを指定する場合にのみ必要です。  
  
 *system_object*  
 権限を許可するオブジェクトを指定します。  
  
 *principal*  
 権限を許可するプリンシパルを指定します。  
  
## <a name="remarks"></a>Remarks  
 このステートメントを使用すると、特定のストアド プロシージャ、拡張ストアド プロシージャ、テーブル値関数、スカラー関数、ビュー、カタログ ビュー、互換ビュー、INFORMATION_SCHEMA ビュー、動的管理ビュー、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってインストールされたシステム テーブルに対する権限を許可できます。 これらのシステム オブジェクトはそれぞれ、サーバーのリソース データベース (mssqlsystemresource) に一意なレコードとして存在しています。 リソース データベースは読み取り専用です。 オブジェクトへのリンクは、各データベースの sys スキーマでは 1 レコードとして表されます。 システム オブジェクトを実行または選択する権限は、許可、拒否、および取り消しが可能です。  
  
 オブジェクトを実行または選択する権限を許可しても、そのオブジェクトの使用に必要なすべての権限が与えられるわけではありません。 ほとんどのオブジェクトでは、操作の実行に追加の権限が必要です。 たとえば、ユーザーに対して sp_addlinkedserver の EXECUTE 権限が許可されていても、sysadmin 固定サーバー ロールのメンバーでない限り、そのユーザーはリンク サーバーを作成できません。  
  
 既定の名前解決では、修飾子のないプロシージャ名はリソース データベースとして解釈されます。 したがって、sys 修飾子は、カタログ ビューおよび動的カタログ ビューを指定する場合にのみ必要です。  
  
 システム オブジェクトのトリガーおよび列に対する権限の許可はサポートされていません。  
  
 システム オブジェクトの権限は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレード時も維持されます。  
  
 システム オブジェクトは、 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) カタログ ビューで確認できます。 システム オブジェクトの権限は、master データベースの [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) カタログ ビューで確認できます。  
  
 次のクエリでは、システム オブジェクトの権限に関する情報が返されます。  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-granting-select-permission-on-a-view"></a>A. ビューに対する SELECT 権限を許可する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの一覧を表示するビューを選択する権限を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `Sylvester1` に許可します。 その後、ユーザーが所有していない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインでメタデータを表示するために必要な追加権限を許可します。  
  
```  
USE AdventureWorks2012;  
GRANT SELECT ON sys.sql_logins TO Sylvester1;  
GRANT VIEW SERVER STATE to Sylvester1;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-an-extended-stored-procedure"></a>B. 拡張ストアド プロシージャに対する EXECUTE 権限を許可する  
 次の例では、`Sylvester1` に対し、`xp_readmail` の `EXECUTE` 権限を許可します。  
  
```  
GRANT EXECUTE ON xp_readmail TO Sylvester1;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [REVOKE (システム オブジェクトの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)   
 [DENY (システム オブジェクトの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
