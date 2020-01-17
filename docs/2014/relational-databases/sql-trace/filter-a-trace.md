---
title: トレースへのフィルターの適用 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 381007cb26f74cdf945900436d8a9fcea5a4ef39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714719"
---
# <a name="filter-a-trace"></a>トレースへのフィルターの適用
  フィルターを使用すると、トレースに出力するイベントを制限することができます。 フィルターが設定されていない場合は、選択したイベント クラスのすべてのイベントがトレースに出力されます。 たとえば、トレースに出力する Windows ユーザーとして特定のユーザー名を指定すると、それらのユーザーのデータのみが出力されます。  
  
 トレースのフィルター設定は必須ではありません。 ただし、フィルターを設定すると、トレース中に発生するオーバーヘッドを低減できます。 フィルターによって、データを絞り込むことができ、パフォーマンス分析および監査が簡略化されます。  
  
 トレースに出力するイベント データを制限するには、必要なデータだけがトレースに記録されるようにイベントのトレース条件を選択します。 たとえば、特定のアプリケーションの動作状況をトレースの対象としたり、トレースから除外したりできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] でトレースを作成する場合、既定では、この Profiler 自身の動作状況はトレースから除外されます。  
  
 たとえば、クエリを監視して、実行に長時間かかるバッチを調べる場合、イベントのトレース条件を設定することで、実行時間が 30 秒を超えるバッチだけを監視できます (CPU 時間の最小値は 30,000 ミリ秒です)。  
  
## <a name="filter-creation-guidelines"></a>フィルター作成のガイドライン  
 トレースにフィルターを適用するには、次の手順を実行します。  
  
1.  トレースの対象とするイベントを決めます。  
  
2.  必要な情報を保存するデータおよびデータ列を決めます。  
  
3.  必要なデータのサブセットを決め、そのデータのサブセットに基づいてフィルターを設定します。  
  
 たとえば、ある一定の時間よりも長くかかるイベントをトレースで出力するとします。 その場合、 **Duration** データ列が 300 ミリ秒よりも長いイベントを出力するトレースを作成できます。 300 ミリ秒以内に完了したイベントはトレースから除外されます。  
  
 フィルターは、SQL Server Profiler または Transact-SQL ストアド プロシージャを使用して作成できます。  
  
 **トレース テンプレートを使用してイベントにフィルターを適用するには**  
  
 [トレース内のイベントへのフィルターの適用 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
 [トレース フィルターの設定 &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
 **フィルターを変更するには**  
  
 [フィルターの変更 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 フィルターを適用できるかどうかは、データ列によって異なります。 一部のデータ列にはフィルターを適用できません。 フィルターの適用が可能なデータ列では、次の表に示す関係演算子を使用してフィルターを指定できます。  
  
|関係演算子|演算子記号|説明|  
|-------------------------|---------------------|-----------------|  
|Like|Like|イベントのトレース データが入力したテキストと同じでなければならないことを指定します。 複数の値を指定できます。|  
|パターンに一致しない|パターンに一致しない|イベントのトレース データが入力したテキストと同じであってはならないことを指定します。 複数の値を指定できます。|  
|[等しい]|=|イベントのトレース データが入力した値と等しくなければならないことを指定します。 複数の値を指定できます。|  
|等しくない|<>|イベントのトレース データが入力した値と等しくあってはならないことを指定します。 複数の値を指定できます。|  
|より大きい|>|イベントのトレース データが入力した値よりも大きくなければならないことを指定します。|  
|以上|>=|イベントのトレース データが入力した値以上でなければならないことを指定します。|  
|次の値未満|<|イベントのトレース データが入力した値よりも小さくなければならないことを指定します。|  
|以下|<=|イベントのトレース データが入力した値以下でなければならないことを指定します。|  
  
 次の表は、フィルターを適用できるデータ列と利用可能な関係演算子の一覧です。  
  
|データ列|関係演算子|  
|------------------|--------------------------|  
|**ApplicationName**|LIKE、NOT LIKE|  
|**BigintData1**|=、<>、>=、<=|  
|**BigintData2**|=、<>、>=、<=|  
|**BinaryData**|このデータ列のイベントにフィルターを適用するには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用します。 詳細については、「 [SQL Server Profiler でのトレースへのフィルターの適用](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)」を参照してください。|  
|**ClientProcessID**|=、<>、>=、<=|  
|**ColumnPermissions**|=、<>、>=、<=|  
|**CPU**|=、<>、>=、<=|  
|**DatabaseID**|=、<>、>=、<=|  
|**DatabaseName**|LIKE、NOT LIKE|  
|**DBUserName**|LIKE、NOT LIKE|  
|**Duration**|=、<>、>=、\<=|  
|**EndTime**|>=、<=|  
|**Error**|=、<>、>=、<=|  
|**EventSubClass**|=、<>、>=、<=|  
|**FileName**|LIKE、NOT LIKE|  
|**GUID**|このデータ列のイベントにフィルターを適用するには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用します。 詳細については、「 [SQL Server Profiler でのトレースへのフィルターの適用](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)」を参照してください。|  
|**Handle**|=、<>、>=、<=|  
|**HostName**|LIKE、NOT LIKE|  
|**IndexID**|=、<>、>=、<=|  
|**IntegerData**|=、<>、>=、<=|  
|**IntegerData2**|=、<>、>=、<=|  
|**IsSystem**|=、<>、>=、<=|  
|**LineNumber**|=、<>、>=、<=|  
|**LinkedServerName**|LIKE、NOT LIKE|  
|**LoginName**|LIKE、NOT LIKE|  
|**LoginSid**|このデータ列のイベントにフィルターを適用するには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用します。 詳細については、「 [SQL Server Profiler でのトレースへのフィルターの適用](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)」を参照してください。|  
|**MethodName**|LIKE、NOT LIKE|  
|**モード**|=、<>、>=、<=|  
|**NestLevel**|=、<>、>=、<=|  
|**NTDomainName**|LIKE、NOT LIKE|  
|**NTUserName**|LIKE、NOT LIKE|  
|**Exchange Spill**|=、<>、>=、<=|  
|**ObjectID2**|=、<>、>=、<=|  
|**ObjectName**|LIKE、NOT LIKE|  
|**ObjectType**|=、<>、>=、<=|  
|**Offset**|=、<>、>=、<=|  
|**OwnerID**|=、<>、>=、<=|  
|**OwnerName**|LIKE、NOT LIKE|  
|**ParentName**|LIKE、NOT LIKE|  
|**権限**|=、<>、>=、<=|  
|**ProviderName**|LIKE、NOT LIKE|  
|**Reads**|=、<>、>=、<=|  
|**RequestID**|=、<>、>=、<=|  
|**RoleName**|LIKE、NOT LIKE|  
|**RowCounts**|=、<>、>=、<=|  
|**SessionLoginName**|LIKE、NOT LIKE|  
|**Severity**|=、<>、>=、<=|  
|**SourceDatabaseID**|=、<>、>=、<=|  
|**SPID**|=、<>、>=、\<=|  
|**SqlHandle**|このデータ列のイベントにフィルターを適用するには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用します。 詳細については、「 [SQL Server Profiler でのトレースへのフィルターの適用](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)」を参照してください。|  
|**StartTime**|>=、<=|  
|**State**|=、<>、>=、<=|  
|**成功**|=、<>、>=、<=|  
|**TargetLoginName**|LIKE、NOT LIKE|  
|**TargetLoginSid**|このデータ列のイベントにフィルターを適用するには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用します。 詳細については、「 [SQL Server Profiler でのトレースへのフィルターの適用](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)」を参照してください。|  
|**TargetUserName**|LIKE、NOT LIKE|  
|**TextData** <sup>1</sup>|LIKE、NOT LIKE|  
|**TransactionID**|=、<>、>=、<=|  
|**型**|=、<>、>=、<=|  
|**Writes**|=、<>、>=、<=|  
|**XactSequence**|=、<>、>=、<=|  
  
 <sup>1</sup>からイベントをトレースしている場合、 **osql**ユーティリティまたは**sqlcmd**ユーティリティでは、常に追加 **%** でフィルターする、 **TextData**データ列。  
  
 セキュリティ対策として、SQL トレースは、パスワードに影響を与えるセキュリティ関連ストアド プロシージャの情報をトレースの対象から自動的に除外します。 このセキュリティ メカニズムは変更不可能で、常に有効な状態になっています。 これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上でのすべての動作状況をトレースする権限を持たないユーザーがパスワードを取得するのを防ぎます。  
  
 監視されるのは次のセキュリティ関連ストアド プロシージャですが、 **TextData** データ列には出力されません。  
  
 [sp_addapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addapprole-transact-sql)  
  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)  
  
 [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)  
  
 [sp_adddistributor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)  
  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql)  
  
 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)  
  
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)  
  
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)  
  
 [sp_addremotelogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql)  
  
 [sp_addsubscriber &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql)  
  
 [sp_approlepassword &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-approlepassword-transact-sql)  
  
 [sp_changedistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)  
  
 [sp_changesubscriber &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql)  
  
 [sp_dsninfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dsninfo-transact-sql)  
  
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)  
  
 [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)  
  
 [sp_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)  
  
 [sp_setapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql)  
  
  
