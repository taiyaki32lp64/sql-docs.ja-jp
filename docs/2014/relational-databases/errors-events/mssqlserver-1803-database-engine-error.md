---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1fd65bf2c79c7360f2502975e911aea7ab225d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915271"
---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
    
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
  
  
