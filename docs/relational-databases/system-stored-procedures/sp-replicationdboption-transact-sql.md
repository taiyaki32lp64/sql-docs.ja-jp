---
title: sp_replicationdboption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c0837db9666ab6b49aee30b81b5585cbf5d5ee0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056771"
---
# <a name="sp_replicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定したデータベースのレプリケーション データベース オプションを設定します。 このストアドプロシージャは、任意のデータベースのパブリッシャーまたはサブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbname'` は、レプリケーションデータベースオプションを設定するデータベースです。 *db_name*は**sysname**であり、既定値はありません。  
  
`[ @optname = ] 'optname'` は、を有効または無効にするレプリケーションデータベースオプションです。 *optname*は**sysname**で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**merge publish**|データベースは、マージ パブリケーションで使用できます。|  
|**publish**|データベースは、他の種類のパブリケーションで使用できます。|  
|**web**|データベースはサブスクリプションデータベースです。|  
|**バックアップとの同期**|データベースは、連携バックアップに対して有効になっています。 詳細については、「[トランザクション&#40;レプリケーションレプリケーションでの連携バックアップの有効化&#41;transact-sql プログラミング](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)」を参照してください。|  
  
`[ @value = ] 'value'` は、指定されたレプリケーションデータベースオプションを有効または無効にするかどうかを指定します。 *値*は**sysname**で、 **true**または**false**を指定できます。 この値が**false**で、 *optname*が**merge publish**の場合、マージパブリッシュされたデータベースに対するサブスクリプションも削除されます。  
  
`[ @ignore_distributor = ] ignore_distributor` は、ディストリビューターに接続せずにこのストアドプロシージャを実行するかどうかを示します。 *ignore_distributor*のデータ型は**bit**で、既定値は**0**です。この場合、ディストリビューターは、パブリッシングデータベースの新しい状態に接続して更新する必要があります。 値**1**は、ディストリビューターにアクセスできない場合にのみ指定し、パブリッシングを無効にするために**sp_replicationdboption**を使用する必要があります。  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_replicationdboption**は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
 このプロシージャでは、指定したオプションに従って、特定のレプリケーション システム テーブル、セキュリティ アカウントなどが作成または削除されます。 対応する**is_published** (transacational またはスナップショットレプリケーション)、 **is_merge_published** (マージレプリケーション)、または**is_distributor**ビットを**master データベース**テーブルに設定し、必要なシステムテーブルを作成します。  
  
 パブリッシングを無効にするには、パブリケーションデータベースがオンラインである必要があります。 パブリケーションデータベースのデータベーススナップショットが存在する場合は、パブリッシングを無効にする前にデータベーススナップショットを削除する必要があります。 データベーススナップショットは、データベースの読み取り専用のオフラインコピーであり、レプリケーションスナップショットに関連付けられていません。 詳細については、「[データベース スナップショット &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replicationdboption**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [パブリッシングとディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [パブリケーション  の削除](../../relational-databases/replication/publish/delete-a-publication.md)  
 [パブリッシングおよびディストリビューションの無効化](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
