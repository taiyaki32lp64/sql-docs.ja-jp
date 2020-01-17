---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d59fd7ce3c6de67ed0072d908c4427cc9e2d8957
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68220234"
---
# <a name="mssqlserver2508"></a>MSSQLSERVER_2508
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2508|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_OUT_OF_DATE_PAGE_OR_ROW_COUNT|  
|メッセージ テキスト|オブジェクト "%.\*ls"、インデックス ID %d、パーティション ID %I64d、アロケーション ユニット ID %I64d (型 %.\*ls) の %.*ls のカウントが正しくありません。 DBCC UPDATEUSAGE を実行してください。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以前のバージョンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、テーブルおよびインデックスの行やページのカウント値が正しくならないことがあります。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] より前のバージョンで作成したデータベースはカウントが誤っている場合があります。 DBCC CHECKDB は、これらのエラーを検出するように拡張されており、エラーが見つかるとこの警告メッセージを返します。  
  
## <a name="user-action"></a>ユーザーの操作  
指定したオブジェクトやインデックス、またはオブジェクトが格納されているデータベースに対して DBCC UPDATEUSAGE を実行し、無効なカウントを修正します。  
  
