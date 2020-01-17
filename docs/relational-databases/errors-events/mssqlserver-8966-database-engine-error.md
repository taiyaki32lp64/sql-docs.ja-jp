---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8dff6385227c8ec498187541f4c8f8653ace15b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074291"
---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|8966|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|メッセージ テキスト|ラッチ型 TYPE のページ P_ID を読み取ってラッチすることができません。 OPERATION が失敗しました。|  
  
## <a name="explanation"></a>説明  
ページの読み取りに失敗したか、PFS ページまたは GAM ページでラッチを取得できませんでした。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに、ラッチ タイムアウトまたは他の添付メッセージが記録される場合があります。  
  
## <a name="user-action"></a>ユーザーの操作  
SQL エラー ログの添付メッセージを確認し、これらのエラーを解決します。  
  
