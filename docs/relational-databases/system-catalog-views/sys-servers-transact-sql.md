---
title: sys.servers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- servers_TSQL
- sys.servers_TSQL
- servers
- sys.servers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.servers catalog view
ms.assetid: 4e774ed9-4e83-4726-9f1d-8efde8f9feff
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b17296d558c078d3f580e63bf662bb975615ad94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132947"
---
# <a name="sysservers-transact-sql"></a>sys.servers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  登録されると、リンクまたはリモート サーバーごとに 1 行と 1 行を持つ、ローカル サーバーのデータを含む**server_id** = 0。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|リンク サーバーのローカル ID です。|  
|**name**|**sysname**|ときに**server_id** = 0 の場合、サーバー名が返されます。<br /><br /> ときに**server_id** > 0 の場合、返される値は、リンク サーバーのローカル名。|  
|**product**|**sysname**|リンク サーバーの製品名。 "SQL Server"の値を別のインスタンスを示します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**provider**|**sysname**|リンク サーバー接続用の OLE DB プロバイダー名です。|  
|**data_source**|**nvarchar (4000)**|OLE DB データ ソース接続プロパティです。|  
|**location**|**nvarchar (4000)**|OLE DB 場所接続プロパティです。 存在しない場合は NULL です。|  
|**provider_string**|**nvarchar (4000)**|OLE DB プロバイダー文字列接続プロパティです。<br /><br /> 呼び出し側に ALTER ANY LINKED SERVER 権限がなければ NULL になります。|  
|**catalog**|**sysname**|OLEDB カタログ接続プロパティです。 存在しない場合は NULL です。|  
|**connect_timeout**|**int**|存在しない場合は、秒単位、0 のタイムアウトを接続します。|  
|**query_timeout**|**int**|存在しない場合は、タイムアウトを秒単位、0 クエリします。|  
|**is_linked**|**bit**|0 = を使用して追加された旧形式のサーバーは、 **sp_addserver**、さまざまな RPC および分散トランザクションの動作。<br /><br /> 1 の場合、標準リンク サーバーです。|  
|**is_remote_login_enabled**|**bit**|このサーバーに対する着信リモート ログインを有効にする RPC オプションが設定されています。|  
|**is_rpc_out_enabled**|**bit**|(このサーバーからの) 発信 RPC が有効です。|  
|**is_data_access_enabled**|**bit**|分散クエリでは、サーバーは有効です。|  
|**is_collation_compatible**|**bit**|リモート データの照合順序は、照合順序に関する情報がない場合にはローカル データと互換性があると見なされます。|  
|**uses_remote_collation**|**bit**|1 の場合、リモート サーバーによってレポートされる照合順序を使用し、それ以外の場合は、次の列で指定された照合順序を使用します。|  
|**collation_name**|**sysname**|使用する照合順序名です。ローカルを使用するだけの場合は NULL です。|  
|**lazy_schema_validation**|**bit**|1 の場合、スキーマの検証はクエリの開始時はチェックされません。|  
|**is_system**|**bit**|このサーバーは、内部システムからのみアクセスできます。|  
|**is_publisher**|**bit**|サーバーは、レプリケーションのパブリッシャーです。|  
|**is_subscriber**|**bit**|サーバーはレプリケーション サブスクライバーです。|  
|**is_distributor**|**bit**|サーバーはレプリケーション ディストリビューターです。|  
|**is_nonsql_subscriber**|**bit**|サーバーは SQL Server 以外のレプリケーション サブスクライバーです。|  
|**is_remote_proc_transaction_promotion_enabled**|**bit**|1 の場合、リモート ストアド プロシージャを呼び出す、分散トランザクションを開始しは MS DTC トランザクションに参加します。 詳細については、「 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)からデータにアクセスする方法について説明します。|  
|**modify_date**|**datetime**|サーバー情報が前回変更された日付です。|  
  
## <a name="permissions"></a>アクセス許可  
 値**provider_string**は呼び出し元は、ALTER ANY LINKED SERVER 権限を持っていない場合に常に NULL です。  
  
 アクセス許可がローカル サーバーを表示する必要はありません (**server_id** = 0)。  
  
 リンクまたはリモート サーバーを作成するときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、既定のログイン マッピングを作成、**パブリック**サーバーの役割。 既定のログイン マッピングは、すべてのログインがすべてのリンクとリモート サーバーを表示できることを意味します。 これらのサーバーへの可視性を制限するには、実行することによって既定のログイン マッピングを削除[sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) NULL を指定して、 *locallogin*パラメーター。  
  
 既定のログイン マッピングを削除すると、リンク ログインまたはリモート ログインとして明示的に追加されている唯一のユーザーはログインがあるリンクまたはリモート サーバーを表示できます。  次のアクセス許可は、既定のログイン マッピング後のすべてのリンクとリモート サーバーを表示する必要があります。  
  
- `ALTER ANY LINKED SERVER` または `ALTER ANY LOGIN ON SERVER`  
- メンバーシップ、 **setupadmin**または**sysadmin**固定サーバー ロール  
  
## <a name="see-also"></a>関連項目  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [リンク サーバーのカタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
  
