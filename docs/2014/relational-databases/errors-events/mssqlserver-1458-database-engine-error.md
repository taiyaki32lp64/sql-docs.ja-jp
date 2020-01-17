---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e18232c9d45b9552bbb1c8a194d1dbb1f74878f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915653"
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1458|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBM_FAILREDO_ON_PRIMARY|  
|メッセージ テキスト|'%.*ls' データベースのプリンシパル コピーでエラー %d、ステータス %d、重要度 %d が発生しました。 データベース ミラーリングは中断されました。 エラー状態を解決して、ミラーリングを再開してください。|  
  
## <a name="explanation"></a>説明  
 このメッセージは、データベース ミラーリングを中断させるエラーがプリンシパル データベースで検出されたことを示しています。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーはほとんどの場合、自動で修復されます。 問題が修正されない場合、通常はデータベースまたはサーバー インスタンスを再起動することで問題が解決されます。 詳細については、各パートナーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログを参照し、このメッセージに先行する関連エラーがないかどうかを確認してください。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングの監視 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
