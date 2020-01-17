---
title: sp_remoteoption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remoteoption_TSQL
- sp_remoteoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remoteoption
ms.assetid: c9a7309b-eab7-4192-a414-e282581af4e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 93e65bb7d72b15dcb29763a1c02845b6ff5faa01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68215932"
---
# <a name="spremoteoption-transact-sql"></a>sp_remoteoption (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているローカル サーバーで定義されているリモート ログインのオプションを表示または変更します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]sp_remoteoption では、任意のオプションは変更されず、エラー メッセージが返されます。 旧バージョンと互換性のためだけのことができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_remoteoption [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @loginame = ] 'loginame' ]   
     [ , [ @remotename = ] 'remotename' ]   
     [ , [ @optname = ] 'optname' ]   
     [ , [ @optvalue = ] 'optvalue' ]  
```  
  
## <a name="remarks"></a>コメント  
 このストアド プロシージャには、次のエラー メッセージが返されます。  
  
 `The trusted option in remote login mapping is no longer supported.`  
  
## <a name="see-also"></a>関連項目  
 [リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
  
