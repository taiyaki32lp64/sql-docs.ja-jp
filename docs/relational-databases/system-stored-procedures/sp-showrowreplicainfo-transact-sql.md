---
title: sp_showrowreplicainfo (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
author: stevestein
ms.author: sstein
ms.openlocfilehash: d0c750fd35dce98c1d754f192214cd96cfc56143
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032895"
---
# <a name="sp_showrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ レプリケーション内のアーティクルとして使用されているテーブルの行についての情報を表示します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @ownername = ] 'ownername'` テーブルの所有者の名前です。 *ownername*は**sysname**、既定値は NULL です。 このパラメーターは、データベースに同じ名前を持つ複数のテーブルが含まれていますが、各テーブルには所有者が異なる場合は、テーブルを区別するために便利です。  
  
`[ @tablename = ] 'tablename'` 情報が返される行を含むテーブルの名前です。 *tablename*は**sysname**、既定値は NULL です。  
  
`[ @rowguid = ] rowguid` 行の一意の識別子です。 *rowguid*は**uniqueidentifier**、既定値はありません。  
  
`[ @show = ] 'show'` 結果セットで返される情報の量を決定します。 *表示*は**nvarchar (20)** 両方の既定値。 場合**行**行のバージョン情報のみが返されます。 場合**列**列のバージョン情報のみが返されます。 場合**両方**、両方の行および列情報が返されます。  
  
## <a name="result-sets-for-row-information"></a>行情報の結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|行バージョン エントリを作成したデータベースをホストしているサーバーの名前です。|  
|**db_name**|**sysname**|このエントリを作成したデータベースの名前です。|  
|**db_nickname**|**binary(6)**|このエントリを作成したデータベースのニックネームです。|  
|**version**|**int**|エントリのバージョンです。|  
|**current_state**|**nvarchar (9)**|行の現在の状態に関する情報を返します。<br /><br /> **y** -行データが行の現在の状態を表します。<br /><br /> **n** -行データは、行の現在の状態を表しません。<br /><br /> **\<該当なし >** は適用されません。<br /><br /> **\<不明な >** -現在の状態を特定できません。|  
|**rowversion_table**|**nchar(17)**|格納される行バージョンであるかどうかを示す、 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)テーブルまたは[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)テーブル。|  
|**comment**|**nvarchar (255)**|この行バージョン エントリに関する追加情報。 通常、このフィールドが空です。|  
  
## <a name="result-sets-for-column-information"></a>列情報の結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|列バージョン エントリを作成したデータベースを処理するサーバーの名前です。|  
|**db_name**|**sysname**|このエントリを作成したデータベースの名前です。|  
|**db_nickname**|**binary(6)**|このエントリを作成したデータベースのニックネームです。|  
|**version**|**int**|エントリのバージョンです。|  
|**colname**|**sysname**|列バージョン エントリを表すアーティクル列の名前です。|  
|**comment**|**nvarchar (255)**|この列バージョン エントリに関する追加情報です。 通常、このフィールドが空です。|  
  
## <a name="result-set-for-both"></a>両方の結果セット  
 場合、値**両方**に選択されている*表示*行と列の両方の結果セットが返されます。  
  
## <a name="remarks"></a>コメント  
 **sp_showrowreplicainfo**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **sp_showrowreplicainfo**のメンバーによってのみ実行されることができます、 **db_owner**のパブリケーション データベースのパブリケーション アクセス リスト (PAL) のメンバー、またはパブリケーション データベースの固定データベース ロール。  
  
## <a name="see-also"></a>関連項目  
 [マージ レプリケーションの詳細 - 競合の検出および解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
