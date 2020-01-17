---
title: REVOKE (システム オブジェクトの権限の取り消し) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, system objects
- permissions [SQL Server], system objects
ms.assetid: 84983238-dd7d-45bd-99bb-52c9d8e96a87
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 47428ffc2ab1074ec2b4ce1789e679c184607a05
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914200"
---
# <a name="revoke-system-object-permissions-transact-sql"></a>REVOKE (システム オブジェクトの権限の取り消し) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ストアド プロシージャ、拡張ストアド プロシージャ、関数、ビューなどのシステム オブジェクトに対する権限が、プリンシパルから取り消されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVOKE { SELECT | EXECUTE } ON [sys.]system_object FROM principal   
```  
  
## <a name="arguments"></a>引数  
 **[sys.]** .  
 **sys** 修飾子は、カタログ ビューおよび動的カタログ ビューを指定する場合にのみ必要です。  
  
 *system_object*  
 権限を取り消すオブジェクトが指定されます。  
  
 *principal*  
 権限を取り消すプリンシパルを指定します。  
  
## <a name="remarks"></a>Remarks  
 このステートメントを使用すると、特定のストアド プロシージャ、拡張ストアド プロシージャ、テーブル値関数、スカラー関数、ビュー、カタログ ビュー、互換ビュー、INFORMATION_SCHEMA ビュー、動的管理ビュー、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってインストールされたシステム テーブルに対する権限を取り消すことができます。 これらのシステム オブジェクトはそれぞれ、リソース データベース (**mssqlsystemresource**) に一意なレコードとして存在しています。 リソース データベースは読み取り専用です。 オブジェクトへのリンクは、各データベースの **sys** スキーマでは 1 レコードとして表されます。  
  
 既定の名前解決では、修飾子のないプロシージャ名はリソース データベースとして解釈されます。 したがって、**sys.** 修飾子は、カタログ ビューおよび動的カタログ ビューを指定する場合にのみ必要です。  
  
> [!CAUTION]  
>  システム オブジェクトに対する権限を取り消すと、そのシステム オブジェクトに依存するアプリケーションは失敗します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ではカタログ ビューが使用されており、カタログ ビューの既定の権限を変更すると、正常に機能しなくなることがあります。  
  
 システム オブジェクトのトリガーおよび列に対する権限の取り消しはサポートされていません。  
  
 システム オブジェクトの権限は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレード時も維持されます。  
  
 システム オブジェクトは、 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) カタログ ビューで確認できます。  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`sp_addlinkedserver` に対する `EXECUTE` 権限を、`public` から取り消します。  
  
```  
REVOKE EXECUTE ON sys.sp_addlinkedserver FROM public;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [GRANT (システム オブジェクトの権限の許可) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [DENY (システム オブジェクトの権限の拒否) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
