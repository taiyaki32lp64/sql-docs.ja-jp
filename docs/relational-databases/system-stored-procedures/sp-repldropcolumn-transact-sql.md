---
title: sp_repldropcolumn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldropcolumn_TSQL
- sp_repldropcolumn
helpviewer_keywords:
- sp_repldropcolumn
ms.assetid: fdc1ec5f-f108-42b4-a2d8-f06a71913ab8
author: stevestein
ms.author: sstein
ms.openlocfilehash: a6b398a4dd7e93521b38708d3a7e37ae09e70a15
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771468"
---
# <a name="sprepldropcolumn-transact-sql"></a>sp_repldropcolumn (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリッシュされた既存のテーブルアーティクルから列を削除します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!IMPORTANT]
>  このストアドプロシージャは非推奨とされており、主に旧バージョンとの互換性のためにサポートされています。 これは、パブリッシャーと再[!INCLUDE[msCoName](../../includes/msconame-md.md)]パブリッシュサブスクライバー [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]で[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]のみ使用してください。 このプロシージャは、以降で[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]導入されたデータ型の列では使用できません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_repldropcolumn [ @source_object = ] 'source_object', [ @column = ] 'column'   
    [ , [ @from_agent = ] from_agent]   
    [ , [ @schema_change_script = ] 'schema_change_script' ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>引数  
 [ @source_object =] '*source_object*'  
 削除する列が含まれるテーブル アーティクルの名前を指定します。 *source_object*は nvarchar (258),、既定値はありません。  
  
 [ @column =] '*column*'  
 テーブル内の削除する列の名前を指定します。 *列*は sysname,、既定値はありません。  
  
 [ @from_agent =] *from_agent*  
 ストアドプロシージャがレプリケーションエージェントによって実行される場合はです。 *from_agent*は int,、既定値は0です。このストアドプロシージャがレプリケーションエージェントによって実行されるときに値1が使用され、その他のすべての場合は既定値0を使用します。  
  
 [ @schema_change_script =] '*schema_change_script*'  
 システムによって生成される[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]カスタムストアドプロシージャの変更に使用するスクリプトの名前とパスを指定します。 *schema_change_script*は nvarchar (4000),、既定値は NULL です。 レプリケーションでは、トランザクションレプリケーションで使用される1つ以上の既定のプロシージャを、ユーザー定義のカスタムストアドプロシージャで置き換えることができます。 *schema_change_script*は、sp_repldropcolumn を使用してレプリケートされたテーブルアーティクルに対してスキーマ変更が行われた後に実行され、次のいずれかの操作に使用できます。  
  
-   カスタムストアドプロシージャが自動的に再生成された場合、 *schema_change_script*を使用してこれらのカスタムストアドプロシージャを削除し、新しいスキーマをサポートするユーザー定義のカスタムストアドプロシージャに置き換えることができます。  
  
-   カスタムストアドプロシージャが自動的に再生成されない場合は、 *schema_change_script*を使用して、これらのストアドプロシージャを再生成したり、ユーザー定義のカスタムストアドプロシージャを作成したりできます。  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 スナップショットを無効にする機能を有効または無効にします。 *force_invalidate_snapshot*はビット,、既定値は1です。  
  
 1 に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。この場合、値 1 では新しいスナップショットを作成する権限が与えられます。  
  
 0 に設定すると、アーティクルへの変更によってスナップショットが無効になることはありません。  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 サブスクリプションを再初期化する機能を有効または無効にします。 *force_reinit_subscription*はビットで、既定値は0です。  
  
 0に設定すると、アーティクルへの変更によってサブスクリプションが再初期化されることはありません。  
  
 1 に設定すると、アーティクルへの変更によってサブスクリプションが再初期化されることがあります。この場合、値 1 ではサブスクリプションを再初期化する権限が与えられます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 sp_repldropcolumn を実行できるのは、パブリッシャー側の sysadmin 固定サーバー ロールのメンバー、またはパブリケーション データベースの db_owner 固定データベース ロールや db_ddladmin 固定データベース ロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server レプリケーションの非推奨の機能](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
