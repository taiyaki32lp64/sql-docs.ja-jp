---
title: マージ アーティクル (レプリケーション TRANSACT-SQL プログラミング) のダミー更新の実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_mergedummyupdate
- dummy updates [SQL Server replication]
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 691988cd229f9b0c9ab81f31713a2b2e46806bdb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162008"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>マージ アーティクルのダミー更新の実行 (レプリケーション Transact-SQL プログラミング)
  マージ レプリケーションではレプリケーション処理の中でトリガーを使用します。パブリッシュ済みのテーブルに更新が加えられると、更新トリガーが起動します。 WRITETEXT 操作や UPDATETEXT 操作の際など、トリガーを起動せずにデータを更新できる場合もあります。 このような場合、ダミーの UPDATE ステートメントを明示的に追加して、変更をレプリケートする必要があります。 ダミーの UPDATE ステートメントは、レプリケーション ストアド プロシージャを使用して追加できます。  
  
### <a name="to-add-a-dummy-update-statement"></a>ダミーの UPDATE ステートメントを追加するには  
  
1.  ダミーの更新を必要とするマージ パブリッシュ済みテーブルの行に対して、操作 (たとえば UPDATETEXT など) を実行します。  
  
2.  サーバー (パブリッシャーまたはサブスクライバー) 上の変更が加えられたデータベースに対して、[sp_mergedummyupdate &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql) を実行します。 変更が加えられたテーブルを **@source_object** に指定し、変更された行の一意な識別子を **@rowguid** を実行します。  
  
3.  サブスクリプションを同期して、変更された行をレプリケートします。  
  
  
