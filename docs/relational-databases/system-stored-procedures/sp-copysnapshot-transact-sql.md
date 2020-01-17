---
title: sp_copysnapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysnapshot
- sp_copysnapshot_TSQL
helpviewer_keywords:
- sp_copysnapshot
ms.assetid: a012a32f-6f26-45bf-8046-b51cd7fec455
author: stevestein
ms.author: sstein
ms.openlocfilehash: d8b34915371b164a4167058729d2720d9e60cdcd
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154606"
---
# <a name="sp_copysnapshot-transact-sql"></a>sp_copysnapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたパブリケーションのスナップショットフォルダーを **\@destination_folder**に一覧表示されているフォルダーにコピーします。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。 このストアド プロシージャは、スナップショットを CD-ROM などのリムーバブル メディアにコピーするときに効果的です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_copysnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` スナップショットの内容をコピーするパブリケーションの名前を指定します。 *publication* は **sysname** 、既定値はありません。  
  
`[ @destination_folder = ] 'destination_folder'` には、パブリケーションスナップショットの内容をコピーするフォルダーの名前を指定します。 *destination_folder*は**nvarchar (255)** ,、既定値はありません。 *Destination_folder*は、別のサーバー、ネットワークドライブ、リムーバブルメディア (cd-rom やリムーバブルディスクなど) などの別の場所にすることができます。  
  
`[ @subscriber = ] 'subscriber'` はサブスクライバーの名前です。 *サブスクライバー*の sysname,、既定値は NULL です。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプション データベースの名前です。 *subscriber_db*は sysname,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_copysnapshot**は、すべての種類のレプリケーションで使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョン7.0 以前の [!INCLUDE[msCoName](../../includes/msconame-md.md)] 実行されているサブスクライバーでは、代替スナップショットの場所を使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_copysnapshot**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [スナップショット フォルダーの代替位置](../../relational-databases/replication/snapshot-options.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
