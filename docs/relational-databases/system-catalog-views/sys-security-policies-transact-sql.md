---
title: sys.security_policies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SECURITY_POLICIES_TSQL
- SECURITY_POLICIES_TSQL
- SYS.SECURITY_POLICIES
- SECURITY_POLICIES
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_policies catalog view
- security_policies catalog view
ms.assetid: 35362f5b-e601-4049-9e1d-c5307e823831
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d6eec5c523e2bdd321af145f19d0b5e7e7cba39b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135309"
---
# <a name="syssecuritypolicies-transact-sql"></a>sys.security_policies (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  データベース内には、セキュリティ ポリシーごとに行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|セキュリティ ポリシーの名前。データベース内で一意です。|  
|object_id|**int**|セキュリティ ポリシーの ID。|  
|principal_id|**int**|データベースに登録したセキュリティ ポリシーの所有者の ID。 スキーマを使用して所有者が特定された場合は NULL です。|  
|schema_id|**int**|オブジェクトが存在するスキーマの ID。|  
|parent_object_id|**int**|ポリシーが所属するオブジェクトの ID。 0 を指定する必要があります。|  
|type|**vachar(2)**|**SP** を指定する必要があります。|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**します。|  
|create_date|**datetime**|セキュリティ ポリシーが作成された UTC 日付。|  
|modify_date|**datetime**|セキュリティ ポリシーが最後に変更された UTC 日付。|  
|is_ms_shipped|**bit**|常に false です。|  
|is_enabled|**bit**|セキュリティ ポリシー指定状態:<br /><br /> 0 = 無効になっています<br /><br /> 1 = 有効になっています。|  
|is_not_for_replication|**bit**|NOT FOR REPLICATION オプションを指定して作成されたポリシーです。|  
|uses_database_collation|**bit**|データベースと同じ照合順序を使用します。|  
|is_schemabinding_enabled|**bit**|セキュリティ ポリシーの Schemabinding の状態:<br /><br /> 0 または NULL = 有効になっています。<br /><br /> 1 = 無効|  
  
## <a name="permissions"></a>アクセス許可  
 持つプリンシパル、 **ALTER ANY SECURITY POLICY**アクセス許可がある、すべてのユーザーをこのカタログ ビューのすべてのオブジェクトへのアクセス**VIEW DEFINITION**オブジェクト。  
  
## <a name="see-also"></a>参照  
 [行レベルのセキュリティ](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
