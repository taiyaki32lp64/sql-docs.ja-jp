---
title: MSSQLSERVER_4846 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b43cd194a2bfcf93b74b53fa2e9cb3a6a3eaff2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913792"
---
# <a name="mssqlserver4846"></a>MSSQLSERVER_4846
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|4846|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|BULKPROV_MEMORY|  
|メッセージ テキスト|一括データ ソース プロバイダーがメモリの割り当てに失敗しました。|  
  
## <a name="explanation"></a>説明  
 メモリの割り当てが失敗しました。  
  
## <a name="user-action"></a>ユーザーの操作  
 メモリ エラーのトラブルシューティングを行うための一般的な手順は次のとおりです。  
  
1.  このサーバー上で、他のアプリケーションやサービスによってメモリが消費されていないか確認します。 重要度の低いアプリケーションやサービスのメモリ消費量が少なくなるように、構成を変更します。  
  
2.  パフォーマンス モニター カウンターを収集を開始**SQL Server:バッファー マネージャー**、 **SQL Server:Memory Manager**します。  
  
3.  次に示す SQL Server メモリ構成パラメーターを確認します。  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     通常とは異なる設定がないか確認します。 必要に応じて、これらを修正します。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で必要なメモリの要件を把握しておきます。 既定の設定については、SQL Server オンライン ブックの「サーバー構成オプションの設定」を参照してください。  
  
4.  DBCC MEMORYSTATUS 出力を監視し、エラー メッセージが表示された場合にどのように変化するかを調べます。  
  
5.  ワークロード (同時セッション数や現在実行中のクエリ数など) をチェックします。  
  
 次のアクションを実行すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用できるメモリを増やせる可能性があります。  
  
-   SQL Server 以外のアプリケーションがリソースを消費している場合は、そのアプリケーションの実行を停止するか、別のサーバーで実行することを検討します。 これにより、外部的なメモリ負荷を軽減できます。  
  
-   **max server memory** を構成した場合は、設定値を大きくします。  
  
 次の DBCC コマンドを実行して、いくつかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ キャッシュを解放します。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 問題が解決しない場合は、さらに調査します。ワークロードの軽減が必要になる場合もあります。  
  
  
