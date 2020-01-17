---
title: msdb データベース | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, msdb database
- alerts [SQL Server], msdb database
- jobs [SQL Server], msdb database
- msdb database [SQL Server]
ms.assetid: 5032cb2d-65a0-40dd-b569-4dcecdd58ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cee4c5d802447488930ffd04d698edcd2015e86b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871713"
---
# <a name="msdb-database"></a>msdb データベース
  **msdb** データベースは、警告やジョブのスケジュール設定のために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって使用されます。また、その他の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[ssSB](../../includes/sssb-md.md)]、データベース メールなどの機能でも使用されます。  
  
 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、オンラインのバックアップおよび復元の履歴をすべて **msdb**データベース内のテーブルで自動的に管理します。 この情報には、バックアップの実行者名、バックアップ日時、バックアップが格納されているデバイスやファイルなどが含まれます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、この情報を使用して、データベースを復元してトランザクション ログ バックアップを適用するプランを立てます。 すべてのデータベースに対するバックアップ イベントは、独自のアプリケーションやサード パーティのツールで発生した場合にも記録されます。 たとえば、SMO (SQL Server 管理オブジェクト) オブジェクトを呼び出してバックアップ操作を行う [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] アプリケーションの場合、イベントは **msdb** システム テーブル、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログ、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに記録されます。 **msdb**に格納される情報を保護するために、 **msdb** トランザクション ログをフォールト トレラント ストレージに置くことを検討するようにお勧めします。  
  
 既定では、 **msdb** は単純復旧モデルを使用します。 [バックアップおよび復元の履歴](../backup-restore/backup-history-and-header-information-sql-server.md)テーブルを使用する場合は、**msdb** の完全復旧モデルを使用することをお勧めします。 詳細については、「[復旧モデル &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールまたはアップグレードするとき、Setup.exe を使用してシステム データベースを再構築すると必ず、**msdb** の復旧モデルは自動的に simple に設定されることに注意してください。  
  
> [!IMPORTANT]  
>  データベースのバックアップや復元など、**msdb** を更新する操作の後は、**msdb** をバックアップすることをお勧めします。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。  
  
## <a name="physical-properties-of-msdb"></a>msdb データベースの物理プロパティ  
 **msdb** データベースのデータとログ ファイルの初期構成値を次の表に示します。 これらのファイルのサイズは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のエディションによって多少異なる場合があります。  
  
|ファイル|論理名|物理名|ファイル拡張|  
|----------|------------------|-------------------|-----------------|  
|プライマリ データ|MSDBData|MSDBData.mdf|ディスクがいっぱいになるまで 10% ずつ自動拡張|  
|Log|MSDBLog|MSDBLog.ldf|最大 2 TB まで 10% ずつ自動拡張|  
  
 **msdb** データベースまたはログ ファイルを移動するには、「 [システム データベースの移動](move-system-databases.md)」を参照してください。  
  
### <a name="database-options"></a>データベース オプション  
 **msdb** データベースの各データベース オプションの既定値とそのオプションを変更できるかどうかを次の表に示します。 これらのオプションの現在の設定を表示するには、 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) カタログ ビューを使用します。  
  
|データベース オプション|既定値|変更可否|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|いいえ|  
|ANSI_NULL_DEFAULT|OFF|はい|  
|ANSI_NULLS|OFF|はい|  
|ANSI_PADDING|OFF|はい|  
|ANSI_WARNINGS|OFF|はい|  
|ARITHABORT|OFF|[はい]|  
|AUTO_CLOSE|OFF|はい|  
|AUTO_CREATE_STATISTICS|ON|はい|  
|AUTO_SHRINK|OFF|はい|  
|AUTO_UPDATE_STATISTICS|ON|はい|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|はい|  
|CHANGE_TRACKING|OFF|いいえ|  
|CONCAT_NULL_YIELDS_NULL|OFF|はい|  
|CURSOR_CLOSE_ON_COMMIT|OFF|はい|  
|CURSOR_DEFAULT|GLOBAL|はい|  
|データベース可用性オプション|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|いいえ<br /><br /> はい<br /><br /> [はい]|  
|DATE_CORRELATION_OPTIMIZATION|OFF|はい|  
|DB_CHAINING|ON|はい|  
|ENCRYPTION|OFF|いいえ|  
|NUMERIC_ROUNDABORT|OFF|はい|  
|PAGE_VERIFY|CHECKSUM|はい|  
|PARAMETERIZATION|SIMPLE|はい|  
|QUOTED_IDENTIFIER|OFF|はい|  
|READ_COMMITTED_SNAPSHOT|OFF|いいえ|  
|RECOVERY|SIMPLE|はい|  
|RECURSIVE_TRIGGERS|OFF|[はい]|  
|Service Broker のオプション|ENABLE_BROKER|はい|  
|TRUSTWORTHY|ON|はい|  
  
 これらのデータベース オプションの説明は、「[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。  
  
## <a name="restrictions"></a>制限  
 **msdb** データベースでは、次の操作を実行できません。  
  
-   照合順序の変更。 既定の照合順序はサーバーの照合順序です。  
  
-   データベースの削除。  
  
-   データベースからの **guest** ユーザーの削除。  
  
-   変更データ キャプチャの有効化。  
  
-   データベース ミラーリングへの参加。  
  
-   プライマリ ファイル グループ、プライマリ データ ファイル、またはログ ファイルの削除。  
  
-   データベース名またはプライマリ ファイル グループ名の変更。  
  
-   データベースの OFFLINE への設定。  
  
-   プライマリ ファイル グループの READ_ONLY への設定。  
  
## <a name="related-content"></a>関連コンテンツ  
 [システム データベース](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [データベース ファイルの移動](move-database-files.md)  
  
 [データベース メール](../database-mail/database-mail.md)  
  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
