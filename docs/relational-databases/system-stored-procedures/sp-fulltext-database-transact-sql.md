---
title: sp_fulltext_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0c27f2efcfc15cc1ff9d53f735c08fad922f9466
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124278"
---
# <a name="spfulltextdatabase-transact-sql"></a>sp_fulltext_database (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  フルテキスト カタログにも何も起こりません[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降のバージョンとの下位互換性のみがサポートされます。 **sp_fulltext_database**は、特定のデータベースの Full-text Engine を無効になりません。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でユーザーが作成したすべてのデータベースでは、常にフルテキスト インデックスが有効になっています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>引数  
`[ @action = ] 'action'` 実行する操作です。 **アクション**は**varchar (20)** 、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**enable**|旧バージョンとの互換性のためにのみサポートされています。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンのフルテキスト カタログには影響しません。|  
|**disable**|旧バージョンとの互換性のためにのみサポートされています。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンのフルテキスト カタログには影響しません。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、フルテキスト インデックスを無効にすることはできません。 フルテキスト インデックス作成を無効にするから行が削除されません**sysfulltextcatalogs**され、フルテキストが有効なテーブルが、フルテキスト インデックス作成を不要になったマークされていることを示していません。 すべてのフルテキスト メタデータ定義では、システム テーブルに存在します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールと**db_owner**固定データベース ロールが実行できる**sp_fulltext_database**します。  
  
## <a name="see-also"></a>関連項目  
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
