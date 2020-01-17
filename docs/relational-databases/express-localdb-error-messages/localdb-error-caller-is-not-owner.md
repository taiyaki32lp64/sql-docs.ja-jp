---
title: LOCALDB_ERROR_CALLER_IS_NOT_OWNER |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: f3303072-2b44-4443-936c-f024b0b2a8c5
author: stevestein
ms.author: sstein
ms.openlocfilehash: e220b6e5c07d7b6e8fdfdf32f5e6a8923c4d6e19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996017"
---
# <a name="localdberrorcallerisnotowner"></a>LOCALDB_ERROR_CALLER_IS_NOT_OWNER
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|282|  
|イベント ソース|SQL Server Local Database Runtime 12.0|  
|コンポーネント|Local Database Runtime API|  
|メッセージ テキスト|API 呼び出し元は、ローカル データベース インスタンスの所有者ではありません。|  
  
## <a name="explanation"></a>説明  
 要求された操作を実行するには、ユーザーがインスタンスの所有者である必要があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 インスタンスの所有者に問い合わせてください。  
  
  
