---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1064b834d24c820da49a1791a6a319f27c27d301
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867989"
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|MSSQLSERVER|  
|イベント ID|3937|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|XACT_FILESTREAM_ROLLBACK_ERROR|  
|メッセージ テキスト|ファイル ストリーム フィルター ドライバーに、トランザクションがロールバックされたことを通知しようとして、エラーが発生しました。 エラー コード:0x%0x。|  
  
## <a name="explanation"></a>説明  
 トランザクションのロールバック通知の発行時に、RsFx ドライバーからエラーが返されました。 これは、リソース不足が原因である可能性があります。 これにより、RsFx フィルター ドライバーで小規模なメモリ リークが発生する場合があります。ただし、このメモリ リークはトランザクションを作成した sqlservr.exe プロセスの終了時に解放されます。  
  
## <a name="user-action"></a>ユーザーの操作  
  
