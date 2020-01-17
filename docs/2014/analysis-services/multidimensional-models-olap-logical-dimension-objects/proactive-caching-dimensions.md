---
title: プロアクティブ キャッシュ (ディメンション) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], proactive caching
- proactive caching [Analysis Services]
ms.assetid: 7d57fe93-6e5f-4a50-844f-dd2bbdbb94a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6f5e6bab81e982adbf8ee443bd84a5e806b960db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727300"
---
# <a name="proactive-caching-dimensions"></a>プロアクティブ キャッシュ (ディメンション)
  プロアクティブ キャッシュでは、自動 MOLAP キャッシュの作成と、OLAP オブジェクトの管理が可能です。 データベース内のデータに加えられた変更は、データベースからの通知に基づき、すぐにキューブに反映されます。 プロアクティブ キャッシュの目標は、従来の MOLAP のパフォーマンスを提供しながら、ROLAP の即時性と管理のしやすさを保つことです。  
  
 簡単な <xref:Microsoft.AnalysisServices.ProactiveCaching> オブジェクトは、タイミングの指定およびテーブル通知で構成されます。 タイミングの指定は、変更通知を受信してからキャッシュが更新されるまでのタイムフレームを定義します。 テーブル通知は、データ テーブルと <xref:Microsoft.AnalysisServices.ProactiveCaching> オブジェクトとの間の通知スキーマを定義します。  
  
  
