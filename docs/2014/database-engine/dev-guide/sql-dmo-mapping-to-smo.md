---
title: SMO へのマッピングを SQL-DMO |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a6273032f88807291bfc7024f1abcdbd1440073
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780682"
---
# <a name="sql-dmo-mapping-to-smo"></a>SQL-DMO の SMO へのマッピング
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、SQL 分散管理オブジェクト (SQL-DMO) は含まれなくなりました。SQL-DMO アプリケーションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) で使用できるように変換する必要があります。 SMO オブジェクト モデルは SQL-DMO に似ているため、大半の SQL-DMO オブジェクトは SMO と同じ名前のオブジェクトにマップされます。 ただし、一部の SQL-DMO オブジェクトは SMO への移行で変更または削除されました。 次の表は、SMO に直接変換されなかった SQL-DMO オブジェクトに対して推奨される操作を示しています。  
  
|SQL-DMO オブジェクト|SMO でのアクション|  
|---------------------|-------------------|  
|View2 オブジェクト|移動<xref:Microsoft.SqlServer.Management.Smo.Agent>Namespace です。|  
|AlertSystem オブジェクト|移動<xref:Microsoft.SqlServer.Management.Smo.Agent>Namespace です。|  
|Application オブジェクト|削除されます。|  
|Backup オブジェクトおよび Backup2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Backup> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> オブジェクト。|  
|BackupDevice オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.BackupDevice> オブジェクト|  
|BulkCopy オブジェクトおよび BulkCopy2 オブジェクト|削除され、<xref:Microsoft.SqlServer.Management.Smo.Transfer> オブジェクトによって置き換えられました。|  
|Category オブジェクト|移動<xref:Microsoft.SqlServer.Management.Smo.Agent>Namespace です。 <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory> オブジェクト、<xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory> オブジェクト、および <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory> オブジェクトによって置き換えられました。|  
|Check オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Check> オブジェクト|  
|Column オブジェクトおよび Column2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Column> オブジェクト。|  
|Configuration オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Configuration> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase> オブジェクト。|  
|ConfigValue オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> オブジェクト。|  
|Database オブジェクトおよび Database2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクト。|  
|DatabaseRole オブジェクトおよび DatabaseRole2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> オブジェクト。|  
|DBFile オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.DataFile> オブジェクト。|  
|DBOption オブジェクトおよび DBOption2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions> オブジェクトに移動されました。|  
|Default オブジェクトおよび Default2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Default> オブジェクト。|  
|DistributionArticle オブジェクトおよび DistributionArticle2 オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|DistributionDatabase オブジェクトおよび DistributionDatabase2 オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|DistributionPublication オブジェクトおよび DistributionPublication2 オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|DistributionSubscription オブジェクトおよび DistributionSubscription2 オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|Distributor オブジェクトおよび Distributor2 オブジェクト|移動、<xref:Microsoft.SqlServer.Replication>名前空間。|  
|DRIDefault オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> 名前空間に移動されました。|  
|FileGroup オブジェクトおよび FileGroup2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.FileGroup> オブジェクト。|  
|FullTextCatalog オブジェクトおよび FullTextCatalog2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex> オブジェクト。|  
|Index オブジェクトおよび Index2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Index> オブジェクト|  
|IntegratedSecurity オブジェクト|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> 名前空間の <xref:Microsoft.SqlServer.Management.Common> オブジェクトに機能が移動されました。|  
|Job オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Agent.Job> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|JobFilter オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|JobHistoryFilter オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|JobSchedule オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|JobServer オブジェクトおよび JobServer2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|JobStep オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|Key オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.ForeignKey> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.Index> オブジェクト。|  
|LinkedServer オブジェクトおよび LinkedServer2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> オブジェクト。|  
|LinkedServerLogin オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> オブジェクト。|  
|LogFile オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.LogFile> オブジェクト。|  
|Login オブジェクトおよび Login2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Login> オブジェクト。|  
|MergeArticle オブジェクトおよび MergeArticle2 オブジェクト|<xref:Microsoft.SqlServer.Replication.MergeArticle> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|MergeDynamicSnapshotJob オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|MergePublication オブジェクトおよび MergePublication2 オブジェクト|<xref:Microsoft.SqlServer.Replication.MergePublication> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|MergePullSubscription オブジェクトおよび MergePullSubscription2 オブジェクト|<xref:Microsoft.SqlServer.Replication.MergePullSubscription> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|MergeSubscription オブジェクト|<xref:Microsoft.SqlServer.Replication.MergeSubscription> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|MergeSubsetFilter オブジェクト|移動`N:Microsoft.SqlServer.Replication`名前空間。|  
|NameList オブジェクト|削除されます。 代替機能が <xref:Microsoft.SqlServer.Management.Smo.Scripter> オブジェクトで提供されています。|  
|Operator オブジェクト|移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|Permission オブジェクトおよび Permission2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.ServerPermission> オブジェクト、<xref:Microsoft.SqlServer.Management.Smo.DatabasePermission> オブジェクト、<xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> オブジェクト、および <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission> オブジェクト。|  
|Property オブジェクト|`Property` オブジェクト。|  
|Publisher オブジェクトおよび Publisher2 オブジェクト|<xref:Microsoft.SqlServer.Replication.ReplicationServer> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|QueryResults オブジェクトおよび QueryResults2 オブジェクト|<xref:System.Data.DataTable> システム オブジェクトまたは <xref:System.Data.DataSet> システム オブジェクトによって置き換えられました。|  
|RegisteredServer オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|RegisteredSubscriber オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|Registry オブジェクトおよび Registry2 オブジェクト|削除されます。|  
|RemoteLogin オブジェクト|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト。 Common 名前空間に移動されました。|  
|RemoteServer オブジェクトおよび RemoteServer2 オブジェクト|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Common>名前空間。|  
|レプリケーション オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|ReplicationDatabase オブジェクトおよび ReplicationDatabase2 オブジェクト|<xref:Microsoft.SqlServer.Replication.ReplicationDatabase> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|ReplicationSecurity オブジェクト|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト。 移動<xref:Microsoft.SqlServer.Management.Common>名前空間。|  
|ReplicationStoredProcedure オブジェクトおよび ReplicationStoredProcedure2 オブジェクト|<xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|ReplicationTable オブジェクトおよび ReplicationTable2 オブジェクト|<xref:Microsoft.SqlServer.Replication.ReplicationTable> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|Restore オブジェクトおよび Restore2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Restore> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase> オブジェクト。|  
|Rule オブジェクトおよび Rule2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクト|  
|Schedule オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|ServerGroup オブジェクト|削除されます。|  
|ServerRole オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.ServerRole> オブジェクト。|  
|SQLObjectList オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject> 配列。|  
|SQLServer オブジェクトおよび SQLServer2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト。|  
|StoredProcedure オブジェクトおよび StoredProcedure2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> および <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> オブジェクト|  
|Subscriber オブジェクトおよび Subscriber2 オブジェクト|移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|SystemDatatype オブジェクトおよび SystemDataType2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.DataType> オブジェクト。|  
|Table オブジェクトおよび Table2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクト。|  
|TargetServer オブジェクト|移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|TargetServerGroup オブジェクト|移動<xref:Microsoft.SqlServer.Management.Smo.Agent>名前空間。|  
|TransactionLog オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトに機能が移動されました。|  
|TransArticle オブジェクトおよび TransArticle2 オブジェクト|<xref:Microsoft.SqlServer.Replication.TransArticle> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|Transfer メソッドと Transfer2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Transfer> オブジェクト。|  
|TransPublication オブジェクトおよび TransPublication2 オブジェクト|<xref:Microsoft.SqlServer.Replication.TransPublication> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|TransPullSubscription オブジェクトおよび TransPullSubscription2 オブジェクト|<xref:Microsoft.SqlServer.Replication.TransPullSubscription> オブジェクト。 移動<xref:Microsoft.SqlServer.Replication>名前空間。|  
|Trigger オブジェクトおよび Trigger2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.Trigger> オブジェクト。|  
|User オブジェクトおよび User2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.User> オブジェクト。|  
|UserDefinedDatatype オブジェクトおよび UserDefinedDataType2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> オブジェクト。|  
|UserDefinedFunction オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter> オブジェクト。|  
|View オブジェクトおよび View2 オブジェクト|<xref:Microsoft.SqlServer.Management.Smo.View> オブジェクト。|  
  
## <a name="see-also"></a>参照  
 [SQL Server 管理オブジェクト &#40;SMO&#41; プログラミング ガイド](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
