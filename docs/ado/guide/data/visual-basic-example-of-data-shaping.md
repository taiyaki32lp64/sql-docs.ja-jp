---
title: Visual Basic の例のデータの整形 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic example of data shaping[ADO], about data shaping
ms.assetid: d95dd499-19e2-4ce7-b16e-f56a04a9519c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a21eda26bab7f5bc5d678c6763c803323ffcff8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923504"
---
# <a name="visual-basic-example-of-data-shaping"></a>Visual Basic のデータ シェイプの例
```  
' This application makes use of Microsoft Hierarchical FlexGrid  
' Control, which is named as MSHFLexGrid.  
Const SHAPER = "MSDataShape"  
Const DP = "SQLOLEDB"  
Const DS = "MySQLServer"  
Const DB = "Northwind"  
  
Private Sub Form_Load()  
    FirstExample  
End Sub  
  
Private Sub Form_Resize()  
    MSHFlexGrid.Top = 0  
    MSHFlexGrid.Left = 0  
    MSHFlexGrid.Width = Me.ScaleWidth  
    MSHFlexGrid.Height = Me.ScaleHeight  
End Sub  
  
Private Sub FirstExample()  
    Dim con As ADODB.Connection  
    Dim rst As ADODB.Recordset  
    Dim sCmd As String  
  
    Set con = New ADODB.Connection  
    Set rst = New ADODB.Recordset  
  
    con.ConnectionString = ConnectionString(SHAPER, DP, DS, DB)  
    con.Open  
  
    sCmd = "SHAPE {SELECT CustomerID, ContactName FROM Customers} " _  
        & "APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} " _  
        & "AS chapOrders " _  
        & "RELATE customerID TO customerID)"  
  
    rst.Open sCmd, con, adOpenStatic, 2  
    Set MSHFlexGrid.Recordset = rst  
  
    rst.Close  
    Set rst = Nothing  
  
    con.Close  
    Set con = Nothing  
  
End Sub  
  
Private Function ConnectionString(pr As String, _  
                                  dpr As String, _  
                                  dsr As String, _  
                                  dbs As String)  
    Dim s As String  
    If pr = "" Then  
        s = "Provider=" & dpr & _  
          ";Data Source=" & dsr & _  
          ";Initial Catalog=" & dbs & _  
          ";Integrated Security=SSPI;"  
    Else  
        s = "Provider=" & pr & _  
          ";Data Provider=" & dpr & _  
          ";Data Source=" & dsr & _  
          ";Initial Catalog=" & dbs & _  
          ";Integrated Security=SSPI;"  
    End If  
    ConnectionString = s  
End Function  
  
```  
  
#### <a name="try-it"></a>手順を次に示します。  
  
1.  標準 EXE の Visual Basic アプリケーション プロジェクトを作成します。  
  
2.  選択**コンポーネント**から、**プロジェクト**Visual Studio のメニュー  
  
3.  "Microsoft 階層フレキシブル グリッド コントロール 6.0 (OLEDB)"を選択してから、**コンポーネント**ポップアップ ウィンドウをクリック**保存**します。  
  
4.  Visual Basic ワークスペースの [ツールボックス] ウィンドウからフレキシブル グリッド コントロールをダブルクリックします。 フレキシブルをこのインスタンスの名前を変更します。  
  
5.  上記のコードをコピーして貼り付けます、**コード**ページを既存のコードに置き換えます。  
  
6.  選択**開始**から、**実行** メニューのアプリケーションを実行します。
