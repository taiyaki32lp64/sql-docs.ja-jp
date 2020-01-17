---
title: sp_changereplicationserverpasswords (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9feddab12ea972ea4d7764fccfdd91a7f9b89cec
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762253"
---
# <a name="sp_changereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  レプリケーショントポロジ内のサーバー [!INCLUDE[msCoName](../../includes/msconame-md.md)]に接続する[!INCLUDE[msCoName](../../includes/msconame-md.md)]ときに、レプリケーションエージェントによって使用される Windows アカウントまたは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインのために保存されたパスワードを変更します。 通常は、サーバーで実行中のエージェントがすべて同じログインまたはアカウントを使用している場合でも、個々のエージェントごとにパスワードを変更する必要があります。 このストアド プロシージャにより、サーバーで実行中のすべてのレプリケーション エージェントが使用する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインまたは Windows アカウントのすべてのインスタンスに対するパスワードを変更することができます。 このストアドプロシージャは、master データベースのレプリケーショントポロジ内の任意のサーバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @login_type = ] login_type`指定された資格情報の認証の種類を指定します。 *login_type*は**tinyint**,、既定値はありません。  
  
 **1** = Windows 統合認証  
  
 **0**  = 認証[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
`[ @login = ] 'login'`変更する Windows アカウントまたは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインの名前を指定します。 *ログイン*は**nvarchar (257)** ,、既定値はありません。  
  
`[ @password = ] 'password'`指定した*ログイン*用に格納する新しいパスワードを指定します。 *パスワード*は**sysname**,、既定値はありません。  
  
> [!NOTE]  
>  レプリケーション パスワードを変更したら、そのパスワードを使用する各エージェントを停止して再起動し、エージェントに対して変更を反映させる必要があります。  
  
`[ @server = ] 'server'`格納されているパスワードを変更するサーバー接続を指定します。 *サーバー*は**sysname**で、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**distributor**|ディストリビューターへのすべてのエージェント接続。|  
|**publisher**|パブリッシャーへのすべてのエージェント接続。|  
|**subscriber**|サブスクライバーへのすべてのエージェント接続。|  
|**%** (既定値)|レプリケーション トポロジ内のすべてのサーバーへのすべてのエージェント接続です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changereplicationserverpasswords**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changereplicationserverpasswords**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
