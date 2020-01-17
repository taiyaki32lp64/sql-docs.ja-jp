---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c54c9e2f5e0e3d0a640935d80f22537a96876903
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903912"
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|611|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|VAR_SIZE_TOO_BIG|  
|メッセージ テキスト|行を挿入または更新できません。オーバーヘッドを含む、変数列の合計サイズが、制限を超える %d バイトです。|  
  
## <a name="explanation"></a>説明  
最大の可変長の列サイズがスキーマで許可されている値を超えています。 vardecimal ストレージ形式を設定したときに可変長の列が固定値の制限を超えているか、可変長の列サイズが圧縮データ レコードの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で許可されている制限を超えていた場合に、エラー 611 が返されます。  
  
## <a name="user-action"></a>ユーザーの操作  
レコードのサイズを縮小します。  
  
