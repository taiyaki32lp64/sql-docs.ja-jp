---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 23d53cad26ed52d985fa5c99fe07c9f0dd64e42f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101515"
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|8443|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SB_DIALOG_WO_CONV_GROUP|  
|メッセージ テキスト|ID '%.*ls' のメッセージ交換と発信側: %d は存在しないメッセージ交換グループ '%.\*ls' を参照しています。 DBCC CHECKDB を実行して、データベースを分析し、修復してください。|  
  
## <a name="explanation"></a>説明  
メタデータ層から、メッセージ交換グループに対して NULL が返されました。 なんらかの形でデータベースが破損しています。 考えられる原因の 1 つは、ディスク エラーです。  
  
## <a name="user-action"></a>ユーザーの操作  
修復モードで DBCC CHECKDB を実行し、データベースを一貫性のある状態に戻します。 一貫性のある状態を復元するために必要であれば、メッセージは削除される場合があります。 システム エラー ログで、システム内の別の障害が原因でこのエラーが生じていないか調べてください。  
  
