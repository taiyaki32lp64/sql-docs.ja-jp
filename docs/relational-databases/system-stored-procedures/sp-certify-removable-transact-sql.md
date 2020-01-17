---
title: sp_certify_removable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_certify_removable_TSQL
- sp_certify_removable
dev_langs:
- TSQL
helpviewer_keywords:
- sp_certify_removable
ms.assetid: ca12767f-0ae5-4652-b523-c23473f100a1
author: stevestein
ms.author: sstein
ms.openlocfilehash: c39665f54a915282a6c59fe7d57b24d0cde0a5e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045930"
---
# <a name="sp_certify_removable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  リムーバブル メディア上でデータベースが配布用に正しく構成されているかどうか確認し、問題があればユーザーにレポートします。  
  
> **重要!!** [!INCLUDE[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) instead.  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbname'` 確認するデータベースを指定します。 *dbname*は**sysname**します。  
  
`[ @autofix = ] 'auto'` システム管理者に、データベースとすべてのデータベース オブジェクトの所有権を与え、ユーザーが作成したデータベース ユーザーと既定以外の権限を削除します。 *自動*は**nvarchar (4)** 、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 データベースが正しく構成されている場合**sp_certify_removable**次を実行します。  
  
-   ファイルをコピーできるように、データベースをオフラインに設定します。  
  
-   すべてのテーブルに関する統計を更新し、所有権やユーザーに関する問題をレポートする。  
  
-   データ ファイル グループを読み取り専用としてマークし、ファイルを読み取り専用メディアにコピーできるようにする。  
  
 システム管理者は、データベースとすべてのデータベース オブジェクトの所有者であることが必要です。 システム管理者が実行されているすべてのサーバー上に存在する既知のユーザー [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]し、データベースが後で配布され、インストールされているときに存在するが期待できます。  
  
 実行する場合**sp_certify_removable**せず、**自動**値とは、次の条件のいずれかに関する情報を返します。  
  
-   システム管理者は、データベース所有者ではありません。  
  
-   すべてのユーザーが作成したユーザーが存在します。  
  
-   システム管理者は、データベース内のすべてのオブジェクトを所有していません。  
  
-   既定値以外の権限が与えられている。  
  
 次の方法では、これらの条件を修正できます。  
  
-   使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ツールと手順、および実行し**sp_certify_removable**もう一度です。  
  
-   実行するだけで**sp_certify_removable**で、**自動**値。  
  
 このストアド プロシージャが、ユーザーおよびユーザーのアクセス許可のチェックだけに注意してください。 データベースにはグループを追加でき、そのグループに権限を与えることができます。 詳細については、「 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)と共に使用できるように構成する方法について説明します。  
  
## <a name="permissions"></a>アクセス許可  
 実行のアクセス許可がのメンバーに制限されます、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、`inventory` データベースを削除できるかどうかを確認します。  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_create_removable &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
