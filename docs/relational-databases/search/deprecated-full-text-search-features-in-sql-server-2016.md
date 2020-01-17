---
title: SQL Server 2016 の非推奨のフルテキスト検索機能
ms.custom: seo-lt-2019
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: daf20c621f00529313498c4802cd1d7dfce0fd8b
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056222"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2016"></a>SQL Server 2016 の非推奨のフルテキスト検索機能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、SQL Server でまだ使用できるものの、非推奨のフルテキスト検索機能について説明します。 これらの機能は今後のリリースで削除される予定です。 非推奨の機能を新しいアプリケーションで使用しないでください。  
  
非推奨の機能の使用は、**SQL Server:Deprecated Features** オブジェクトのパフォーマンス カウンターおよびトレース イベントを使用して監視します。 詳細については、「 [SQL Server オブジェクトの使用](../../relational-databases/performance-monitor/use-sql-server-objects.md)」を参照してください。  
  
## <a name="features-no-longer-supported"></a>機能は現在サポートされません  

  
|非推奨の機能|代替|機能名|機能 ID|  
|------------------------|-----------------|------------------|----------------|  
|FULLTEXTCATALOGPROPERTY プロパティ: LogSize|[なし] :|FULLTEXTCATALOGPROPERTY **('LogSize')**|211|  
|FULLTEXTSERVICEPROPERTY プロパティ<br /><br /> ConnectTimeout<br /><br /> DataTimeout|[なし] :|FULLTEXTSERVICEPROPERTY **('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY **('DataTimeout'** )|210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|sp_fulltext_service アクションの値: clean_up、connect_timeout、および data_timeout は 0 を返します|なし|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|sys.dm_fts_active_catalogs 列<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> ステータス<br /><br /> status_description<br /><br /> worker_count|[なし] :|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|sys.dm_fts_memory_buffers 列<br /><br /> row_count|[なし] :|dm_fts_memory_buffers.row_count|225|  
|sys.fulltext_catalogs 列<br /><br /> path<br /><br /> data_space_id<br /><br /> file_id 列|[なし] :|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server の今後のバージョンでサポートされない機能  
 以下のフルテキスト検索機能は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の次のバージョンではサポートされますが、その後のバージョンでは削除されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のどのバージョンであるかは決定していません。  
  
 **機能名** の値は、トレース イベントには ObjectName として表示され、パフォーマンス カウンターおよび sys.dm_os_performance_counters にはインスタンス名として表示されます。 **機能 ID** の値は、トレース イベントに ObjectId として表示されます。  
  
|非推奨の機能|代替|機能名|機能 ID|  
|------------------------|-----------------|------------------|----------------|  
|CONTAINS および CONTAINSTABLE 汎用 NEAR 演算子<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|カスタム NEAR 演算子<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,...*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,...*n*] )<br /><br /> [,<distance> [,<order>] ]<br /><br /> }<br /><br /> )<br /><br /> <distance> ::= {*integer* &#124; **MAX**}<br /><br /> <order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|CREATE FULLTEXT CATALOG オプション<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|[なし] :|CREATE FULLTEXT CATLOG IN PATH<br /><br /> [なし] :<sup>*</sup>|237<br /><br /> なし*|  
|DATABASEPROPERTYEX プロパティ: IsFullTextEnabled|[なし] :|DATABASEPROPERTYEX **('IsFullTextEnabled')**|202|  
|sp_detach_db オプション<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|[なし] :|sp_detach_db @keepfulltextindexfile|226|  
|sp_fulltext_service アクションの値: resource_usage には機能がありません。|なし|sp_fulltext_service @action=resource_usage|200|  
  
 &#42;**SQL Server:Deprecated Features** オブジェクトは、CREATE FULLTEXT CATLOG ON FILEGROUP *filegroup* の使用を監視しません。  
  
  
