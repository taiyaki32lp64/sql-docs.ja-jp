---
title: MSSQL_ENG021331 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 63becb9b07114b6e0ae0589664ae80d82f8babb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023385"
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21331|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|ユーザー スクリプト ファイルをディストリビューターにコピーできませんでした。(%ls)|  
  
## <a name="explanation"></a>説明  
 このエラーは、サブスクリプションが手動で初期化され、レプリケーションによって作成されたスクリプト、またはレプリケーション コマンドで指定されたスクリプトが、指定されたディレクトリに保存できない場合に発生します。 このエラーは、権限に関する問題によって発生する可能性があります。サブスクリプションがスナップショットを使用しないで初期化される場合、パブリッシャーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの実行に使用されるアカウントは、ディストリビューターのスナップショット フォルダーに対する書き込み権限を持つ必要があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 スナップショット フォルダーに対して正しいパスが指定されていること、およびパブリッシャーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの実行に使用されるアカウントが十分な権限を持っていることを確認します。  
  
## <a name="see-also"></a>参照  
 [既定のスナップショットの場所を指定します。](snapshot-options.md#snapshot-folder-locations)   
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)   
 [スナップショットを使用しないトランザクション サブスクリプションの初期化](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
