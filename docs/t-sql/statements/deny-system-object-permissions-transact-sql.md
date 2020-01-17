---
title: DENY (システム オブジェクトの権限の拒否) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, system objects
- encryption [SQL Server], system objects
- system objects [SQL Server]
- cryptography [SQL Server], system objects
ms.assetid: 4e43f954-0982-470b-a239-08a13c61563a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54959f89172d0d382c20c60d46dac11df5837137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984411"
---
# <a name="deny-system-object-permissions-transact-sql"></a>DENY (システム オブジェクトの権限の拒否) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ストアド プロシージャ、拡張ストアド プロシージャ、関数、ビューなどのシステム オブジェクトに対する権限を拒否します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DENY { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>引数  
 **[sys.]**  
 **sys** 修飾子は、カタログ ビューおよび動的カタログ ビューを指定する場合にのみ必要です。  
  
 *system_object*  
 権限を拒否するオブジェクトを指定します。  
  
 *principal*  
 権限を取り消すプリンシパルを指定します。  
  
## <a name="remarks"></a>Remarks  
 このステートメントを使用すると、特定のストアド プロシージャ、拡張ストアド プロシージャ、テーブル値関数、スカラー関数、ビュー、カタログ ビュー、互換ビュー、INFORMATION_SCHEMA ビュー、動的管理ビュー、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってインストールされたシステム テーブルに対する権限を拒否できます。 これらのシステム オブジェクトはそれぞれ、リソース データベース (**mssqlsystemresource**) に一意なレコードとして存在しています。 リソース データベースは読み取り専用です。 オブジェクトへのリンクは、各データベースの **sys** スキーマでは 1 レコードとして表されます。  
  
 既定の名前解決では、修飾子のないプロシージャ名はリソース データベースとして解釈されます。 したがって、**sys** 修飾子は、カタログ ビューおよび動的カタログ ビューを指定する場合にのみ必要です。  
  
> [!CAUTION]  
>  システム オブジェクトに対する権限を拒否すると、そのシステム オブジェクトに依存するアプリケーションは失敗します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ではカタログ ビューが使用されており、カタログ ビューの既定の権限を変更すると、正常に機能しなくなることがあります。  
  
 システム オブジェクトのトリガーおよび列に対する権限の拒否はサポートされていません。  
  
 システム オブジェクトの権限は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレード時も維持されます。  
  
 システム オブジェクトは、 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) カタログ ビューで確認できます。 システム オブジェクトの権限は、 [master](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) データベースの **sys.database_permissions** カタログ ビューで確認できます。  
  
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
 次の例では、`public` に対し、`xp_cmdshell` の `EXECUTE` 権限を拒否します。  
  
```  
DENY EXECUTE ON sys.xp_cmdshell TO public;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [GRANT (システム オブジェクトの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [REVOKE (システム オブジェクトの権限の取り消し) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)  
  
  
