---
title: システム互換性ビュー (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compatibility views [SQL Server]
- system tables [SQL Server], compatibility views
- type IDs [SQL Server]
- system views [SQL Server], compatibility
- metadata [SQL Server], views
- backward compatibility [SQL Server], compatibility views
- compatibility [SQL Server], compatibility views
- backward compatibility [SQL Server], system tables
- compatibility [SQL Server], system tables
- user IDs [SQL Server]
ms.assetid: 8e4624f5-9d36-4ce7-9c9e-1fe010fa2122
author: rothja
ms.author: jroth
ms.openlocfilehash: 466dc68da1c5cef56a7debe3953ba38956bb2993
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018036"
---
# <a name="system-compatibility-views-transact-sql"></a>システム互換性ビュー (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  以前のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の多くのシステム テーブルは、一連のビューとして実装されるようになりました。 これらのビューは互換性ビューと呼ばれ、旧バージョンとの互換性のためだけに用意されています。 互換性ビューでは、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] で利用できるメタデータと同じメタデータを利用できますが、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降で導入された機能に関連するメタデータは利用できません。 したがって、[!INCLUDE[ssSB](../../includes/sssb-md.md)] やパーティションなどの新機能を使用するときは、カタログ ビューを使用するように切り替える必要があります。  
  
 カタログ ビューへアップグレードするもう 1 つの理由としては、ユーザー ID および型 ID を格納する互換性ビューの列では NULL が返されるか算術オーバーフローが発生する可能性があることが挙げられます。 これは、32,767 を超えるユーザー、グループ、およびロール、および 32,767 のデータ型を作成するためです。 たとえば、32,768 人のユーザーを作成し、次のクエリを実行した場合:`SELECT * FROM sys.sysusers`します。 ここで ARITHABORT が ON に設定されている場合、クエリは算術オーバーフロー エラーで失敗します。 ARITHABORT が OFF に設定されている場合、 **uid**列は NULL を返します。  
  
 これらの問題を避けるためには、ユーザー Id の数の増加を処理し、Id を入力できますが、新しいカタログ ビューを使用することをお勧めします。 次の表に、このオーバーフローが発生する可能性のある列を示します。  
  
|列名|互換性ビュー|SQL Server 2005 ビュー|  
|-----------------|------------------------|--------------------------|  
|**xusertype**|**syscolumns**|**sys.columns**|  
|**usertype**|**syscolumns**|**sys.columns**|  
|**memberuid**|**sysmembers**|**sys.database_role_members**|  
|**groupuid**|**sysmembers**|**sys.database_role_members**|  
|**uid**|**sysobjects**|**sys.objects**|  
|**uid**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**権限の許可者**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**xusertype**|**systypes**|**sys.types**|  
|**uid**|**systypes**|**sys.types**|  
|**uid**|**sysusers**|**sys.database_principals**|  
|**altuid**|**sysusers**|**sys.database_principals**|  
|**gid**|**sysusers**|**sys.database_principals**|  
|**uid**|**syscacheobjects**|**sys.dm_exec_plan_attributes**|  
|**uid**|**sysprocesses**|**sys.dm_exec_requests**|  
  
 システムでは、SQL Server 2000 で非推奨と発表されたテーブル、ユーザー データベースで参照された場合、(など**syslanguages**または**syscacheobjects**)、バック互換性ビューにバインドされますが、**sys**スキーマ。 以降、SQL Server 2000 システム テーブルは、複数のバージョンの非推奨とされましたが、この変更には、重大な変更はありません。  
  
 例:ユーザーというユーザー テーブルを作成する場合**syslanguages**ユーザー データベース、SQL Server 2008 で、ステートメントで`SELECT * from dbo.syslanguages;`そのデータベースの値を返す、ユーザー テーブルから。 SQL Server 2012 以降では、この演習用データが返されます、システム ビューから**sys.syslanguages**します。  
  
## <a name="see-also"></a>関連項目  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
