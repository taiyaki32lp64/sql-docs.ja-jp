---
title: ALTER SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SERVICE_MASTER_KEY_TSQL
- ALTER SERVICE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- FORCE option
- ALTER SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- modifying Service Master Key
- decryption [SQL Server], Service Master Key
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], modifying
ms.assetid: a1e9be0e-4115-47d8-9d3a-3316d876a35e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 29a30f6b8d65cf1b821c93de0f051925b3cb6626
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112857"
---
# <a name="alter-service-master-key-transact-sql"></a>ALTER SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのサービス マスター キーを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER SERVICE MASTER KEY   
    [ { <regenerate_option> | <recover_option> } ] [;]  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE  
  
<recover_option> ::=  
    { WITH OLD_ACCOUNT = 'account_name' , OLD_PASSWORD = 'password' }  
    |      
    { WITH NEW_ACCOUNT = 'account_name' , NEW_PASSWORD = 'password' }  
```  
  
## <a name="arguments"></a>引数  
 FORCE  
 データが失われる可能性があっても、サービス マスター キーを再生成することを示します。 詳しくは、後の「[SQL Server サービス アカウントの変更](#_changing)」をご覧ください。  
  
 REGENERATE  
 サービス マスター キーを再生成することを示します。  
  
 OLD_ACCOUNT **='***account_name***'**  
 古い Windows サービス アカウントの名前を指定します。  
  
> [!WARNING]  
>  このオプションは、互換性のために残されています。 使用しないでください。 代わりに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager を使用してください。  
  
 OLD_PASSWORD **='***password***'**  
 古い Windows サービス アカウントのパスワードを指定します。  
  
> [!WARNING]  
>  このオプションは、互換性のために残されています。 使用しないでください。 代わりに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager を使用してください。  
  
 NEW_ACCOUNT **='***account_name***'**  
 新しい Windows サービス アカウントの名前を指定します。  
  
> [!WARNING]  
>  このオプションは、互換性のために残されています。 使用しないでください。 代わりに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager を使用してください。  
  
 NEW_PASSWORD **='***password***'**  
 新しい Windows サービス アカウントのパスワードを指定します。  
  
> [!WARNING]  
>  このオプションは、互換性のために残されています。 使用しないでください。 代わりに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager を使用してください。  
  
## <a name="remarks"></a>Remarks  
 サービス マスター キーは、リンク サーバーのパスワード、資格情報、またはデータベースのマスター キーの暗号化が最初に必要になったときに、自動的に生成されます。 サービス マスター キーは、ローカル コンピューターのキーまたは Windows Data Protection API を使用して暗号化されます。 この API では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントの Windows 資格情報から派生するキーが使用されます。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] AES 暗号化アルゴリズムを使用してサービス マスター キー (SMK) とデータベース マスター キー (DMK) を保護します。 AES は、以前のバージョンで使用されていた 3DES よりも新しい暗号化アルゴリズムです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] にアップグレードした後で、マスター キーを AES にアップグレードするために SMK と DMK を再度生成する必要があります。 DMK を再作成する方法については、「[ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)」を参照してください。  
  
##  <a name="_changing"></a> SQL Server サービス アカウントの変更  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントを変更するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、サービス アカウントの変更を管理するために、サービス マスター キーの冗長なコピーが保存されます。このコピーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス グループに与えられる必要な権限を持つコンピューター アカウントによって保護されます。 コンピューターを再構築した場合、以前にサービス アカウントによって使用されていたのと同じドメイン ユーザーがサービス マスター キーを復元できますが、 ローカル アカウントや、Local System、Local Service、Network Service の各アカウントでは復元できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を別のコンピューターに移動する場合は、バックアップと復元を使用してサービス マスター キーを移行してください。  
  
 REGENERATE 句では、サービス マスター キーが再生成されます。 サービス マスター キーが再生成されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では古いサービス マスター キーで暗号化されていたすべてのキーの暗号化が解除され、それらのキーが新しいマスター キーで暗号化されます。 ただし、この操作はリソースを大量に消費するため、 キーのセキュリティに問題がある場合を除き、リソース要求が少ないときに実行するように考慮してください。 暗号化解除が 1 つでも失敗した場合は、ステートメント全体が失敗します。  
  
 FORCE オプションを使用すると、キーの再生成処理で現在のマスター キーを取得できなかった場合や、そのマスター キーで暗号化されている秘密キーをすべて暗号化解除できなかった場合でも、再生成処理が続行されます。 FORCE は、再生成が失敗し、[RESTORE SERVICE MASTER KEY](../../t-sql/statements/restore-service-master-key-transact-sql.md) ステートメントを使用してもサービス マスター キーを復元できない場合にのみ使用してください。  
  
> [!CAUTION]  
>  サービス マスター キーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 暗号化階層のルートになります。 サービス マスター キーでは、直接または間接的に、そのツリー内にある他のすべてのキーとシークレットが保護されます。 強制再生成で、依存関係のあるキーの暗号化を解除できなかった場合、そのキーで保護されているデータは失われます。  
  
 別のコンピューターに SQL を移動する場合、同じサービス アカウントを使用して SMK の暗号化を解除する必要があります。SQL Server では、自動的に、コンピューター アカウントの暗号化が修復されます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、サービス マスター キーを再生成します。  
  
```  
ALTER SERVICE MASTER KEY REGENERATE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
