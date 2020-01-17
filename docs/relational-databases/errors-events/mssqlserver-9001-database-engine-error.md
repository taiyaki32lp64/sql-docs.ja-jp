---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 22767609a0281cc21a38d51716661ac98a8ffc24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118368"
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|9001|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LOG_NOT_AVAIL|  
|メッセージ テキスト|データベース '%.*ls' のログは使用できません。 イベント ログで、関連するエラー メッセージを確認してください。 エラーがある場合は解決し、データベースを再起動してください。|  
  
## <a name="explanation"></a>説明  
データベース ログがオフラインになりました。 通常、これは、データベースの再起動を必要とする重大なエラーを示しています。  
  
## <a name="user-action"></a>ユーザーの操作  
他のエラーを診断し、まだ自動的に再起動されていない場合は SQL Server インスタンスを再起動します。  
  
