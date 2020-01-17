---
title: sp_fulltext_pendingchanges (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4d8cbd7082a3ec8d19ccc6df7212a70b101e6b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124222"
---
# <a name="spfulltextpendingchanges-transact-sql"></a>sp_fulltext_pendingchanges (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  保留中の挿入、更新、および削除の場合は、指定したテーブルを使用している変更の追跡など返しますが、変更にまだ処理されていません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>引数  
 *table_id*  
 テーブルの ID。 テーブルがない場合、フルテキスト インデックスを作成、またはテーブルの変更の追跡が有効でない、エラーが返されます。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**[キー]**|*|指定したテーブルからのフルテキスト キー値。|  
|**DocId**|**bigint**|キー値に対応する内部ドキュメント識別子 (DocId) 列。|  
|**状態**|**int**|0 = 行は、フルテキスト インデックスから削除されます。<br /><br /> 1 = 行にはフルテキスト インデックスが作成されます。<br /><br /> 2 = 行は最新です。<br /><br /> -1 = 行は、遷移 (一括処理されたがコミットされていない) 状態またはエラー状態にします。|  
|**DocState**|**tinyint**|内部ドキュメント識別子 (Docld) のマップ ステータス列の行ダンプ。|  
  
 <sup>* キーのデータ型は、ベース テーブルのフルテキスト キー列のデータ型と同じです。</sup>  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="remarks"></a>コメント  
 未処理の変更がない場合、空の行セットが返されます。  
  
 フルテキスト検索のクエリを持つ行が返されない、**状態**0 の値。 これは、行がベース テーブルから削除されて、フルテキスト インデックスから削除するを待機しているためです。  
  
 いくつの変更が保留中を検索する特定のテーブルを使用して、 **TableFullTextPendingChanges** OBJECTPROPERTYEX 関数のプロパティ。  
  
## <a name="see-also"></a>関連項目  
 [フルテキスト検索およびセマンティック検索ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
