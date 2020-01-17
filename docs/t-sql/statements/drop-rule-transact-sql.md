---
title: DROP RULE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_RULE_TSQL
- DROP RULE
dev_langs:
- TSQL
helpviewer_keywords:
- rules [SQL Server], removing
- deleting roles
- DROP RULE statement
- removing roles
- dropping roles
ms.assetid: 8370b730-7fd5-43fe-a7f6-8300b3caa16d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cce8533a1ac74feb95577d28f73cb6f87c15aa31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223600"
---
# <a name="drop-rule-transact-sql"></a>DROP RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つ以上のユーザー定義のルールを現在のデータベースから削除します。  
  
> [!IMPORTANT]
>  DROP RULE は、次期バージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定です。 新しい開発作業では、DROP RULE の使用は避け、現在このオプションを使用しているアプリケーションは修正するようにしてください。 代わりに、[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) または [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) の CHECK キーワードを使用して作成できる CHECK 制約を使用してください。 詳細については、「 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DROP RULE [ IF EXISTS ] { [ schema_name . ] rule_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 条件付きでは既に存在する場合にのみ、ルールを削除します。  
  
 *schema_name*  
 ルールが属しているスキーマの名前を指定します。  
  
 *rule*  
 削除するルールです。 ルール名は、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 ルールのスキーマ名の指定は省略可能です。  
  
## <a name="remarks"></a>Remarks  
 ルールを削除するには、そのルールが列または別名データ型に現在バインドされている場合、まず、このバインドを解除します。 ルールのバインドを解除するには、**sp_unbindrule** を使います。 バインドされているルールを削除しようとすると、エラー メッセージが表示され、DROP RULE ステートメントは取り消されます。  
  
 ルールを削除すると、以前はそのルールに制御されていた列に新しいデータを入力しても、ルールの制約を受けなくなります。 既存のデータはまったく影響を受けません。  
  
 DROP RULE ステートメントは、CHECK 制約には適用されません。 CHECK 制約の削除について詳しくは、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 DROP RULE を実行するには、少なくとも、ルールが属するスキーマに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`VendorID_rule` というルールのバインドを解除し、削除します。 
  
```  
sp_unbindrule 'Production.ProductVendor.VendorID'  
DROP RULE VendorID_rule  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  

