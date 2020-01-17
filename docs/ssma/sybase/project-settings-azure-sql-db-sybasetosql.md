---
title: プロジェクトの設定 (Azure SQL DB) (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 829e7b0c51cd341193944fb2f28241f48618c407
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176227"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>プロジェクトの設定 (Azure SQL DB) (SybaseToSQL)
Azure sql db プロジェクト設定を使用すると、azure sql db データベースのサフィックスを接続ダイアログに追加するように構成できます。また、azure SQL db 接続でハートビートメカニズムを実装することもできます。  
  
Azure SQL DB ウィンドウは、**プロジェクトの設定** ダイアログボックスと **既定のプロジェクトの設定** ダイアログボックスで使用できます。  
  
-   [プロジェクトの設定] ダイアログボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 Azure SQL DB の設定にアクセスするには、 **[ツール]** メニューの **[プロジェクトの設定]** を選択し、左側のウィンドウの下部にある **[全般]** をクリックして、 **[azure sql db]** を選択します。  
  
-   [既定のプロジェクトの設定] ダイアログボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 Azure SQL DB の設定にアクセスするには、 **[ツール]** メニューの **[Defaultproject の設定]** を選択し、左側のウィンドウの下部にある **[全般]** をクリックして、 **[azure sql db]** を選択します。  
  
## <a name="connectivity"></a>接続  
**ハートビートの間隔**  
  
Azure SQL DB の接続を ' 分: seconds ' 形式で保持するハートビートメカニズムに使用される時間間隔を指定します。  
  
**既定値**: ' 4:45 '  
  
値は、' m:ss ' 形式 (たとえば、' 4:45 ' または ' 0:50 ') で指定する必要があります。  
  
**Azure SQL DB サーバーサフィックス**  
  
Azure SQL DB サーバーのサフィックスを指定します  
  
**既定値**: ' database.windows.net '。  
  
