---
title: sp_enumcustomresolvers (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumcustomresolvers
- sp_enumcustomresolvers_TSQL
helpviewer_keywords:
- sp_enumcustomresolvers
ms.assetid: 81bd0d3a-48dc-42b1-b662-c630f61fc630
author: stevestein
ms.author: sstein
ms.openlocfilehash: 361a0d8e47372612eddf40cdf1663df2e70da0a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124630"
---
# <a name="sp_enumcustomresolvers-transact-sql"></a>sp_enumcustomresolvers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  すべての使用可能なビジネス ロジック ハンドラーと、ディストリビューターで登録済みのカスタム競合回避モジュールの一覧を返します。 このストアド プロシージャは、任意のデータベースのパブリッシャーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_enumcustomresolvers [ [ @distributor =] 'distributor']  
```  
  
## <a name="arguments"></a>引数  
`[ @distributor = ] 'distributor'` カスタム競合回避モジュールが配置されているディストリビューターの名前です。 *ディストリビューター*は**sysname**、既定値は NULL です。 *このパラメーターは非推奨し、将来のリリースで削除される予定です。*  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**article_resolver**|**nvarchar (255)**|ビジネス ロジック ハンドラーまたは競合リゾルバーのフレンドリ名。|  
|**resolver_clsid**|**nvarchar (50)**|COM ベースの競合回避モジュールのクラス ID (CLSID) です。 ビジネス ロジック ハンドラーでは、この列は、0 の CLSID 値を返します。|  
|**is_dotnet_assembly**|**bit**|ビジネス ロジック ハンドラーに対する登録かどうかを示します。<br /><br /> **0** COM ベース競合回避モジュールを =<br /><br /> **1**ビジネス ロジック ハンドラーを =|  
|**dotnet_assembly_name**|**nvarchar (255)**|ビジネス ロジック ハンドラーを実装している [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework アセンブリの名前です。|  
|**dotnet_class_name**|**nvarchar (255)**|オーバーライドするクラスの名前を指定<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>ビジネス ロジック ハンドラーを実装します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_enumcustomresolvers**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールおよび**db_owner**固定データベース ロールが実行できる**sp_enumcustomresolvers**します。  
  
## <a name="see-also"></a>関連項目  
 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [マージ アーティクルのカスタム競合回避モジュールの実装](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
