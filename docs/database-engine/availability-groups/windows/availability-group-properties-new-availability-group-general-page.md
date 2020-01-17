---
title: '[全般] ページ ([新しい可用性グループ] ダイアログ ボックスと [プロパティ] ダイアログ ボックス)'
titleSuffix: SQL Server
description: SQL Server Management Studio (SSMS) の [新しい可用性グループ] ダイアログ ボックスと [可用性グループのプロパティ] ダイアログ ボックスの [全般] ページにあるさまざまなプロパティの説明です。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroupproperties.general.f1
ms.assetid: 9af5379f-91b8-4729-9f75-4a80242a30e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f379d55d2728d19a3321e99b342d8597622a6fc0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254078"
---
# <a name="availability-group-properties-new-availability-group-general-page"></a>可用性グループのプロパティ:新しい可用性グループ ([全般] ページ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックは、 **[新しい可用性グループ]** ダイアログ ボックスと **[可用性グループのプロパティ]** ダイアログ ボックスの **[全般]** タブに該当します。  **[新しい可用性グループ]** ダイアログ ボックスでは、 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]を使用せずに新しい可用性グループを作成できます。 **[可用性グループのプロパティ]** ダイアログ ボックスでは、既存の可用性グループの構成を表示、変更できます。  
  
 **可用性グループのプロパティを表示するには**  
  
-   [可用性グループのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **[可用性グループ名]**  
 可用性グループの名前。 これはユーザー指定の名前であり、Windows Server フェールオーバー クラスター (WSFC) 内で一意であることが必要です。  
  
## <a name="availability-databases"></a>可用性データベース  
 **データベース名**  
 可用性グループに追加されたデータベースの名前。  
  
 **追加**  
 クリックすると、データベースが可用性グループに追加されます。  
  
 **Remove**  
 クリックすると、選択したデータベースが可用性グループから削除されます。  
  
## <a name="availability-replicas"></a>可用性レプリカ  
 **サーバー インスタンス**  
 このレプリカをホストし、既定ではないインスタンスの場合はレプリカのインスタンス名もホストしている、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスのサーバー名。  
  
 **ロール**  
 **プライマリ**  
 現在、プライマリ レプリカです。  
  
 **セカンダリ**  
 現在、セカンダリ レプリカです。  
  
 **[解決中]**  
 現在、レプリカのロールは、プライマリ ロールとセカンダリ ロールのどちらかに解決中です。  
  
 **可用性モード**  
 レプリカの可用性モード。次のいずれかです。  
  
 **[非同期コミット]**  
 プライマリ レプリカは、セカンダリがログをディスクに書き込むのを待機することなくトランザクションをコミットできます。  
  
 **[同期コミット]**  
 プライマリ レプリカは、セカンダリ レプリカがトランザクションをディスクに書き込むまで、特定のトランザクションのコミットを待機します。  
  
 詳細については、「[可用性モード &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。  
  
 **フェールオーバー モード**  
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
 Application Intent 接続プロパティが **ReadOnly** に設定されている接続は許可されません。 Application Intent プロパティが **ReadWrite** に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 **[読み取り可能セカンダリ]**  
 セカンダリ ロールを実行している (つまりセカンダリ レプリカとして機能している) 可用性レプリカがクライアントからの接続を受け入れることができるかどうか。以下のいずれかです。  
  
 **いいえ**  
 このレプリカのセカンダリ データベースに対する直接接続は禁止されます。 読み取りアクセスで利用することはできません。 これが既定の設定です。  
  
 **[読み取り目的のみ]**  
 このレプリカのセカンダリ データベースに対する直接接続は、読み取り専用でのみ許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
 **はい**  
 読み取りアクセスに限り、このレプリカのセカンダリ データベースに対するすべての接続が許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
 **[セッションのタイムアウト (秒)]**  
 このレプリカでのセッションのタイムアウト期間の秒数。  
  
 **エンドポイント URL**  
 エンドポイントの URL です。 詳細については、「[可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)」を参照してください。  
  
 **追加**  
 クリックすると、セカンダリ レプリカが可用性グループに追加されます。  
  
 **Remove**  
 クリックすると、セカンダリ レプリカが可用性グループから削除されます。  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
