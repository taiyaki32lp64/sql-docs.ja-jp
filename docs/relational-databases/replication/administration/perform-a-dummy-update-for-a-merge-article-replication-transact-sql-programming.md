---
title: ダミーのマージ アーティクルの更新 (レプリケーション SP)
description: Transact-SQL レプリケーション ストアド プロシージャを使用して、マージ レプリケーションで使用されるマージ アーティクルのダミー更新を実行します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 05c3a91d647819126261f0637e0de24d0ce3e4fd
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322037"
---
# <a name="perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming"></a>マージ アーティクルのダミー更新の実行 (レプリケーション Transact-SQL プログラミング)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  マージ レプリケーションではレプリケーション処理の中でトリガーを使用します。パブリッシュ済みのテーブルに更新が加えられると、更新トリガーが起動します。 WRITETEXT 操作や UPDATETEXT 操作の際など、トリガーを起動せずにデータを更新できる場合もあります。 このような場合、ダミーの UPDATE ステートメントを明示的に追加して、変更をレプリケートする必要があります。 ダミーの UPDATE ステートメントは、レプリケーション ストアド プロシージャを使用して追加できます。  
  
### <a name="to-add-a-dummy-update-statement"></a>ダミーの UPDATE ステートメントを追加するには  
  
1.  ダミーの更新を必要とするマージ パブリッシュ済みテーブルの行に対して、操作 (たとえば UPDATETEXT など) を実行します。  
  
2.  サーバー (パブリッシャーまたはサブスクライバー) 上の変更が加えられたデータベースに対して、[sp_mergedummyupdate &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md) を実行します。 `@source_object` には変更されたテーブルを指定し、`@rowguid` には変更された行の一意な識別子を指定します。  
  
3.  サブスクリプションを同期して、変更された行をレプリケートします。  
  
  
