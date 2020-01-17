---
title: データベースの状態 | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASESTATES.F1
helpviewer_keywords:
- emergency database state [SQL Server]
- verifying database states
- viewing database states
- displaying database states
- database states [SQL Server]
- current database state
- offline database state [SQL Server]
- suspect database state
- recovery pending database state [SQL Server]
- states [SQL Server], databases
- online database state
- states [SQL Server]
- restoring database state [SQL Server]
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b6e2072e06e1ea5d61802a4c6a006737bc04762
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871698"
---
# <a name="database-states"></a>データベースの状態
  データベースは、常に、ある特定の状態にあります。 たとえば、ONLINE、OFFLINE、SUSPECT などです。 データベースの現在の状態を確認するには、 **sys.databases** カタログ ビューで [state_desc](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 列を選択するか、 **DATABASEPROPERTYEX** 関数で [Status](/sql/t-sql/functions/databasepropertyex-transact-sql) プロパティを選択します。  
  
## <a name="database-state-definitions"></a>データベースの状態の定義  
 次の表では、データベースの状態を定義します。  
  
|状態|定義|  
|-----------|----------------|  
|ONLINE|データベースにアクセスできます。 復旧時に行われる元に戻すフェーズが完了していなくても、プライマリ ファイル グループはオンラインです。|  
|OFFLINE|データベースは使用できません。 ユーザーの明示的な操作によってデータベースがオフラインになり、ユーザーが新たな操作を行うまでオフラインのままになります。 たとえば、ファイルを新しいディスクに移動するために、データベースをオフラインにできます。 移動の完了後に、データベースをオンラインに戻します。|  
|RESTORING|プライマリ ファイル グループの 1 つ以上のファイルが復元中か、1 つ以上のセカンダリ ファイルがオフラインで復元中です。 データベースは使用できません。|  
|RECOVERING|データベースが復旧中です。 復旧処理は一時的な状態です。復旧が成功すると、データベースは自動的に online 状態になります。 復旧が失敗すると、データベースは suspect 状態になります。 データベースは使用できません。|  
|RECOVERY PENDING|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で、復旧中にリソースに関連するエラーが発生しました。 データベースは破損していませんが、ファイルが見つからないか、システム リソースの制限によりデータベースを起動できない可能性があります。 データベースは使用できません。 エラーを解決して復旧処理を完了するには、ユーザーによる新たな操作が必要です。|  
|SUSPECT|少なくともプライマリ ファイル グループが問題のある状態で、破損している可能性があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の起動中にはデータベースを復旧できません。 データベースは使用できません。 問題を解決するには、ユーザーによる新たな操作が必要です。|  
|EMERGENCY|ユーザーがデータベースを変更し、状態を EMERGENCY に設定しました。 データベースはシングル ユーザー モードになり、修復または復元できます。 データベースは READ_ONLY に設定され、ログ記録が無効になり、アクセスが **sysadmin** 固定サーバー ロールのメンバーに制限されます。 EMERGENCY は、主にトラブルシューティングの目的で使用されます。 たとえば、suspect に設定されたデータベースを、EMERGENCY 状態に設定できます。 これにより、システム管理者にデータベースへの読み取り専用のアクセスを許可できます。 **sysadmin** 固定サーバー ロールのメンバーのみが、データベースを EMERGENCY 状態に設定できます。|  
  
## <a name="related-content"></a>関連コンテンツ  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [ミラーリング状態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [ファイルの状態](file-states.md)  
  
  
