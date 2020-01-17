---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b88b9212cec193e86de72b70c126df3e3d0d92e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120488"
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|MSSQLSERVER|  
|イベント ID|8710|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|メッセージ テキスト|CUBE、ROLLUP、または GROUPING SET クエリで使用される集計関数は、サブ集計をマージするものである必要があります。 この問題を解決するには、集計関数を削除するか、UNION ALL を GROUP BY 句で使用するクエリを記述してください。|  
  
## <a name="explanation"></a>説明  
サブ集計をマージできない集計関数が CUBE、ROLLUP、または GROUPING SET で使用されています。  
  
## <a name="user-action"></a>ユーザーの操作  
この問題を解決するには、集計関数を削除するか、UNION ALL を GROUP BY 句で使用するクエリを記述してください。  
  
