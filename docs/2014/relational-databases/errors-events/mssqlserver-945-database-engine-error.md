---
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8c2cf1abfb41f4a49fccfe1befad11e429037da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761744"
---
# <a name="mssqlserver945"></a>MSSQLSERVER_945
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|945|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DB_IS_SHUTDOWN|  
|メッセージ テキスト|ファイルにアクセスできないか、メモリまたはディスク領域が不足しているので、データベース '%.*ls' を開けません。  詳細については、SQL Server エラー ログを確認してください。|  
  
## <a name="explanation"></a>説明  
 ファイルなどのリソースが存在しないため、データベースにアクセスできませんでした。  
  
## <a name="user-action"></a>ユーザーの操作  
 エラー ログを参照し、メモリ、ディスク領域、または権限のエラーに関する追加情報を確認してください。 影響を受けたデータベースの .mdf ファイルと .ndf ファイルの場所を確認し、[!INCLUDE[ssDE](../../includes/ssde-md.md)]で使用するアカウントにこれらのファイルへのアクセス権が与えられていることを確認します。 問題を解決した後、データベースを再起動します。この操作を行うには、ALTER DATABASE を使用して、データベースを ONLINE に設定します。  
  
  
