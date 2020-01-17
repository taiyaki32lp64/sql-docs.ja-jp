---
title: ad hoc distributed queries サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- OPENROWSET function, ad hoc distributed queries option
- Ad Hoc Distributed Queries option
- ad hoc distributed queries
- 7415 (Database Engine Error)
- OPENDATASOURCE function, ad hoc distributed queries option
- ad hoc access
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 04c2ea76808c2fa98e933021af93481c829baa21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813485"
---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>ad hoc distributed queries サーバー構成オプション
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定では、OPENROWSET および OPENDATASOURCE を使用したアドホックな分散クエリは実行できません。 このオプションを 1 に設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でアドホック アクセスを実行できます。 このオプションを設定しなかった場合または 0 に設定した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でアドホック アクセスを実行できません。  
  
 アドホック分散クエリの実行時には、OLE DB を使用するリモート データ ソースへの接続に OPENROWSET 関数および OPENDATASOURCE 関数が使用されます。 OPENROWSET 関数および OPENDATASOURCE 関数は、アクセス頻度の低い OLE DB データ ソースを参照する目的のみに使用してください。 何度もアクセスするデータ ソースに対しては、リンク サーバーを定義してください。  
  
> [!IMPORTANT]  
>  アドホック名を使用できるようにすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への認証済みログインであればプロバイダーにアクセスできるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の管理者は、ローカル ログインからアクセスされても安全なプロバイダーに対してのみ、この機能を有効にしてください。  
  
## <a name="remarks"></a>コメント  
 **アドホック分散クエリ**を有効にせずにアドホック接続を試みると、次のエラーが発生します: メッセージ 7415、レベル 16、状態 1、行 1  
  
 OLE DB プロバイダー 'Microsoft.ACE.OLEDB.12.0' へのアドホック アクセスが拒否されました。 リンク サーバー経由でこのプロバイダーにアクセスしてください。  
  
## <a name="examples"></a>使用例  
 次の例では、アドホック分散クエリを有効にし、 `Seattle1` 関数を使用して `OPENROWSET` という名前のサーバーにクエリを実行します。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
sp_configure 'Ad Hoc Distributed Queries', 1;  
RECONFIGURE;  
GO  
  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](/sql/t-sql/functions/opendatasource-transact-sql)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
  
