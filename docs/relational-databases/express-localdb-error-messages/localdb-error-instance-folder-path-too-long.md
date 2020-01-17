---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3db8328576d69fe32cea28d3596c5f9b1658d7b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995819"
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|260|  
|イベント ソース|SQL Server Local Database Runtime 12.0|  
|コンポーネント|Local Database Runtime API|  
|メッセージ テキスト|ローカル データベース インスタンス フォルダーの完全なパスの長さが MAX_PATH よりも長くなっています。 インスタンスは、フォルダーに格納する必要があります: %%LOCALAPPDATA%%\Microsoft\Microsoft SQL Server のローカル DB\Instances\\< インスタンス名\>します。|  
  
## <a name="explanation"></a>説明  
 インスタンスを格納するパスの長さが MAX_PATH を超過しています。  
  
## <a name="user-action"></a>ユーザーの操作  
 MAX_PATH よりも短い新しいパスを作成してください。  
  
  
