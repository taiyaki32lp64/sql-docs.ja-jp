---
title: sp_registercustomresolver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_registercustomresolver
- sp_registercustomresolver_TSQL
helpviewer_keywords:
- sp_registercustomresolver
ms.assetid: 6d2b0472-0e1f-4005-833c-735d1940fe93
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0d003cccfa6fdedd0610ea34f15acb6ee1833e5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075735"
---
# <a name="sp_registercustomresolver-transact-sql"></a>sp_registercustomresolver (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ビジネス ロジック ハンドラーまたはマージ レプリケーションの同期処理中に呼び出すことができます (COM) ベースのカスタム リゾルバーを登録します。 このストアド プロシージャは、ディストリビューターで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_registercustomresolver [ @article_resolver = ] 'article_resolver'   
    [ , [ @resolver_clsid = ] 'resolver_clsid' ]  
    [ , [ @is_dotnet_assembly = ] 'is_dotnet_assembly' ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @article_resolver = ] 'article_resolver'` 登録されているカスタム ビジネス ロジックのフレンドリ名を指定します。 *article_resolver*は**nvarchar (255)** 、既定値はありません。  
  
`[ @resolver_clsid = ] 'resolver_clsid'` 登録されている COM オブジェクトの CLSID 値を指定します。 カスタム ビジネス ロジック*resolver_clsid*は**nvarchar (50)** 、既定値は NULL です。 このパラメーターの設定は有効な clsid またはビジネス ロジック ハンドラー アセンブリを登録するときに NULL に設定する必要があります。  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly'` 登録されているカスタム ビジネス ロジックの種類を指定します。 *is_dotnet_assembly*は**nvarchar (50)** 、既定値は FALSE。 **true**登録されているカスタム ビジネス ロジックがビジネス ロジック ハンドラー アセンブリであることを示します**false**は COM コンポーネントであることを示します。  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name'` ビジネス ロジック ハンドラーを実装するアセンブリの名前です。 *\@dotnet_assembly_name*は **nvarchar (255)** 既定値は NULL です。 マージ エージェントの実行可能ファイルがあるディレクトリ、マージ エージェントを同期的に起動するアプリケーションがあるディレクトリ、およびグローバル アセンブリ キャッシュ (GAC) の、いずれとも異なる場所にアセンブリが配置されている場合は、アセンブリの完全なパスを指定する必要があります。  
  
`[ @dotnet_class_name = ] 'dotnet_class_name'` オーバーライドするクラスの名前を指定<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>ビジネス ロジック ハンドラーを実装します。 形式で名前を指定する必要があります**Namespace.Classname**します。 *\@dotnet_class_name*は **nvarchar (255)** 既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_registercustomresolver**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_registercustomresolver**します。  
  
## <a name="see-also"></a>関連項目  
 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [マージ アーティクルのカスタム競合回避モジュールの実装](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
