---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6f82b4412fdea7d7aa6dc21577502b1f7ede955a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137171"
---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1803|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NO_SPACE|  
|メッセージ テキスト|CREATE DATABASE が失敗しました。 プライマリ ファイルは、model データベースのコピーを格納するために少なくとも %d MB にしてください。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、model データベースのコピーを作成することによって、データベースを作成します。 その後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってコピーの名前が変更され、新しいデータベースが要求されたサイズに拡張されます。 この場合は、ユーザーが model データベースよりも小さいデータベースの作成を試みました。 この操作は、model データベースのコピーがプライマリ データ ファイルに収まらなかったため失敗しました。これは、プライマリ データ ファイルが model データベースより小さいことが原因です。  
  
## <a name="user-action"></a>ユーザーの操作  
データベース ファイルのサイズを大きくして、データベースを作成します。 その後で、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または DBCC SHRINKDATABASE ステートメントを使用して、必要に応じてデータベースを圧縮します。  
  
