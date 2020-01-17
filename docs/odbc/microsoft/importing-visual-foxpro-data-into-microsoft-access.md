---
title: Visual FoxPro データを Microsoft Access にインポートする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 557b5505b9eb6a15080a7d0495df2e63aefd2d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085543"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Visual FoxPro データの Microsoft Access へのインポート
Visual FoxPro データベースにインポートする オプションを使用して Microsoft Access データベースに格納されたデータをインポートすることができます。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Visual FoxPro データを Microsoft Access データベースにインポートするには  
  
1.  Microsoft Access データベースを開きます。  
  
2.  [ファイル] メニューから外部データの取り込みをインポートしを選択します。  
  
3.  インポート ダイアログ ボックスでは、ファイルの種類の一覧で、ODBC データベースを選択します。  
  
4.  SQL データ ソース ダイアログ ボックスで、クエリを実行し、ok をクリックする FoxPro データに接続する Visual FoxPro データ ソースを選択します。  
  
5.  オブジェクトのインポート ダイアログ ボックスで、インポートし、ok をクリックする 1 つまたは複数のテーブルを選択します。 インポートした Visual FoxPro テーブルの名前は、Microsoft Access データベースのテーブル タブに表示されます。  
  
 インポートした Visual FoxPro テーブル内のデータを操作する Microsoft Access を使えるようになりました。 インポートするデータは、Visual FoxPro; に格納されているデータのスナップショットインポートされたデータに加えた変更は、Visual FoxPro データ ソースには送信されません。  
  
 Microsoft Access、Visual FoxPro データ ソースのデータを変更するを参照してくださいで行った変更する場合は[クエリの実行と Microsoft Access から Visual FoxPro データを更新](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)します。
