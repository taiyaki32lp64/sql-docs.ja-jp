---
title: sys.fn_servershareddrives (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_servershareddrives
- fn_servershareddrives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_servershareddrives function
- shared drives [SQL Server]
- names [SQL Server], shared drives
- sys.fn_serversharedrives function
ms.assetid: ff01eff7-8cb6-460c-ba7a-6a52bda6d471
author: rothja
ms.author: jroth
ms.openlocfilehash: 71858ee3c57af8d94bdf4ef4addad720655942f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122551"
---
# <a name="sysfnservershareddrives-transact-sql"></a>sys.fn_servershareddrives (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  クラスター化されたサーバーが使用する共有ドライブの名前を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのシステム関数は、旧バージョンとの互換性のために用意されています。 使用することをお勧めします。 [sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_servershareddrives()  
```  
  
## <a name="tables-returned"></a>返されるテーブル  
 現在のサーバーがクラスター化されたサーバーの場合**fn_servershareddrives**共有ドライブのドライブ名を返します。  
  
 現在のサーバー インスタンスがクラスター化されたサーバーではない場合**fn_servershareddrives**空の行セットを返します。  
  
## <a name="remarks"></a>コメント  
 `fn_servershareddrives` このクラスター化されたサーバーで使用する共有ドライブの一覧を返します。 これらの共有ドライブのと同じクラスター グループに属している、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]リソース。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリソースはこれらのドライブに依存しています。  
  
 この関数は、ユーザーが利用できるドライブを特定するのに役立つです。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では`fn_servershareddrives`クラスター化されたサーバー インスタンスに対してクエリを実行します。  
  
```  
SELECT * FROM fn_servershareddrives();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 DriveName  
  
 -------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)  
  
  
