---
title: Visual FoxPro データベースから Microsoft Excel にデータをインポートする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65635132c5f98b0565391122877f2e3c0a6714
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085555"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Visual FoxPro データベースから Microsoft Excel へのデータのインポート
そのデータ ソースを定義している場合は、Microsoft Excel ワークシートに Visual FoxPro データをインポートできます。 Visual FoxPro データ ソースを作成する方法の詳細については、次を参照してください。 [Microsoft Excel から Visual FoxPro データ ソースへのアクセス](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)します。  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro データを Microsoft Excel ワークシートにインポートするには  
  
1.  Microsoft Excel スプレッドシートを開きます。  
  
2.  [データ] メニューから外部データの取り込みを選択します。 Microsoft のクエリが開きます。  
  
3.  データ ソースの選択 ダイアログ ボックスで、Visual FoxPro データ ソースを選択し、使用 をクリックします。  
  
4.  データ ソースからアクセスされるデータベースには、テーブルが含まれている場合は、テーブルの追加 ダイアログ ボックスからテーブルを選択します。 Microsoft のクエリでは、クエリ デザイナーの上部に追加されたテーブルが表示されます。  
  
    > [!NOTE]  
    >  ドライバーは所有者をサポートしていないためにも、所有者のリストはこのダイアログ ボックスでご利用いただけません。 ドライバーがデータ ソースで複数のデータベースをサポートしていないために、データベースの一覧は使用できません。  
  
5.  ドラッグして、テーブルから、下半分のデザイナー、クエリのフィールドを選択します。  
  
6.  Microsoft のクエリを閉じます。 選択したデータは、Microsoft Excel スプレッドシートにインポートされます。
