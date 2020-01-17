---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5747a13e60182596610f25dd4ed1243670ff5018
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912176"
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|9790|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|メッセージ テキスト|着信メッセージをルーティングできません。 ルーティング情報を保持するシステム データベース MSDB がシングル ユーザー モードです。|  
  
## <a name="explanation"></a>説明  
 MSDB データベースがシングル ユーザー モードであったため、外部から受信したメッセージを分類しようとしたときにエラーが発生しました。  
  
## <a name="user-action"></a>ユーザーの操作  
 ALTER DATABASE コマンドを使用して、MSDB をマルチ ユーザー モードに変更します。  
  
  
