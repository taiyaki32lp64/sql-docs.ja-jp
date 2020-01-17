---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f5078c98445587dbf8c8b99fa18fed4df2ca5846
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951668"
---
# <a name="mssqlserver617"></a>MSSQLSERVER_617
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|617|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NODESHASH|  
|メッセージ テキスト|データベース ID %d のオブジェクト ID %ld の記述子の非ハッシュ化を試みたときに、記述子がハッシュ テーブルに見つかりませんでした。 作業テーブルがエントリに見つかりません。 クエリを再実行してください。 カーソルが含まれている場合は、カーソルを閉じてから再度開いてください。|  
  
## <a name="explanation"></a>説明  
SQL Server で、作業テーブルの特定のエントリが見つかりません。  
  
## <a name="user-action"></a>ユーザーの操作  
  
1.  カーソルが含まれている場合は、カーソルを閉じてから再度開いてください。  
  
2.  クエリを再実行します。  
  
