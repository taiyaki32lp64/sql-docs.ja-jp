---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f58c6d1767666d1965bbfa99d9d257e0ed90022b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125530"
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|7915|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|メッセージ テキスト|修復:オブジェクト ID O_ID、インデックス ID I_ID、パーティション ID PN_ID、アロケーション ユニット ID A_ID (型 TYPE) の IAM チェーンがページ P_ID の前で切り捨てられました。チェーンが再構築されます。|  
  
## <a name="explanation"></a>説明  
これは、REPAIR から送られた情報メッセージであり、指定の IAM (Index Allocation Map) チェーンが再構築できるように修復されたことを示します。 この修復で、IAM チェーンの新しい開始位置の割り当てや、チェーンからの不正なページの削除が必要であった可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
なし  
  
