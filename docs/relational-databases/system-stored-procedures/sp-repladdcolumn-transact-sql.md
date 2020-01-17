---
title: sp_repladdcolumn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords:
- sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
author: stevestein
ms.author: sstein
ms.openlocfilehash: 75c66d1077b111837197957cc845b690b794ea24
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771052"
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリッシュされた既存のテーブル アーティクルに列を追加します。 このテーブルをパブリッシュするすべてのパブリッシャーに新しい列を追加することも、テーブルをパブリッシュする特定のパブリケーションに列を追加することもできます。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!IMPORTANT]
>  このストアドプロシージャは非推奨とされており、旧バージョンとの互換性のためにサポートされています。 これは、パブリッシャーと再[!INCLUDE[msCoName](../../includes/msconame-md.md)]パブリッシュサブスクライバー [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]で[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]のみ使用してください。 このプロシージャは、以降で[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]導入されたデータ型の列では使用できません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_repladdcolumn [ @source_object = ] 'source_object', [ @column = ] 'column' ]  
    [ , [ @typetext = ] 'typetext' ]  
    [ , [ @publication_to_add = ] 'publication_to_add' ]  
    [ , [ @from_agent = ] from_agent ]  
    [ , [ @schema_change_script = ] 'schema_change_script' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引数  
 [ @source_object =] '*source_object*'  
 追加する新しい列が含まれるテーブルアーティクルの名前を指定します。 *source_object*は**nvarchar (358**),、既定値はありません。  
  
 [ @column =] '*column*'  
 レプリケーション用に追加するテーブル内の列の名前を指定します。 *列*は**sysname**,、既定値はありません。  
  
 [ @typetext =] '*typetext*'  
 追加する列の定義を指定します。 *typetext*は**nvarchar (3000)** ,、既定値はありません。 たとえば、列 order_filled が追加されていて、それが NULL ではなく1つの文字フィールドで、既定値が**N**の場合、order_filled は column パラメーター、列の定義では、 **CHAR (1) not NULL 制約になります。constraint_name の既定**値は*typetext*パラメーター値になります。  
  
 [ @publication_to_add =] '*publication_to_add*'  
 新しい列を追加するパブリケーションの名前を指定します。 *publication_to_add*は**nvarchar (4000)** ,、既定値は**ALL**です。 **All**の場合、このテーブルを含むすべてのパブリケーションが影響を受けます。 場合*publication_to_add*が指定されている場合、このパブリケーションでは、新しい列が追加されます。  
  
 [ @from_agent =] *from_agent*  
 ストアドプロシージャがレプリケーションエージェントによって実行される場合はです。 *from_agent*は**int**,、既定値は**0**です。このストアドプロシージャがレプリケーションエージェントによって実行されるときに値**1**が使用され、その他のすべての場合は既定値**0**を使用します。  
  
 [ @schema_change_script =] '*schema_change_script*'  
 システムによって生成される[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]カスタムストアドプロシージャの変更に使用するスクリプトの名前とパスを指定します。 *schema_change_script*は**nvarchar (4000)** ,、既定値は NULL です。 レプリケーションでは、トランザクションレプリケーションで使用される1つ以上の既定のプロシージャを、ユーザー定義のカスタムストアドプロシージャで置き換えることができます。 *schema_change_script*は、sp_repladdcolumn を使用してレプリケートされたテーブルアーティクルに対してスキーマ変更が行われた後に実行され、次のいずれかの操作に使用できます。  
  
-   カスタムストアドプロシージャが自動的に再生成された場合、 *schema_change_script*を使用してこれらのカスタムストアドプロシージャを削除し、新しいスキーマをサポートするユーザー定義のカスタムストアドプロシージャに置き換えることができます。  
  
-   カスタムストアドプロシージャが自動的に再生成されない場合は、 *schema_change_script*を使用して、これらのストアドプロシージャを再生成したり、ユーザー定義のカスタムストアドプロシージャを作成したりできます。  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 スナップショットを無効にする機能を有効または無効にします。 *force_invalidate_snapshot*は**ビット**,、既定値は**1**です。  
  
 **1**に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。この場合、値**1**を指定すると、新しいスナップショットを作成する権限が与えられます。  
  
 **0**を指定すると、アーティクルへの変更によってスナップショットが無効になることはありません。  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 サブスクリプションを再初期化する機能を有効または無効にします。 *force_reinit_subscription*は**ビット**で、既定値は**0**です。  
  
 **0**に設定すると、アーティクルへの変更によってサブスクリプションが再初期化されることはありません。  
  
 **1**に設定すると、アーティクルへの変更によってサブスクリプションが再初期化される可能性があります。この場合、値**1**を指定すると、サブスクリプションの再初期化が許可されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 sp_repladdcolumn を実行できるのは、sysadmin 固定サーバー ロールまたは db_owner 固定データベース ロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server レプリケーションの非推奨の機能](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
