---
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 676f0d1d131e8cc1a1c5265384bcd53cf11e9dab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116186"
---
# <a name="mssqlserver1101"></a>MSSQLSERVER_1101
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1101|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NOALLOCPG|  
|メッセージ テキスト|データベース '%.*ls' の新しいページを割り当てられませんでした。ファイル グループ '%.\*ls' のディスク領域が不足しています。 ファイル グループ内のオブジェクトの削除、ファイル グループへの新しいファイルの追加、またはファイル グループの既存のファイルの自動拡張の設定のいずれかを行って、必要な領域を作成してください。|  
  
## <a name="explanation"></a>説明  
ファイル グループでディスク領域が不足しています。  
  
## <a name="user-action"></a>ユーザーの操作  
次の操作により、ファイル グループで領域を使用できるようになることがあります。  
  
-   AUTOGROW をオンにする。  
  
-   ファイル グループにファイルをさらに追加する。  
  
-   ファイル グループ内の不要なインデックスやテーブルを削除することにより、ディスク領域を解放する。  
  
