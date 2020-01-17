---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f8d62a98d39a65db78f79fdfaf3ecdb2921408e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915374"
---
# <a name="mssqlserver17130"></a>MSSQLSERVER_17130
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|17130|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|INIT_NOLOCKSPACE|  
|メッセージ テキスト|構成されたロック数に対するメモリが不足しています。 より小さいロックのハッシュ テーブルで開始しますが、パフォーマンスに影響する場合があります。 データベース管理者に連絡して、データベース エンジンのこのインスタンスに割り当てるメモリを増やすように構成してください。|  
  
## <a name="explanation"></a>説明  
 ロック マネージャーのハッシュ テーブルの必要なサイズに対してメモリが不足しています。  より小さいハッシュ テーブルの割り当てが試行されます。  
  
## <a name="user-action"></a>ユーザーの操作  
 サーバーのメモリ構成パラメーター (min/max server memory) を確認し、メモリ負荷を確認します。 SQL Server へのメモリの割り当てを増やします。  
  
  
