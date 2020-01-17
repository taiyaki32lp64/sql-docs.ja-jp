---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18db8cfd54a9df36564d64c0cd94407bfefb21f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914796"
---
# <a name="mssqlserver3151"></a>MSSQLSERVER_3151
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3151|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LDDB_MASTER_LOAD_FAILED|  
|メッセージ テキスト|master データベースを復元できませんでした。 SQL Server をシャットダウンしています。 エラー ログを確認し、master データベースを再構築してください。 master データベースを再構築する方法の詳細については、SQL Server オンライン ブックを参照してください。|  
  
## <a name="explanation"></a>説明  
 これは一般エラー メッセージであり、**master** データベースに関するさまざまな問題を示しています。  
  
## <a name="user-action"></a>ユーザーの操作  
 詳細については、エラー ログを確認してください。 使用可能な **master** データベースを作成するには、REBUILDDATABASE オプションを使用して Setup.exe を実行します。 詳細については、次を参照してください。"する方法。SQL Server のインストール、コマンド プロンプトから"SQL Server オンライン ブック。  
  
  
