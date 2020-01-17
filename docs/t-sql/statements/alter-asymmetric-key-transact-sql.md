---
title: ALTER ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.date: 04/12/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ASYMMETRIC_KEY_TSQL
- ALTER ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- passwords [SQL Server], asymmetric keys
- encryption [SQL Server], asymmetric keys
- DECRYPTION BY PASSWORD option
- ALTER ASYMMETRIC KEY statement
- asymmetric keys [SQL Server], modifying
ms.assetid: 958e95d6-fbe6-43e8-abbd-ccedbac2dbac
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 06263499babe005bca36a982bc863dfa24356b5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066072"
---
# <a name="alter-asymmetric-key-transact-sql"></a>ALTER ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  非対称キーのプロパティを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ALTER ASYMMETRIC KEY Asym_Key_Name <alter_option>  
  
<alter_option> ::=  
      <password_change_option>   
    | REMOVE PRIVATE KEY   

<password_change_option> ::=  
    WITH PRIVATE KEY ( <password_option> [ , <password_option> ] )  

<password_option> ::=  
      ENCRYPTION BY PASSWORD = 'strongPassword'  
    | DECRYPTION BY PASSWORD = 'oldPassword'  
```  
  
## <a name="arguments"></a>引数  
 *Asym_Key_Name*  
 データベースで認識される非対称キーの名前を指定します。  
  
 REMOVE PRIVATE KEY  
 非対称キーから秘密キーを削除します。公開キーは削除されません。  
  
 WITH PRIVATE KEY  
 秘密キーの保護を変更します。  
  
 ENCRYPTION BY PASSWORD **='***strongPassword***'**  
 秘密キーを保護するための新しいパスワードを指定します。 *password* は、Windows のパスワード ポリシーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行するコンピューターに要求する条件を満足する必要があります。 このオプションを省略した場合、秘密キーはデータベースのマスター キーで暗号化されます。  
  
 DECRYPTION BY PASSWORD **='***oldPassword***'**  
 現在秘密キーが保護されている、古いパスワードを指定します。 秘密キーがデータベースのマスター キーで暗号化されている場合は指定する必要はありません。  
  
## <a name="remarks"></a>Remarks  
 データベースのマスター キーがない場合は、ENCRYPTION BY PASSWORD オプションを指定する必要があります。パスワードを指定しないと、この操作は失敗します。 データベースのマスター キー作成方法については、「[CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)」をご覧ください。  
  
 秘密キーの保護を変更するには、ALTER ASYMMETRIC KEY を使用して、PRIVATE KEY オプションを次のように指定します。  
  
|保護の変更対象|ENCRYPTION BY PASSWORD|DECRYPTION BY PASSWORD|  
|----------------------------|----------------------------|----------------------------|  
|古いパスワードから新しいパスワードへ|Required|Required|  
|パスワードからマスター キーへ|[省略]|Required|  
|マスター キーからパスワードへ|Required|[省略]|  
  
 データベースのマスター キーを秘密キーの保護に使用するには、マスター キーを先に開いておく必要があります。 詳しくは、「[OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)」をご覧ください。  
  
 非対称キーの所有権を変更するには、[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 秘密キーを削除する場合、非対称キーに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-password-of-the-private-key"></a>A. 秘密キーのパスワードを変更する  
 次の例では、非対称キー `PacificSales09` の秘密キーの保護に使用するパスワードを変更します。 新しいパスワードは `<enterStrongPasswordHere>` です。  
  
```  
ALTER ASYMMETRIC KEY PacificSales09   
    WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<oldPassword>',  
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>');  
GO  
```  
  
### <a name="b-removing-the-private-key-from-an-asymmetric-key"></a>B. 非対称キーから秘密キーを削除する  
 次の例では、`PacificSales19` から秘密キーを削除し、公開キーだけを残します。  
  
```  
ALTER ASYMMETRIC KEY PacificSales19 REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="c-removing-password-protection-from-a-private-key"></a>C. 秘密キーからパスワード保護を削除する  
 次の例では、秘密キーからパスワード保護を削除し、データベースのマスター キーで保護します。  
  
```  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<database master key password>';  
ALTER ASYMMETRIC KEY PacificSales09 WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<enterStrongPasswordHere>' );  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
