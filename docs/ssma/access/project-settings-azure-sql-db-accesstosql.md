---
title: プロジェクトの設定 (Azure SQL DB) (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 60140559f94cdeebea935b423fbbeef24bce7a08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929466"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>プロジェクトの設定 (Azure SQL DB) (AccessToSQL)
SQL Azure プロジェクトの設定を使用して、接続ダイアログで追加して、SQL Azure 接続でハートビート メカニズムを実装することもできますを SQL Azure データベース サフィックスを構成できます。  
  
SQL Azure のウィンドウが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   プロジェクトの設定 ダイアログ ボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 SQL Azure の設定にアクセスする、**ツール**メニューの [**プロジェクト設定**、] をクリックして**全般**選択し、左側のウィンドウの下部にある**SQLAzure**します。  
  
-   プロジェクトの既定の設定 ダイアログ ボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 SQL Azure の設定にアクセスする、**ツール**メニューの  **DefaultProject 設定**で"SQL Azure"として、プロジェクトの種類を選択します**移行ターゲット バージョン**にコンボ ボックス。SQL Azure のウィンドウでの設定で、**全般**選択し、左側のウィンドウの下部にある**SQL Azure**します。  
  
## <a name="options"></a>および  
  
## <a name="connectivity"></a>接続  
**ハートビートの間隔**  
  
SQL Azure 接続を維持するハートビート メカニズムを使用する時間間隔を指定します。 ' 分: 秒の形式。  
  
**既定値**:' 4:45 '  
  
値を指定する必要がありますでいます: ss の形式 (たとえば、' 4:45 '、' 0:50 ')。  
  
**SQL Azure サーバーのサフィックス**  
  
SQL Azure サーバーのサフィックスを指定します  
  
**既定値**: 'database.windows.net'。  
  
