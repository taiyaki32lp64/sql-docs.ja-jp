---
title: sp_pdw_remove_network_credentials
titleSuffix: Azure SQL Data Warehouse
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.subservice: design
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7068beee49260db17e7b8f704e5aba316deb6ea3
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844442"
---
# <a name="sp_pdw_remove_network_credentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  これにより、ネットワークファイル共有にアクセスするために [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] に格納されているネットワーク資格情報が削除されます。 たとえば、このストアドプロシージャを使用すると、独自のネットワーク内に存在するサーバーでバックアップ操作と復元操作を実行するために [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] のアクセス許可を削除できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>引数  
 '*target_server_name*'  
 対象サーバーのホスト名または IP アドレスを指定します。 このサーバーにアクセスするための資格情報は、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]から削除されます。 これによって、自分のチームによって管理される実際の対象サーバーのアクセス許可が変更または削除されることはありません。  
  
 *target_server_name*は nvarchar () として定義されています。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 **ALTER SERVER STATE**権限が必要です。  
  
## <a name="error-handling"></a>エラー処理  
 [制御] ノードおよびすべての計算ノードで資格情報の削除が成功しなかった場合に、エラーが発生します。  
  
## <a name="general-remarks"></a>全般的な解説  
 このストアドプロシージャは、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]の NetworkService アカウントからネットワーク資格情報を削除します。 NetworkService アカウントは、コントロールノードとコンピューティングノードで SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスを実行します。 たとえば、バックアップ操作を実行すると、制御ノードと各コンピューティングノードは、NetworkService アカウントの資格情報を使用して対象サーバーにアクセスします。  
  
## <a name="metadata"></a>メタデータ  
 すべての資格情報を一覧表示し、資格情報が削除されたことを確認するには、 [dm_pdw_network_credentials &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)を使用します。  
  
 資格情報を追加するには、 [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)を使用します。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. データベースバックアップを実行するための資格情報を削除する  
 次の例では、10.192.147.63 の IP アドレスを持つ対象サーバーにアクセスするためのユーザー名とパスワードの資格情報を削除します。  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

