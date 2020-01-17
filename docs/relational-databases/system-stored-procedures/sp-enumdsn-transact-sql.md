---
title: sp_enumdsn (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: stevestein
ms.author: sstein
ms.openlocfilehash: d84d366483cd5a887eb299b0f8d9208998e835c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124590"
---
# <a name="sp_enumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  特定の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザー アカウントで実行中のサーバーに定義されている、すべての ODBC および OLE DB のデータ ソース名の一覧を返します。 このストアド プロシージャは、任意のデータベースのパブリッシャーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Data Source Name**|**sysname**|データ ソースの名前。|  
|**Description**|**varchar(255)**|データ ソースの説明です。|  
|**Type**|**int**|データ ソースの種類です。<br /><br /> **1** = ODBC DSN<br /><br /> **3** = OLE DB データ ソース|  
|**Provider Name**|**varchar(255)**|OLE DB プロバイダーの名前です。 ODBC DSN の場合、値は NULL です。|  
  
## <a name="remarks"></a>コメント  
 すべて[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービスがユーザーのコンテキスト。 ユーザー コンテキストは、ユーザーの ODBC データ ソースの定義を含むレジストリ エントリのセットです。 ユーザー コンテキストが、ユーザー名によって提供される、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が実行されています。  
  
 たとえば、サーバーがシステム アカウントのユーザー コンテキストで実行している場合、データ ソース名 (Dsn) が返されるすべてのシステム Dsn はシステム アカウントに関連付けられているの。 サーバーがユーザーの個人アカウントで実行している場合のみで定義された Dsn のユーザーのプライベート アカウントが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_enumdsn**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_dsninfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
