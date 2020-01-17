---
title: Visual Basic アプリケーションでの VFP FoxPro ODBC ドライバーの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 017e8e7897b2b792d7a864dc336537d76dcad8b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087985"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Visual Basic アプリケーションでの VFP FoxPro ODBC ドライバーの使用
Microsoft® Visual Basic® アプリケーションは、Visual FoxPro データ ソースに接続するデータ コントロールを作成して、Visual FoxPro データと通信できます。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Visual basic データ コントロールを使用して Visual FoxPro データに接続するには  
  
1.  Visual FoxPro に含まれる TasTrade サンプル データベースに接続するデータ ソースが"test"という名前を作成します。 Visual FoxPro の既定のインストールは、場所、TasTrade サンプル データベースを配置します。  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  Visual basic では、新しいフォームを作成し、テキスト ボックスと、上のデータ コントロールを配置します。  
  
3.  データ コントロールの接続プロパティを次の手順に変更します。  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  レコード セットのプロパティを次のように変更します。  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  レコードのプロパティを次のように変更します。  
  
    ```  
    customer  
    ```  
  
6.  テキスト ボックスの DataSource プロパティを次のデータ コントロールの既定の名前に変更します。  
  
    ```  
    data1  
    ```  
  
7.  テキスト ボックスの DataField プロパティを次のように変更します。  
  
    ```  
    customer_id  
    ```  
  
8.  フォームを実行し、Visual FoxPro TasTrade サンプル データベースから顧客 id フィールドをスキップするデータ コントロールを使用します。
