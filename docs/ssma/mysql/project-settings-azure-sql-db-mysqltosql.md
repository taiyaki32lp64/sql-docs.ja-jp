---
title: プロジェクトの設定 (Azure SQL DB) (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: e4cf080d7a3bcb2d121a58a57be9f3fd41a4c18a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908826"
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>プロジェクトの設定 (Azure SQL DB) (MySQLToSQL)
SQL Azure プロジェクトの設定を使用して、接続ダイアログで追加して、SQL Azure 接続でハートビート メカニズムを実装することもできますを SQL Azure データベース サフィックスを構成できます。  
  
SQL Azure のウィンドウが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   プロジェクトの設定 ダイアログ ボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 SQL Azure の設定にアクセスする、**ツール**メニューの [**プロジェクト設定**、] をクリックして**全般**選択し、左側のウィンドウの下部にある**SQLAzure**します。  
  
-   プロジェクトの既定の設定 ダイアログ ボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 SQL Azure の設定にアクセスする、**ツール**メニューの  **DefaultProject 設定**、としてから SQL Azure 移行プロジェクトの種類を選択します**移行ターゲット バージョン**ドロップ。アクセスに SQL Azure のウィンドウで、設定 をクリックして**全般**選択し、左側のウィンドウの下部にある**SQL Azure**します。  
  
## <a name="options"></a>および  
  
## <a name="connectivity"></a>接続  
**ハートビートの間隔**  
  
SQL Azure 接続を維持するハートビート メカニズムを使用する時間間隔を指定します。 ' 分: 秒の形式。  
  
**既定値**:' 4:45 '  
  
値を指定する必要がありますでいます: ss の形式 (たとえば、' 4:45 '、' 0:50 ')。  
  
**SQL Azure サーバーのサフィックス**  
  
SQL Azure サーバーのサフィックスを指定します  
  
**既定値**: 'database.windows.net'。  
  
