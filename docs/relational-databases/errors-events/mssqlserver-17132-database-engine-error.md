---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 335ba6a544023fd4eec16cd7461e2e17c224020f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131800"
---
# <a name="mssqlserver17132"></a>MSSQLSERVER_17132
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|17132|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|INIT_NODESSPACE|  
|メッセージ テキスト|記述子用のメモリが不足しているので、サーバーのスタートアップに失敗しました。 不要なメモリ負荷を減らすか、システム メモリを増やしてください。|  
  
## <a name="explanation"></a>説明  
サーバー内部の記述子を格納するための十分なメモリの割り当てに失敗しました。  
  
## <a name="user-action"></a>ユーザーの操作  
コンピューターにメモリを追加してください。 一般的なメモリのトラブルシューティング手順を使用できます。  
  
