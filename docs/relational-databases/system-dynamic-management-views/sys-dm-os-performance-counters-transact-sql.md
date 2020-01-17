---
title: sys.dm_os_performance_counters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5c7b4d78f73af003e93bc662f10f1f95acda2b6a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265711"
---
# <a name="sysdmosperformancecounters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  サーバーで管理されているパフォーマンス カウンターごとに 1 行のデータを返します。 各パフォーマンス カウンターの詳細については、次を参照してください。 [SQL Server オブジェクトを使用して](../../relational-databases/performance-monitor/use-sql-server-objects.md)します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_performance_counters**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|このカウンターが属するカテゴリ。|  
|**counter_name**|**nchar(128)**|カウンターの名前。 これでカウンターの一覧から選択するトピックの名前は、カウンターの詳細を取得する[SQL Server オブジェクトを使用して](../../relational-databases/performance-monitor/use-sql-server-objects.md)します。 |  
|**instance_name**|**nchar(128)**|カウンターの特定のインスタンスの名前です。 多くの場合、データベース名が含まれています。|  
|**cntr_value**|**bigint**|カウンターの現在の値。<br /><br /> **注:** 1 秒あたりのカウンターでは、この値は累積的なです。 レートの値は、連続しない間隔で値をサンプリングして算出する必要があります。 2 つの連続するサンプル値の違いは、使用される時間間隔のレートと同じです。|  
|**cntr_type**|**int**|Windows パフォーマンス アーキテクチャによって定義されているカウンターのタイプします。 参照してください[WMI パフォーマンス カウンターの種類](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-performance-counter-types)Docs 上でパフォーマンス カウンターの種類の詳細については、Windows Server のドキュメント。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール インスタンスで Windows オペレーティング システムのパフォーマンス カウンターが表示されない場合は、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを使用して、パフォーマンス カウンターが無効になっていることを確認します。  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 戻り値が 0 行の場合、パフォーマンス カウンターが無効であることを意味します。 その場合は、セットアップ ログを参照して、エラー 3409 "このインスタンスの sqlctr.ini を再インストールし、インスタンス ログイン アカウントに適切なレジストリ権限が許可されていることを確認してください" を探す必要があります。  これは、パフォーマンス カウンターが無効であったことを示します。 3409 エラーの直前のエラーは、パフォーマンス カウンターを有効にする障害の根本原因を示す必要があります。 セットアップ ログ ファイルの詳細については、次を参照してください。[ビューと読み取り SQL Server セットアップ ログ ファイル](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)します。  
  
## <a name="permission"></a>権限

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
 
## <a name="examples"></a>使用例  
 次の例は、パフォーマンス カウンターの値を返します。  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>参照  
  [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


