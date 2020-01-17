---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 832ee3caa23a034f1c228d01ff8ec2ceda32de06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915124"
---
# <a name="mssqlserver21871"></a>MSSQLSERVER_21871
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21871|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21871|  
|メッセージ テキスト|データベース %s のパブリッシャー %s がリダイレクトされていません。|  
  
## <a name="explanation"></a>説明  
 `sp_validate_replica_hosts_as_publishers` 識別されたパブリッシャーおよびパブリッシャー データベースのエントリをディストリビューション データベース内のテーブル MSredirected_publishers を確認します。  エントリが見つからない場合、`sp_validate_replica_hosts_as_publishers` はエラー 21871 を返します。  
  
## <a name="user-action"></a>ユーザーの操作  
 `sp_validate_replica_hosts_as_publishers` は、リダイレクトされたパブリッシャーにのみ関連しています。 パブリッシャー データベースが可用性グループのメンバーである場合、ストアド プロシージャ `sp_redirect_publisher` を使用して、パブリッシャーおよびパブリッシャー データベースを可用性グループの可用性グループ リスナー名に関連付けます。  
  
  
