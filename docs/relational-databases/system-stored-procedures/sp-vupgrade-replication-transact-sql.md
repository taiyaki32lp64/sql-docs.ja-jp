---
title: sp_vupgrade_replication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f6b2c736087b2f860bf8419264904e8669ba8951
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771548"
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  レプリケーションサーバーをアップグレードするときに、セットアップによってアクティブ化されます。 は、現在の製品レベルでレプリケーションをサポートするために、必要に応じてスキーマとシステムデータをアップグレードします。 また、システム データベースとユーザー データベースに、新しいレプリケーション システム オブジェクトを作成します。 このストアドプロシージャは、レプリケーションのアップグレードが行われるコンピューターで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>引数  
`[ @login = ] 'login'`ディストリビューションデータベースに新しいシステムオブジェクトを作成するときに使用するシステム管理者のログインを示します。 *login* のデータ型は **sysname** で、既定値は NULL です。 *Security_mode*が**1**(Windows 認証) に設定されている場合、このパラメーターは必要ありません。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンへのアップグレードの場合、このパラメーターは無視されます。  
  
`[ @password = ] 'password'`ディストリビューションデータベースに新しいシステムオブジェクトを作成するときに使用するシステム管理者のパスワードを入力します。 *パスワード*は**sysname**,、既定値は **' '** (空の文字列)。 *Security_mode*が**1**(Windows 認証) に設定されている場合、このパラメーターは必要ありません。  
  
> [!NOTE]  
>  SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降のバージョンにアップグレードする場合、このパラメーターは無視されます。  
  
`[ @ver_old = ] 'old_version'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 このストアドプロシージャは非推奨とされており、の将来[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリリースで削除される予定です。  
  
`[ @force_remove = ] 'force_removal'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @security_mode = ] 'security_mode'`ディストリビューションデータベースに新しいシステムオブジェクトを作成するときに使用するログインセキュリティモードを示します。 *security_mode*の部分は**bit**で、既定値は**0**です。 **0**の場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、認証が使用されます。 **1**の場合、Windows 認証が使用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンへのアップグレードの場合、このパラメーターは無視されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_vupgrade_replication**は、すべての種類のレプリケーションをアップグレードするときに使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_vupgrade_replication**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
