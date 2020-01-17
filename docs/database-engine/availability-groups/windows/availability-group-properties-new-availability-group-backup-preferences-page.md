---
title: 可用性グループのプロパティ:[バックアップの設定] ページ
description: SQL Server Management Studio の [新しい可用性グループ] ウィザードの [バックアップの設定] ページにあるさまざまなプロパティの説明。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroupproperties.backuppreferences.f1
helpviewer_keywords:
- read-only routing
ms.assetid: 65fff22d-5963-4a8c-8b31-fe9ab247a03e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cebacaf07ca7e678095a661267b02fe04d8513d9
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822474"
---
# <a name="availability-group-properties-new-availability-group-backup-preferences-page"></a>可用性グループのプロパティ:新しい可用性グループ ([バックアップの設定] ページ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このダイアログ ボックスを使用して、選択した可用性グループのバックアップのユーザー設定を表示および変更します。  
  
 **可用性グループのプロパティを表示するには**  
  
-   [可用性グループのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="where-should-backups-occur"></a>バックアップを実行する場所  
 **[セカンダリを優先]**  
 オンラインのレプリカがプライマリ レプリカのみである場合を除き、セカンダリ レプリカでバックアップを実行することを指定します。 オンラインのレプリカがプライマリ レプリカのみである場合は、プライマリ レプリカでバックアップを実行する必要があります。 既定のオプションです。  
  
 **[セカンダリのみ]**  
 バックアップをプライマリ レプリカでは実行しないことを指定します。 オンラインのレプリカがプライマリ レプリカだけの場合、バックアップは実行されません。  
  
 **プライマリ**  
 バックアップを常にプライマリ レプリカで実行することを指定します。 このオプションは、差分バックアップの作成など、バックアップがセカンダリ レプリカで実行されたときにはサポートされないバックアップ機能が必要な場合に役に立ちます。  
  
 **[任意のレプリカ]**  
 バックアップを実行するレプリカを選択するときにバックアップ ジョブが可用性レプリカのロールを無視するように指定します。 バックアップ ジョブは、動作状態および接続状態と組み合わせて、各可用性レプリカのバックアップ優先順位などの他の要素を評価する場合があります。  
  
> [!IMPORTANT]  
>  バックアップに関するユーザー設定は適用されません。 この優先設定の解釈は、特定の可用性グループのデータベースに対するバックアップ ジョブのスクリプトでのロジックに依存します (ある場合)。 詳細については、「[アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
## <a name="replica-backup-priorities"></a>レプリカのバックアップの優先順位  
 このグリッドには、可用性グループのレプリカをホストする各サーバー インスタンスの現在のバックアップの優先順位が表示されます。 このグリッドを使用して、1 つまたは複数の可用性レプリカのバックアップの優先順位を変更します。  
  
 **サーバー インスタンス**  
 可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前。  
  
 **[バックアップ優先度 (最小 = 1、最高 = 100)]**  
 同じ可用性グループ内の他のレプリカと比較して、このレプリカでバックアップを実行する優先順位を指定します。 値は 0 ～ 100 の範囲の整数です。 1 は最も低い優先順位を示し、100 は最も高い優先順位を示します。 たとえば、 **Backup Priority** = 1 の場合、現在使用可能な可用性レプリカにそれより高い優先順位のものがない場合にのみ、その可用性レプリカがバックアップの実行に対して選択されます。  
  
 **[レプリカの除外]**  
 バックアップの実行時にこの可用性レプリカを選択しない場合に選択します。 これは、たとえば、バックアップをフェールオーバーすることがないリモート可用性レプリカのような場合に便利です。  
  
## <a name="see-also"></a>参照  
 [アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  

