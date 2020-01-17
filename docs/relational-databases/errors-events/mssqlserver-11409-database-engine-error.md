---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7f4bc66c40cb6940694c1a25c4430ba3cc83e7c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116210"
---
# <a name="mssqlserver11409"></a>MSSQLSERVER_11409
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|11409|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|ALTERCOL_COLSET_DROP|  
|メッセージ テキスト|テーブル '%.\*ls' の列セット '%.*ls' を削除できません。テーブルに 1025 以上の列が含まれています。|  
  
## <a name="explanation"></a>説明  
テーブルには、スパース列または計算列として指定していない列を 1024 個まで含めることができます。 スパース列が原因でテーブルの列数が 1024 を超える場合は、テーブルに列セットを定義する必要があります。 参照先のテーブルには 1025 以上の列が含まれており、このテーブルから列セットを削除しようとしました。  
  
## <a name="user-action"></a>ユーザーの操作  
テーブルの現在の列では、列セットを保持する必要があります。  
  
列セットを削除するには、まずテーブルから列を削除し、列数が 1024 以下になるようにします。 その後、列セットを削除できます。  
  
