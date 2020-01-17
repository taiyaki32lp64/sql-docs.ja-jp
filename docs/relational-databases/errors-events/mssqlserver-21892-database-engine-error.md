---
title: MSSQLSERVER_21892 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21892 (Database Engine error)
ms.assetid: 199818e8-28f4-440e-ad85-7bea88f51153
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4ca49ebb4a7481fc7fd23e916d10a185632280cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056654"
---
# <a name="mssqlserver21892"></a>MSSQLSERVER_21892
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21892|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21892|  
|メッセージ テキスト|仮想ネットワーク名 '%s' にプライマリとして関連付けられた可用性グループにある sys.availability_replicas で、メンバー レプリカのサーバー名をクエリすることができません。エラー = %d、エラー メッセージ = '%s'。|  
  
## <a name="explanation"></a>説明  
**sp_validate_replica_hosts_as_publishers** は、リダイレクトされたパブリッシャーに関連付けられている可用性グループの現在のプライマリにクエリを実行し、メンバー レプリカをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを特定します。  このクエリが失敗すると、エラー 21892 が返されます。  
  
**sp_validate_replica_hosts_as_publishers** は通常、一時リンク サーバーを最初に使用するため、接続の問題がある場合は **sp_validate_replica_hosts_as_publishers** で初めて問題が現れる可能性があります。 **sp_validate_redirected_publisher** と異なり、**sp_validate_replica_hosts_as_publishers** が使用するリンク サーバーは、いずれかの可用性グループ レプリカ ホストに接続するときに常に呼び出し元の資格情報を使用します。  
  
## <a name="user-action"></a>ユーザーの操作  
このストアド プロシージャを実行する場合は、レプリカのすべてに対して有効なログインから実行してください。 ログインには、可用性グループのメタデータ テーブルにクエリを実行し、パブリッシャー データベース レプリカのサブスクリプション メタデータ データベースにクエリを実行するための十分な権限が必要になります。  
  
参照される元のエラーを確認し、エラーの原因と適切な修正措置を特定します。  
  
