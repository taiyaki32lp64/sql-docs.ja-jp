---
title: DROP ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ASYMMETRIC KEY
- DROP_ASYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], removing
- removing asymmetric keys
- encryption [SQL Server], asymmetric keys
- DROP ASYMMETRIC KEY statement
- dropping asymmetric keys
- deleting asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: bf94ac07-9b62-4318-b55b-1eed8f3a1ac6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fdc08d0598209e3d5fa4957ca241bfa49c60b6a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898307"
---
# <a name="drop-asymmetric-key-transact-sql"></a>DROP ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベースから非対称キーを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP ASYMMETRIC KEY key_name [ REMOVE PROVIDER KEY ]  
```  
  
## <a name="arguments"></a>引数  
 *key_name*  
 データベースから削除する非対称キーの名前を指定します。  
  
 REMOVE PROVIDER KEY  
 EKM デバイスから拡張キー管理 (EKM) を削除します。 拡張キー管理について詳しくは、「[拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 データベース内の対称キーが非対称キーで暗号化されている場合、またはユーザーやログインが非対称キーにマップされる場合、非対称キーは削除できません。 このようなキーを削除するには、そのキーにマップされるユーザーまたはログインを削除する必要があります。 また、その非対称キーで暗号化されているすべての対称キーを削除または変更する必要があります。 非対称キーによる暗号化を削除するには、[ALTER SYMMETRIC KEY](../../t-sql/statements/alter-symmetric-key-transact-sql.md) の DROP ENCRYPTION オプションを使います。  
  
 非対称キーのメタデータには、[sys.asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md) カタログ ビューを使うことによってアクセスできます。 非対称キー自体を、データベース内部から直接表示することはできません。  
  
 非対称キーが EKM デバイスの拡張キー管理 (EKM) にマップされており、REMOVE PROVIDER KEY オプションが指定されていない場合は、キーはデータベースから削除されますが、デバイスからは削除されません。 この場合、警告が発行されます。  
  
## <a name="permissions"></a>アクセス許可  
 非対称キーに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、非対称キー `MirandaXAsymKey6` をデータベース `AdventureWorks2012` から削除します。  
  
```  
USE AdventureWorks2012;  
DROP ASYMMETRIC KEY MirandaXAsymKey6;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)  
  
  
