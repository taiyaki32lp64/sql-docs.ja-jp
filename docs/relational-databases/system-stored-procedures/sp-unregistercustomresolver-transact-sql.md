---
title: sp_unregistercustomresolver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3e84fb602c253f5ee6dd247c01bbbd64bda1d2f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017865"
---
# <a name="spunregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以前に登録されたビジネス ロジック モジュールを登録解除します。 ビジネス ロジックにできるいずれかの形式、COM コンポーネントまたは[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework アセンブリ。 このストアド プロシージャは、カスタム ビジネス ロジックが登録されたディストリビューターで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>引数  
`[ @article_resolver = ] 'article_resolver'` 登録を解除するカスタム ビジネス ロジックの名前を指定します。 *article_resolver*は**nvarchar (255)** 、既定値はありません。 削除されるビジネス ロジックが COM コンポーネントの場合は、このパラメーターは、コンポーネントのフレンドリ名にします。 ビジネス ロジックが .NET Framework アセンブリの場合、このパラメーターはアセンブリの名前になります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_unregistercustomresolver**はマージ レプリケーションで使用します。  
  
 使用[sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)をトポロジに登録されているカスタム ビジネス ロジック モジュールまたは COM 競合回避モジュールの一覧を返す、レプリケーション トポロジ内の任意のサーバーでします。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_unregistercustomresolver**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_lookupcustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
