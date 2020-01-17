---
title: MSSQL_ENG014157 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014157 error
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26befe89debb6fd890abeee9ea258e53a028b50c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191504"
---
# <a name="mssqleng014157"></a>MSSQL_ENG014157
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14157|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|サブスクライバー '%s' によって作成された、パブリケーション '%s' に対するサブスクリプションは、有効期限が切れたので削除されました。|  
  
## <a name="explanation"></a>説明  
 サブスクライバーは、パブリケーションの保有期間で指定された時間内にパブリッシャーと同期する必要があります。 サブスクライバーがこの期間内に同期しないと、サブスクリプションの有効期限が切れます。 詳細については、「 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 サブスクライバーがデータ変更の受信を再び開始するには、サブスクリプションを再作成して初期化する必要があります。  
  
-   サブスクリプションの作成については、「[パブリケーションのサブスクライブ](subscribe-to-publications.md)」を参照してください。  
  
-   サブスクリプションの初期化については、「[サブスクリプションの初期化](initialize-a-subscription.md)」を参照してください。  
  
 サブスクリプション データベースに、パブリッシャーと同期していない変更が含まれる場合は、 [tablediff Utility](../../tools/tablediff-utility.md) を使用して、パブリケーションとサブスクリプション データベースとの間で異なる行を確認できます。  
  
 サブスクリプションの有効期限が切れないように、パブリケーションの保有期間を長くすることができます。 保有期間に高い値を設定すると、保存されるデータとメタデータの量が増えてパフォーマンスに影響するため注意が必要です。 詳細については、「 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
