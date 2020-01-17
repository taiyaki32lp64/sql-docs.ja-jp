---
title: '[データベースのプロパティ] ([変更の追跡] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 926f6227d5a3a2e11dffbf4b9f080b1fc5ec35a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871855"
---
# <a name="database-properties-changetracking-page"></a>[データベースのプロパティ] \([変更の追跡] ページ)
  このページを使用すると、選択されているデータベースの変更の追跡設定を表示または変更できます。 このページで使用可能なオプションの詳細については、「[変更の追跡の有効化と無効化 &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md)」を参照してください。  
  
## <a name="options"></a>および  
 **変更の追跡**  
 データベースの変更の追跡の有効/無効を切り替えます。  
  
 変更の追跡を有効にするには、データベースを変更する権限が必要です。  
  
 この値を **True** に設定すると、個々のテーブルで変更の追跡を有効にできるデータベース オプションが設定されます。  
  
 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql)を使用して変更追跡を構成することもできます。  
  
 **保有期間**  
 データベースに変更追跡情報を保持する最低限の期間を指定します。 データは、 **[自動クリーンアップ]** の値が **True**の場合にのみ削除されます。  
  
 既定値は 2 です。  
  
 **[保有期間の単位]**  
 保有期間の値の単位を指定します。 **[日]** 、 **[時間]** 、または **[分]** を選択できます。 既定値は **[日]** です。  
  
 最小保有期間は 1 分です。 最大保有期間はありません。  
  
 **[自動クリーンアップ]**  
 指定した保有期間を過ぎると変更追跡情報が自動的に削除されるかどうかを指定します。  
  
 **[自動クリーンアップ]** を有効にすると、以前のカスタム保有期間はすべて既定の保有期間 (2 日) にリセットされます。  
  
## <a name="see-also"></a>関連項目  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
