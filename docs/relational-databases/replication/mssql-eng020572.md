---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 07bd8dfb40c9832c55b6b0d21e11f3f0684c9a54
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770408"
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
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
 サブスクライバーのデータがパブリッシャーのデータに対して検証され、データが一致しなかったため検証に失敗しました。 検証を実行するように指定したときに、検証が失敗した場合にサブスクリプションを再初期化するオプションを選択しました。 サブスクリプションを再初期化するには、サブスクライバーで新しいスナップショットを適用する必要があります。 検証の詳細については、「 [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 サブスクライバーで新しいスナップショットを適用すると、パブリッシャーのデータとサブスクライバーのデータが一致します。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
