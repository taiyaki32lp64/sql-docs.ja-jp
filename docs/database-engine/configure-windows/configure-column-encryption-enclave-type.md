---
title: Always Encrypted サーバー構成オプションのエンクレーブの種類を構成する | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 4786c512850d161d9b7ab33f2a12cd0bd077b2bd
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593827"
---
# <a name="configure-the-enclave-type-for-always-encrypted-server-configuration-option"></a>Always Encrypted サーバー構成オプションのエンクレーブの種類を構成する
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

この記事では、セキュリティで保護されたエンクレーブが設定された Always Encrypted でセキュリティで保護されたエンクレーブを有効または無効にする方法について説明します。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」を参照してください。

**列暗号化エンクレーブの種類**サーバー構成オプションを使うと、Always Encrypted に使用されるセキュリティで保護されたエンクレーブの種類を制御できます。 次のいずれかの値にオプションを設定できます。  
  
|[値]|Description|  
|-------------------|-----------------| 
|0|**セキュア エンクレーブなし**。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は Always Encrypted のセキュア エンクレーブを初期化しません。 そのため、セキュア エンクレーブを使用した Always Encrypted の機能は利用できなくなります。|  
|1|**仮想化ベースのセキュリティ (VBS)** 。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] により、仮想化ベースのセキュリティ (VBS) エンクレーブの初期化が試みられます。

> [!IMPORTANT]
> **列暗号化エンクレーブの種類**の変更は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを再起動するまで反映されません。
   
[sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) ビューを使うことで、構成されているエンクレーブの種類の値と、現在有効なエンクレーブの種類の値を確認できます。 

現在有効になっている (0 より大きい) 種類のエンクレーブが [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] の最後の再起動後に正しく初期化されていることを確認するには、[sys.dm_column_encryption_enclave (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md) ビューを調べます。
 - ビューに含まれているのが 1 行だけの場合、エンクレーブは正しく初期化されています。 
 - ビューに行が含まれていない場合は、SQL Server のエラー ログでエンクレーブの初期化エラーを確認します。「[SQL Server エラー ログの表示 (SQL Server Management Studio)](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)」を参照してください。

VBS エンクレーブを構成する手順のについて詳しくは、「[SQL Server 上でセキュア エンクレーブを使用する Always Encrypted を有効にする](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md#step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server)」を参照してください。

## <a name="examples"></a>使用例  
 次の例では、セキュリティで保護されたエンクレーブを有効にし、エンクレーブの種類を VBS に設定します。

```sql  
sp_configure 'column encryption enclave type', 1;  
GO  
RECONFIGURE;  
GO  
```  

次に示すのは、セキュア エンクレーブを無効にする場合の例です。  

```sql  
sp_configure 'column encryption enclave type', 0;  
GO  
RECONFIGURE;  
GO  
```  

次のクエリでは、構成されているエンクレーブの種類と、現在有効なエンクレーブの種類を取得します。

```sql  
USE [master];
GO
SELECT
[value]
, CASE [value] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_description]
, [value_in_use]
, CASE [value_in_use] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_in_use_description]
FROM sys.configurations
WHERE [name] = 'column encryption enclave type'; 
```  
## <a name="next-steps"></a>Next Steps
 [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)

## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sys.configurations (Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.dm_column_encryption_enclave (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md)   
