---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cd67af96f58396c3f10ffbd97c48bfe2f6602211
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060622"
---
# <a name="mssqlserver10538"></a>MSSQLSERVER_10538
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10538|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_INVALID_PLANGUIDE_HANDLE|  
|メッセージ テキスト|指定したプラン ガイドの ID が NULL または無効であるか、またはプラン ガイドが参照しているオブジェクトに対する権限がないため、プラン ガイドを見つけることができません。 プラン ガイドの ID が有効であること、現在のセッションが適切なデータベース コンテキストに設定されていること、およびプラン ガイドが参照しているオブジェクトに対する ALTER DATABASE 権限または ALTER 権限のいずれかがあることを確認してください。|  
  
## <a name="explanation"></a>説明  
指定したプラン ガイドの ID が NULL または無効であるか、またはプラン ガイドが参照しているオブジェクトに対する権限がありません。  
  
## <a name="user-action"></a>ユーザーの操作  
プラン ガイドの ID が有効であること、現在のセッションが適切なデータベース コンテキストに設定されていること、およびプラン ガイドが参照しているオブジェクトに対する ALTER DATABASE 権限または ALTER 権限があることを確認します。  
  
## <a name="see-also"></a>参照  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[プラン ガイド](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
