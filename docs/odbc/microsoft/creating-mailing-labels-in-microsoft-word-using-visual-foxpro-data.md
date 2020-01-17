---
title: Visual FoxPro データを使用して Microsoft Word での宛名ラベルを作成する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data [ODBC], mailing labels
- Visual FoxPro data [ODBC], Word
- mailing labels [ODBC]
- Visual FoxPro ODBC driver [ODBC], Word
- FoxPro ODBC driver [ODBC], word
ms.assetid: c901b60c-9f84-407a-b3d1-b4d301a71370
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73880171493555a7d30e5c0c5419d02338961e9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096529"
---
# <a name="creating-mailing-labels-in-microsoft-word-using-visual-foxpro-data"></a>Visual FoxPro データを使用した Microsoft Word での宛名ラベルの作成
Visual FoxPro データは、Windows 95 または Windows 98 のドキュメントの Microsoft Word で使用できます。 たとえば、Visual FoxPro テーブルに格納されている、顧客情報の宛名ラベルを作成する可能性があります。  
  
### <a name="to-create-mailing-labels"></a>絞り込みメール配信のラベルを作成するには  
  
1.  Microsoft Word では、新しい空白の文書を作成します。  
  
2.  [ツール] メニューで、メール マージを選択します。  
  
3.  文書の差し込みヘルパーの作成 をクリックし、宛名ラベルします。  
  
4.  メインのドキュメントでは、アクティブなウィンドウを選択します。  
  
5.  データ ソース、データの取得を選択し、データ ソースを開くします。  
  
6.  データ ソースを開く ダイアログ ボックスで、MS クエリを選択します。  
  
7.  データ ソースの選択 ダイアログ ボックスで、Visual FoxPro データ ソースを選択し、使用 をクリックします。  
  
8.  データ ソースからアクセスされるデータベースには、テーブルが含まれている場合は、テーブルの追加 ダイアログ ボックスからテーブルを選択します。 Microsoft のクエリでは、クエリ デザイナーの上部に追加されたテーブルが表示されます。  
  
9. ドラッグして、テーブルから、下半分のデザイナー、クエリのフィールドを選択します。  
  
10. [ファイル] メニューから Microsoft Word へのデータを返すを選択します。 Microsoft クエリが終了し、選択したデータが、差し込み印刷ドキュメントで使用できます。  
  
11. メインのドキュメントでは、セットアップを選択します。  
  
12. ラベルのオプション ダイアログ ボックスで、ok をクリックしてプリンターとラベル情報を選択します。  
  
13. ラベルの作成 ダイアログ ボックスで、絞り込みメール配信のラベルを印刷し、ok をクリックするフィールドを選択します。  
  
14. 文書の差し込みヘルパーのドキュメントをデータのマージ マージをクリックします。  
  
15. マージ ダイアログ ボックスで、結合をクリックして、オプションを選択します。
