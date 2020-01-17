---
title: プログラミング特有のタスク
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SQL Server Management Objects, tasks
- SMO [SQL Server], programming
- SMO [SQL Server], tasks
ms.assetid: a15949ef-88d9-4205-892e-0b66588b4fcc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0ba3ec14f7d94b493b5cc93e3b6b46f0565e38ab
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095209"
---
# <a name="programming-specific-tasks"></a>プログラミング特有のタスク
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO オブジェクトを使用したプログラミングに特有のタスクには、バックアップ、統計の監視、レプリケーション、インスタンス オブジェクトの管理、および構成オプションの設定など、特定の関数を使用したプログラムにのみ必要となる場合がある複雑な処理が含まれています。  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[SMO でのリンク サーバーの使用](../../../relational-databases/server-management-objects-smo/tasks/using-linked-servers-in-smo.md)|SMO が <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> オブジェクトを使用して OLE-DB サーバーをリンクする方法について説明します。|  
|[SMO での SQL Server の構成](../../../relational-databases/server-management-objects-smo/tasks/configuring-sql-server-in-smo.md)|SMO で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの構成設定を確認および変更する方法について説明します。|  
|[テーブルおよびインデックスのパーティション分割の使用](../../../relational-databases/server-management-objects-smo/tasks/using-table-and-index-partitioning.md)|SMO でインデックスおよびテーブル分割を使用する方法について説明します。|  
|[ファイル グループとファイルを使用したデータの格納](../../../relational-databases/server-management-objects-smo/tasks/using-filegroups-and-files-to-store-data.md)|SMO でファイル グループを使用する方法について説明します。|  
|[WMI プロバイダーを使用したサービスの管理とネットワーク設定](../../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)|構成管理用の WMI プロバイダーを表す [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オブジェクトを使用して、<xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> のインスタンスを追跡するいくつかの方法について説明します。|  
|[データベース オブジェクトでの作業](../../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-database-objects.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンス上のオブジェクトを表すインスタンス クラスを作成する方法について説明します。|  
|[ユーザー、ロール、およびログインの管理](../../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)|SMO でセキュリティ ロールを使用する方法について説明します。|  
|[権限の許可、取り消し、および拒否](../../../relational-databases/server-management-objects-smo/tasks/granting-revoking-and-denying-permissions.md)|SMO を使用して、ユーザーまたはロールのメンバーに対して権限の許可、取り消し、および拒否を行う方法について説明します。|  
|[暗号化の使用](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)|SMO で暗号化を使用してデータを保護する方法について説明します。|  
|[SQL Server エージェントでの自動管理タスクのスケジュール設定](../../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントを使用して、SMO のジョブの監視、レポート、およびスケジュール設定を行う方法について説明します。|  
|[データベースおよびトランザクション ログのバックアップと復元](../../../relational-databases/server-management-objects-smo/tasks/backing-up-and-restoring-databases-and-transaction-logs.md)|SMO でデータベースおよびトランザクション ログのバックアップと復元を行う方法について説明します。|  
|[スクリプトの作成](../../../relational-databases/server-management-objects-smo/tasks/scripting.md)|SMO で、オブジェクトのスクリプト化およびオブジェクト間の依存関係の検出を行う方法について説明します。|  
|[データの転送](../../../relational-databases/server-management-objects-smo/tasks/transferring-data.md)|SMO でデータを転送する方法について説明します。|  
|[データベース メールの使用](../../../relational-databases/server-management-objects-smo/tasks/using-database-mail.md)|SMO が電子メール サービスを利用する方法について説明します。|  
|[Service Broker の管理](../../../relational-databases/server-management-objects-smo/tasks/managing-service-broker.md)|SMO を使用して Service Broker を設定する方法について説明します。|  
|[XML スキーマの使用](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)|SMO で XML データ型を使用する方法について説明します。|  
|[シノニムの使用](../../../relational-databases/server-management-objects-smo/tasks/using-synonyms.md)|SMO でシノニムを作成する方法について説明します。|  
|[メッセージの使用](../../../relational-databases/server-management-objects-smo/tasks/using-messages.md)|システム メッセージを使用する方法、および個別のユーザー定義メッセージを定義する方法について説明します。|  
|[フルテキスト検索の実装](../../../relational-databases/server-management-objects-smo/tasks/implementing-full-text-search.md)|SMO でフルテキスト検索カタログおよびインデックスを実装する方法について説明します。|  
|[エンドポイントの実装](../../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md)|データベース ミラーリング、SOAP 要求、および Service Broker のペイロードを処理するためのエンドポイントを作成する方法について説明します。|  
|[統計の作成と更新](../../../relational-databases/server-management-objects-smo/tasks/creating-and-updating-statistics.md)|SMO でデータベース上の統計を設定および監視する方法について説明します。|  
|[イベントのトレースおよび再生](../../../relational-databases/server-management-objects-smo/tasks/tracing-and-replaying-events.md)|SMO で**trace**オブジェクトと**replay**オブジェクトを使用してイベントをトレースおよび再生する方法について説明します。|  
  
  
