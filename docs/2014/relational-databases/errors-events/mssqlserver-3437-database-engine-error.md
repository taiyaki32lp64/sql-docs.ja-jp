---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9999b8536faf87a02cdca3432416e7d12f6b2902
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914530"
---
# <a name="mssqlserver3437"></a>MSSQLSERVER_3437
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3437|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NODTC|  
|メッセージ テキスト|データベース '%.*ls' を復旧中にエラーが発生しました。 トランザクション %S_XID の完了状態を確認するために Microsoft 分散トランザクション コーディネーター (MS DTC) に接続できません。 MS DTC を修正して、復旧を再実行してください。|  
  
## <a name="explanation"></a>説明  
 データベースをシャットダウンしたときに、[!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) を使用する分散トランザクションの 1 つ以上が完了しませんでした。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではトランザクションを完了させたりロールバックしたりするために MS DTC に接続することはできないので、このデータベースを復旧できませんでした。  
  
## <a name="user-action"></a>ユーザーの操作  
 このデータベースを復旧するには、まず MS DTC の問題を解決する必要があります。 MS DTC の問題を調査するため、Windows イベント ログを確認します。 MS DTC の問題を解決してデータベースを復旧できない場合は、データベースのバックアップを復元します。  
  
  
