---
title: sp_helpserver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
author: stevestein
ms.author: sstein
ms.openlocfilehash: 844e96d765f9ed06f88b140b906b78eb4ea16ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997433"
---
# <a name="sphelpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  特定のリモート サーバーまたはレプリケーション サーバー、あるいはすべてのリモート サーバーとレプリケーション サーバーに関する情報をレポートします。 サーバー名、サーバーのネットワーク名、サーバーのレプリケーションの状態、サーバー、および照合順序名の識別番号を提供します。 接続するか、リンク サーバーに対するクエリのタイムアウト値を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @server = ] 'server'` サーバーに関する情報が報告されます。 ときに*server*が指定されていないすべてのサーバーに関するレポート**master.sys.servers**します。 *server*は**sysname**、既定値は NULL です。  
  
`[ @optname = ] 'option'` サーバーを説明するオプション。 *オプション*は**varchar (** 35 **)** 、既定値は null の場合、これらの値のいずれかを指定する必要があります。  
  
|値|説明|  
|-----------|-----------------|  
|**collation compatible**|リンク サーバーに対して分散クエリの実行に影響します。 このオプションを true に設定した場合、|  
|**data access**|分散クエリ アクセスに対してリンク サーバーを有効または無効にします。|  
|**dist**|ディストリビューターです。|  
|**dpub**|このディストリビューターへのリモート パブリッシャーです。|  
|**lazy schema validation**|クエリ開始時のリモート テーブルのスキーマ チェックをスキップします。|  
|**pub**|パブリッシャーです。|  
|**rpc**|指定されたサーバーからの RPC を有効にします。|  
|**rpc out**|指定されたサーバーへの RPC を有効にします。|  
|**sub**|サブスクライバー。|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**use remote collation**|ローカル サーバーの代わりに、リモート列の照合順序を使用します。|  
  
`[ @show_topology = ] 'show_topology'` 他のサーバーに指定されたサーバーのリレーションシップです。 *show_topology*は**varchar (** 1 **)** 、既定値は NULL です。 場合*show_topology*が等しくない**t**が null の場合、または**sp_helpserver**結果セット セクションに示されている列を返します。 場合*show_topology*と等しい**t**、結果セットには、示されている列だけでなく**sp_helpserver**も返します**topx**と**topy**情報。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|サーバー名。|  
|**network_name**|**sysname**|サーバーのネットワーク名|  
|**status**|**varchar(** 70 **)**|サーバーの状態。|  
|**id**|**char(** 4 **)**|サーバーの識別番号|  
|**collation_name**|**sysname**|サーバーの照合順序です。|  
|**connect_timeout**|**int**|リンク サーバーへの接続のタイムアウト値。|  
|**query_timeout**|**int**|リンク サーバーに対するクエリのタイムアウト値|  
  
## <a name="remarks"></a>コメント  
 1 つのサーバーについて複数の状態値が返されることもあります。  
  
## <a name="permissions"></a>アクセス許可  
 権限は確認されません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-information-about-all-servers"></a>A. すべてのサーバーに関する情報を表示します。  
 次の例では、パラメーターを指定せずに `sp_helpserver` を使用して、すべてのサーバーに関する情報を表示します。  
  
```  
USE master;  
GO  
EXEC sp_helpserver;  
```  
  
### <a name="b-displaying-information-about-a-specific-server"></a>B. 特定のサーバーに関する情報を表示する  
 次の例では、すべての情報を表示について、`SEATTLE2`サーバー。  
  
```  
USE master;  
GO  
EXEC sp_helpserver 'SEATTLE2';  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_addsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
