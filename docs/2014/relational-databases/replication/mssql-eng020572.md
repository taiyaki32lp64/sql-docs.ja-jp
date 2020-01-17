---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86ec01db387d1c130ab593e99e5ef66a73259cf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057132"
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|20572|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|パブリケーション '%s' のアーティクル '%s' に対するサブスクライバー '%s' のサブスクリプションが、検証エラーの発生後、再初期化されました。|  
  
## <a name="explanation"></a>説明  
 サブスクライバーのデータがパブリッシャーのデータに対して検証され、データが一致しなかったため検証に失敗しました。 検証を実行するように指定したときに、検証が失敗した場合にサブスクリプションを再初期化するオプションを選択しました。 サブスクリプションを再初期化するには、サブスクライバーで新しいスナップショットを適用する必要があります。 検証の詳細については、「 [Validate Replicated Data](validate-data-at-the-subscriber.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 サブスクライバーで新しいスナップショットを適用すると、パブリッシャーのデータとサブスクライバーのデータが一致します。  
  
## <a name="see-also"></a>関連項目  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
