---
title: sp_vupgrade_mergeobjects (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_mergeobjects
- sp_vupgrade_mergeobjects_TSQL
helpviewer_keywords:
- sp_vupgrade_mergeobjects
ms.assetid: 73257c2e-cc4c-48e7-9d66-7ef045bdd4f5
author: stevestein
ms.author: sstein
ms.openlocfilehash: ed0992ff1b6b7de6f93213b612ff05ebcbdb3df5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042700"
---
# <a name="spvupgrademergeobjects-transact-sql"></a>sp_vupgrade_mergeobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アーティクル固有のトリガー、ストアド プロシージャ、および追跡し、マージ レプリケーションのデータの変更の適用に使用されるビューを再生成します。 次の状況でこの手順を実行します。  
  
-   レプリケーションによって要求されたオブジェクトが誤って削除された場合。  
  
-   1 つ以上のレプリケーション オブジェクトに修正プログラムなどの更新プログラムを適用する場合で、プログラムに修正が必要な場合。 更新プログラムを適用した後、各ノードでプロシージャを実行します。  
  
 このストアド プロシージャを実行しても、サブスクリプションの再初期化は不要です。 この手順は、サービス パックをインストールまたはの新しいバージョンにアップグレードする場合は必要ありません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_vupgrade_mergeobjects [ [@login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @security_mode = ] security_mode ]  
```  
  
## <a name="arguments"></a>引数  
`[ @login = ] 'login'` ディストリビューション データベースに新しいシステム オブジェクトを作成するときに使用するシステム管理者のログインです。 *login* のデータ型は **sysname** で、既定値は NULL です。 このパラメーターは必要ない場合は*security_mode*に設定されている**1**、つまり Windows 認証。  
  
`[ @password = ] 'password'` ディストリビューション データベースに新しいシステム オブジェクトを作成するときに使用するシステム管理者のパスワードです。 *パスワード*は**sysname**、既定値は **'** (空の文字列)。 このパラメーターは必要ない場合は*security_mode*に設定されている**1**、つまり Windows 認証。  
  
`[ @security_mode = ] 'security_mode'` ディストリビューション データベースに新しいシステム オブジェクトを作成するときに使用するログイン セキュリティ モードです。 *security_mode*は**ビット**の既定値を持つ**1**します。 場合**0**、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証が使用されます。 場合**1**、Windows 認証が使用されます。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_vupgrade_mergeobjects**マージ レプリケーションのみに使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [レプリケートされたデータベースのアップグレード](../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
