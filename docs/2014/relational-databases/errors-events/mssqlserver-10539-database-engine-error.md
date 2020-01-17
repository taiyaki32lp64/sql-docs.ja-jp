---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18fafa113002b4a2420ac8784c48451a1d69aa56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916067"
---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10539|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_NO_PLAN_FOR_STMT|  
|メッセージ テキスト|プラン ガイド '%.*ls' をキャッシュから作成できません。開始オフセット %d のステートメントのクエリ プランを使用できません。 この問題は、存在しないデータベース オブジェクトにステートメントが依存している場合に発生することがあります。 必要なデータベース オブジェクトがすべて存在することを確認し、プラン ガイドを作成する前にステートメントを実行します。|  
  
## <a name="explanation"></a>説明  
 指定した開始オフセットを持つステートメントのクエリ プランがプラン キャッシュ内にありません。  
  
## <a name="user-action"></a>ユーザーの操作  
 必要なデータベース オブジェクトがすべて存在することを確認し、プラン ガイドを作成する前にステートメントを実行します。  
  
## <a name="see-also"></a>参照  
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
