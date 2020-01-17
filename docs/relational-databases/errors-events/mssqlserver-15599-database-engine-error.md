---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 35ad5fd021845a0f528ed1a46aac61b93da015c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100412"
---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|15599|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|メッセージ テキスト|監査と権限をローカルの一時オブジェクトで設定できません。|  
  
## <a name="explanation"></a>説明  
監査と権限は、ローカルまたはグローバルの一時オブジェクトに設定する場合にまったく影響しません。 このステートメントではエラーは発生しません (操作は成功を返します) が、効果はありません。  
  
この動作は変更されていませんが、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降はこの情報メッセージがユーザーに通知されます。  
  
## <a name="user-action"></a>ユーザーの操作  
操作は必要ありませんが、ローカルまたはグローバルの一時オブジェクトに監査または権限を設定するステートメントを削除することを検討してください。  
  
