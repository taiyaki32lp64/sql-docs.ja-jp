---
title: sys.database_scoped_credentials (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.database_scoped_credentials
- sys.database_scoped_credentials_TSQL
- database_scoped_credentials
- database_scoped_credentials_TSQL
helpviewer_keywords:
- sys.database_scoped_credentials catalog view
ms.assetid: 68e8aa6b-bcdc-42aa-93d8-d498f724c188
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03687ea50b04c96aa4dbafab9d02d2bbc33a14b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079422"
---
# <a name="sysdatabasescopedcredentials-transact-sql"></a>sys.database_scoped_credentials (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  スコープのデータベースの資格情報をデータベースごとに 1 つの行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|データベースの名前スコープの資格情報。 データベース内で一意です。|  
|credential_id|**int**|データベース スコープ資格情報の ID。 データベース内で一意です。|  
|principal_id|**int**|キーを所有するデータベース プリンシパルの ID。|  
|credential_identity|**nvarchar (4000)**|使用する識別情報の名前。 通常は Windows ユーザーです。 一意である必要はありません。|  
|create_date|**datetime**|データベース スコープ資格情報が作成された時刻。|  
|modify_date|**datetime**|データベース スコープ資格情報が最後に変更された時刻。|  
|target_type|**nvarchar(100)**|種類のデータベース スコープの資格情報。 返します`NULL`データベース スコープの資格情報。|  
|target_id|**int**|データベース スコープ資格情報にマップされているオブジェクトの ID。 スコープの資格情報をデータベースの 0 を返します。|  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する `CONTROL` 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
