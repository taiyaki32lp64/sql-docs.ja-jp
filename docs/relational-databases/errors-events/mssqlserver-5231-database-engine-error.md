---
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2cd4a8208925f6e0fe0a0fed4b162b4eb7361009
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122963"
---
# <a name="mssqlserver5231"></a>MSSQLSERVER_5231
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|5231|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|メッセージ テキスト|オブジェクト ID O_ID (オブジェクト 'NAME'):このオブジェクトを確認のためにロックしようとして、デッドロックが発生しました。 このオブジェクトはスキップされたので、処理されません。|  
  
## <a name="explanation"></a>説明  
DBCC がオブジェクトをロックしようとしてデッドロックが発生し、DBCC がデッドロック対象として選択されました。 このオブジェクトは処理されません。  
  
## <a name="user-action"></a>ユーザーの操作  
なし  
  
