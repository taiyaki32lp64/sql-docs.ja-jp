---
title: SQL Server のパラメーター |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine analysis [Upgrade Advisor]
- SQL Server Upgrade Advisor, Database Engine
- Upgrade Advisor [SQL Server], Database Engine
- analyzing system [Upgrade Advisor], Database Engine
ms.assetid: 44a18bfe-e593-47a5-995f-382c01d3f618
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e528b94e51238a06a9776e58693c3093f4bfb831
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091875"
---
# <a name="sql-server-parameters"></a>SQL Server パラメーター
  このページでは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]の分析で使用するパラメーターを設定します。 1 つ、複数、またはすべてのデータベースの分析、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して作成されたトレース ファイルの分析、および SQL バッチ ファイルの分析を行うことができます。  
  
> [!NOTE]  
>  分析対象のトレース ファイルまたは SQL バッチ ファイルを送信する場合に限り、一部のアップグレード問題が検出される可能性があります。  
  
## <a name="options"></a>および  
 **分析するデータベース**  
 すべてのデータベースを分析するには、選択、**すべてのデータベース**チェック ボックスをオンします。 データベースを選択して分析するには、各データベースの横にあるチェック ボックスをオンにしてスキャンの対象とします。  
  
 **トレース ファイルを分析します。**  
 ファイル システムのトレース ファイルを分析するには、このチェック ボックスをオンにします。  
  
 **トレース ファイルのパス**  
 1 つ以上のファイルを分析できます。 場所を参照して複数のファイルを選択したり、複数のファイル名を指定できます。 各ファイルへの完全パス名およびファイル名を使用し、パイプ文字 (|) でエントリを区切ります。  
  
 有効にした場合**トレース ファイルを分析する**、**次**パス名とファイル名を入力するまでは無効です。  
  
 **分析[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バッチ ファイル**  
 ファイル システムの [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ ファイルを分析するには、このチェック ボックスをオンにします。  
  
 **パス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バッチ ファイル**  
 1 つ以上のバッチ ファイルを分析できます。 場所を参照して複数のファイルを選択したり、複数のファイル名を入力できます。 各ファイルへの完全パス名およびファイル名を使用し、パイプ文字 (|) でエントリを区切ります。  
  
 有効にした場合**分析 SQL バッチ ファイル**、**次**パス名とファイル名を入力するまで、ボタンは無効です。  
  
 **SQL バッチ区切り記号**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの個別のバッチに使用するテキストです。 既定値は**移動**します。  
  
## <a name="see-also"></a>参照  
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [アップグレード アドバイザーのユーザー インターフェイス リファレンス](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
