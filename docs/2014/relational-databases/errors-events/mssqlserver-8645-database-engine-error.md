---
title: MSSQLSERVER_8645 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8645 (Database Engine error)
ms.assetid: 63d6d6d7-3850-4061-8e96-b1fa665e3180
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7a039055daf8574d0c6b217c26d6f5572dd015c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62762565"
---
# <a name="mssqlserver8645"></a>MSSQLSERVER_8645
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|8645|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|MEMTIMEDOUT_ERR|  
|メッセージ テキスト|クエリ実行のためのメモリ リソースを待機中にタイムアウトが発生しました。 クエリを再実行してください。|  
  
## <a name="explanation"></a>説明  
 リソース プール 'default' でクエリ実行のためのメモリ リソースを待機中にタイムアウトが発生しました。  
  
## <a name="user-action"></a>ユーザーの操作  
 リソース ガバナーを使用していない場合は、サーバーの全体的な状態と読み込みを検証するか、リソース プールまたはワークロード グループの設定を確認することをお勧めします。  
  
 メモリ エラーのトラブルシューティングに役立つ一般的な手順の概略を次に示します。  
  
1.  このサーバー上で、他のアプリケーションやサービスによってメモリが消費されていないか確認します。 重要度の低いアプリケーションやサービスのメモリ消費量が少なくなるように、構成を変更します。  
  
2.  パフォーマンス モニター カウンターを収集を開始**SQL Server:バッファー マネージャー**、 **SQL Server:Memory Manager**します。  
  
3.  次に示す SQL Server メモリ構成パラメーターを確認します。  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     通常とは異なる設定がないか確認します。 必要に応じて、これらを修正します。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で増加した必要なメモリの要件を把握しておきます。 既定の設定については、SQL Server オンライン ブックの「サーバー構成オプションの設定」を参照してください。  
  
4.  DBCC MEMORYSTATUS 出力を監視し、エラー メッセージが表示された場合にどのように変化するかを調べます。  
  
5.  ワークロード (同時セッション数や現在実行中のクエリ数など) をチェックします。  
  
 次のアクションを実行すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用できるメモリを増やせる可能性があります。  
  
-   SQL Server 以外のアプリケーションがリソースを消費している場合は、そのアプリケーションの実行を停止するか、別のサーバーで実行することを検討します。 これにより、外部的なメモリ負荷を軽減できます。  
  
-   **max server memory** を構成した場合は、設定値を大きくします。  
  
 次の DBCC コマンドを実行して、いくつかの SQL Server メモリ キャッシュを解放します。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 問題が解決しない場合は、さらに調査します。ワークロードの軽減が必要になる場合もあります。  
  
  
