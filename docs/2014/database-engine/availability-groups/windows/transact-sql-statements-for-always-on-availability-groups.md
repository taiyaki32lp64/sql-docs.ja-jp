---
title: AlwaysOn 可用性グループ (SQL Server) 用の TRANSACT-SQL ステートメントの概要 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: 184d0a81-2259-4db9-9d0d-01aac0b502c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f635faa05d7d77a50d31491b1bab9b16875e728c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813825"
---
# <a name="overview-of-transact-sql-statements-for-alwayson-availability-groups-sql-server"></a>AlwaysOn 可用性グループの Transact-SQL ステートメントの概要 (SQL Server)
  このトピックでは、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] の配置のほか、可用性グループ、可用性レプリカ、および可用性データベースの作成と管理をサポートする [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ステートメントについて説明します。  
  
  
##  <a name="CreateEndpoint"></a> CREATE ENDPOINT  
 [CREATE ENDPOINT ...FOR DATABASE_MIRRORING](/sql/t-sql/statements/create-endpoint-transact-sql) は、サーバー インスタンス上にデータベース ミラーリング エンドポイントが存在しない場合に、データベース ミラーリング エンドポイントを作成します。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] またはデータベース ミラーリングの配置を検討しているすべてのサーバー インスタンスには、データベース ミラーリング エンドポイントが必要です。  
  
 このステートメントは、エンドポイントの作成先となるサーバー インスタンス上で実行します。 特定のサーバー インスタンスに対して作成できるデータベース ミラーリング エンドポイントは 1 つだけです。 詳細については、「 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
##  <a name="CreateAG"></a> CREATE AVAILABILITY GROUP  
 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql) は、新しい可用性グループと、必要に応じて可用性グループのリスナーを作成します。 少なくとも、初期プライマリ レプリカとなるローカル サーバー インスタンスを指定する必要があります。 必要に応じて、セカンダリ レプリカを 4 つまで指定することもできます。  
  
 新しい可用性グループの初期プライマリ レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスで CREATE AVAILABILITY GROUP を実行します。 このサーバー インスタンスは、Windows Server フェールオーバー クラスター (WSFC) のノードに存在する必要があります (詳細については、次を参照してください。[前提条件、制限事項、および AlwaysOn 可用性グループの推奨事項&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)します。  
  
##  <a name="AlterAG"></a> ALTER AVAILABILITY GROUP  
 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) は、既存の可用性グループまたは可用性グループ リスナーの変更と、可用性グループのフェールオーバーをサポートします。  
  
 現在のプライマリ レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスで ALTER AVAILABILITY GROUP を実行します。  
  
##  <a name="AlterDb"></a> ALTER DATABASE ...SET HADR ...  
 ALTER DATABASE ステートメントの [SET HADR](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) 句のオプションを使用すると、セカンダリ データベースを対応するプライマリ データベースの可用性グループに参加させたり、参加データベースを削除したりできます。さらに、参加データベースでのデータ同期化の削除やデータ同期化の再開も行うことができます。  
  
##  <a name="DropAG"></a> DROP AVAILABILITY GROUP  
 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) は、指定された可用性グループとそのすべてのレプリカを削除します。 DROP AVAILABILITY GROUP は、WSFC フェールオーバー クラスター内の任意の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ノードから実行できます。  
  
##  <a name="Restrictions"></a> AVAILABILITY GROUP Transact-SQL ステートメントの制限事項  
 CREATE AVAILABILITY GROUP、ALTER AVAILABILITY GROUP、および DROP AVAILABILITY GROUP の各 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントには、次の制限があります。  
  
-   DROP AVAILABILITY GROUP を除き、これらのステートメントを実行するには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンス上で HADR サービスが有効になっている必要があります。 詳細については、「[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)」を参照してください。  
  
-   これらのステートメントは、トランザクションまたはバッチ内で実行することはできません。  
  
-   障害発生後のクリーンアップについてはベスト エフォートとなります。これらのステートメントでは、障害発生時にすべての変更が確実にロールバックされるという保証はありません。 ただし、システム的には、クリーンに処理し、部分的な障害については無視するようになっています。  
  
-   これらのステートメントは、式または変数をサポートしていません。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを実行したときに、別の可用性グループ アクションまたは復旧が進行中であった場合は、エラーが返されます。 必要に応じて、アクションまたは復旧の完了を待ってステートメントを再試行してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
