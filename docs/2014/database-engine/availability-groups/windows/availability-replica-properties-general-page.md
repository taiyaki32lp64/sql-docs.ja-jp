---
title: 可用性レプリカのプロパティ ([全般] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilityreplicaproperties.general.f1
ms.assetid: 8318fefb-e045-4fab-8507-e1951fc7cec6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07652cec7b3b7a17c4b994eb68afd939e15244a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791906"
---
# <a name="availability-replica-properties-general-page"></a>可用性レプリカのプロパティ ([全般] ページ)
  このダイアログ ボックスには、可用性レプリカのプロパティが表示されます。  
  
## <a name="task-list"></a>タスク一覧  
 **可用性レプリカのプロパティを表示するには**  
  
-   [可用性レプリカのプロパティの表示 &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **[可用性グループ名]**  
 可用性グループの名前。 これはユーザー指定の名前であり、Windows Server フェールオーバー クラスター (WSFC) 内で一意であることが必要です。  
  
 **サーバー インスタンス**  
 このレプリカをホストし、既定ではないインスタンスの場合はレプリカのインスタンス名もホストしている、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスのサーバー名。  
  
 **ロール**  
 **プライマリ**  
 現在、プライマリ レプリカです。  
  
 **セカンダリ**  
 現在、セカンダリ レプリカです。  
  
 **[解決中]**  
 現在、レプリカのロールは、プライマリ ロールとセカンダリ ロールのどちらかに解決中です。  
  
 **[可用性モード]**  
 レプリカの可用性モード。次のいずれかです。  
  
 **[非同期コミット]**  
 プライマリ レプリカは、セカンダリがログをディスクに書き込むのを待機することなくトランザクションをコミットできます。  
  
 **[同期コミット]**  
 プライマリ レプリカは、セカンダリ レプリカがトランザクションをディスクに書き込むまで、特定のトランザクションのコミットを待機します。  
  
 詳細については、次を参照してください。[可用性モード (AlwaysOn 可用性グループ)](availability-modes-always-on-availability-groups.md)します。  
  
 **Failover mode**  
 レプリカのフェールオーバー モード。次のいずれかです。  
  
 **自動**  
 自動フェールオーバー。 レプリカは、自動フェールオーバーのターゲットです。 可用性モードが同期コミットに設定されている場合にのみサポートされます。  
  
 **手動**  
 手動フェールオーバー。 このレプリカには、データベース管理者が手動でのみフェールオーバーできます。  
  
 **[プライマリ ロールの接続]**  
 レプリカがプライマリ ロールを所有している場合にサポートされるクライアント接続の種類。  
  
 **[すべての接続を許可]**  
 プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これが既定の設定です。  
  
 **[読み取り/書き込みの接続を許可]**  
 Application Intent 接続プロパティが **ReadOnly** に設定されている接続は許可されません。 Application Intent プロパティが **ReadWrite** に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。  
  
 **[読み取り可能セカンダリ]**  
 セカンダリ ロールを実行している (つまりセカンダリ レプリカとして機能している) 可用性レプリカがクライアントからの接続を受け入れることができるかどうか。以下のいずれかです。  
  
 **いいえ**  
 このレプリカのセカンダリ データベースに対する直接接続は禁止されます。 読み取りアクセスで利用することはできません。 これが既定の設定です。  
  
 **[読み取り目的のみ]**  
 このレプリカのセカンダリ データベースに対する直接接続は、読み取り専用でのみ許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
 **はい**  
 読み取りアクセスに限り、このレプリカのセカンダリ データベースに対するすべての接続が許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
 詳細については、「[アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ (AlwaysOn 可用性グループ)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)します。  
  
 **[セッションのタイムアウト (秒)]**  
 タイムアウト時間 (秒単位)。 タイムアウト時間は、レプリカが別のレプリカからのメッセージの受信を待機する最大時間です。この時間を過ぎると、プライマリ レプリカとセカンダリ レプリカの間の接続は障害があるものと見なされます。 セッション タイムアウトは、セカンダリ レプリカがプライマリ レプリカに接続されているかどうかを検出します。 セカンダリ レプリカとの接続が確立されていないことを検出すると、プライマリ レプリカはセカンダリ レプリカが NOT_SYNCHRONIZED であるものと判断します。 プライマリ レプリカとの接続が確立されていないことを検出すると、セカンダリ レプリカは単に再接続を試みます。  
  
> [!NOTE]  
>  セッション タイムアウトにより自動フェールオーバーが発生することはありません。  
  
 **エンドポイント URL**  
 データ同期のためにプライマリとセカンダリのレプリカの間の接続で使用される、ユーザー指定のデータベース ミラーリング エンドポイントの文字列表現。 エンドポイント URL の構文の詳細については、「[可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
