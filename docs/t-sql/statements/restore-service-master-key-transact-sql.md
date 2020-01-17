---
title: RESTORE SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE SERVICE MASTER KEY
- RESTORE_SERVICE_MASTER_KEY_TSQL
- LOAD SERVICE MASTER KEY
- LOAD_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- importing Service Master Keys
- copying Service Master Keys
- service master key [SQL Server], importing
- RESTORE SERVICE MASTER KEY statement
- transferring Service Master Keys
ms.assetid: a68fd0ee-70ce-4104-aca0-fcae5f41fc38
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a4bbbb9b08c63e6ab6f8b68d304b611847707558
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141245"
---
# <a name="restore-service-master-key-transact-sql"></a>RESTORE SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  バックアップ ファイルからサービス マスター キーをインポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
RESTORE SERVICE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password' [FORCE]  
```  
  
## <a name="arguments"></a>引数  
 FILE **='** _path\_to\_file_ **'**  
 格納されているサービス マスター キーへの完全なパスを、ファイル名を含めて指定します。 *path_to_file* には、ローカル パスまたはネットワーク上の場所を示す UNC パスを指定できます。  
  
 PASSWORD **='** _password_ **'**  
 ファイルからインポートされるサービス マスター キーの暗号化の解除に必要なパスワードを指定します。  
  
 FORCE  
 データが失われる可能性があっても、強制的にサービス マスター キーを置換します。  
  
## <a name="remarks"></a>Remarks  
 サービス マスター キーを復元するとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、現在のサービス マスター キーで暗号化されているすべてのキーとシークレットの暗号化が解除され、次にそれらがバックアップ ファイルから読み込まれたサービス マスター キーで暗号化されます。  
  
 暗号化解除が 1 つでも失敗した場合、復元は失敗します。 FORCE オプションを使用するとエラーを無視できますが、暗号化を解除できないデータが失われる可能性があります。  
  
> [!CAUTION]  
>  サービス マスター キーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 暗号化階層のルートになります。 サービス マスター キーでは、直接または間接的に、そのツリー内の他のすべてのキーが保護されます。 強制復元で、依存関係のあるキーの暗号化を解除できなかった場合、そのキーで保護されているデータは失われます。  
  
 暗号化階層の再生成操作はリソースを大量に消費するため、 リソース要求が少ないときに実行するように考慮してください。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、バックアップ ファイルからサービス マスター キーを復元します。  
  
```  
RESTORE SERVICE MASTER KEY   
    FROM FILE = 'c:\temp_backups\keys\service_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [サービス マスター キー](../../relational-databases/security/encryption/service-master-key.md)   
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)