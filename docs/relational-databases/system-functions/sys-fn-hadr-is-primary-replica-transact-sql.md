---
title: fn_hadr_is_primary_replica (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_is_primary_replica
- fn_hadr_is_primary_replica_TSQL
- fn_hadr_is_primary_replica
- sys.fn_hadr_is_primary_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_hadr_is_primary_replica
- sys.fn_hadr_is_primary_replica
ms.assetid: c9b1969f-be1d-4dfb-a33d-551f380b9e27
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: befd4ba78a3d147acd8dd2adbd8fcb81500ec4b8
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811408"
---
# <a name="sysfn_hadr_is_primary_replica-transact-sql"></a>fn_hadr_is_primary_replica (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  現在のレプリカがプライマリ レプリカであるかどうかを決定するために使用されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_hadr_is_primary_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>引数  
 '*dbname*'  
 データベースの名前です。 *dbname*の型は sysname です。  
  
## <a name="returns"></a>戻り値  
 現在のインスタンス上のデータベースがプライマリ レプリカの場合は 1 を返します。 それ以外の場合は0を返します。  
  
## <a name="remarks"></a>コメント  
 この関数を使用すると、ローカルインスタンスが、指定された可用性データベースのプライマリレプリカをホストしているかどうかを簡単に判断できます。 サンプル コードは次のようになります。  
  
```  
If sys.fn_hadr_is_primary_replica ( @dbname ) <> 1   
BEGIN  
-- If this is not the primary replica, exit (probably without error).  
END  
-- If this is the primary replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-sysfn_hadr_is_primary_replica"></a>A. sys.fn_hadr_is_primary_replica の使用  
 次の例は、ローカル インスタンスの特定のデータベースがプライマリ レプリカである場合は 1 を返します。  
  
```  
SELECT sys.fn_hadr_is_primary_replica ('TestDB');  
GO  
```    
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループ関数&#40;transact-sql&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [_hadr_database_replica_states &#40;の&#41; transact-sql](../..//relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) [AlwaysOn 可用性グループ&#40;SQL Server&#41; ](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [AlwaysOn 可用性グループカタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)     
  
  
