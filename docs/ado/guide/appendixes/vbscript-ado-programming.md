---
title: VBScript での ADO プログラミング |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f242a3596735a4bc43256d05b87100e71295a3da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926437"
---
# <a name="vbscript-ado-programming"></a>VBScript での ADO プログラミング
## <a name="creating-an-ado-project"></a>ADO プロジェクトの作成  
 Microsoft Visual Basic, Scripting Edition は、ADO をプロジェクトで参照する必要はありませんので、タイプ ライブラリをサポートしません。 そのため、コマンドラインの入力候補などの関連する機能はサポートされません。 また、既定では、ADO 列挙定数で定義されていない VBScript です。  
  
 ただし、ADO は、VBScript で使用する次の定義を含むファイルをインクルードする 2 つを提供します。  
  
-   サーバー側スクリプト使用 Adovbs.inc、既定で c:\Program files \common files Files\System\ado\ フォルダーにインストールされるは。  
  
-   クライアント側スクリプト使用 Adcvbs.inc、既定で c:\Program files \common files Files\System\msdac\ フォルダーにインストールされるは。  
  
 コピーし、ASP ページにこれらのファイルからの定数の定義を貼り付けるか、Adovbs.inc ファイル、Web サイト上のフォルダーをコピーし、次のように、ASP ページから参照する、サーバー側のスクリプトを実行している場合。  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>VBScript で ADO オブジェクトの作成  
 使用することはできません、 **Dim** VBScript で特定の型にオブジェクトを代入するステートメント。 また、VBScript はサポートしません、**新規**で使用される構文、 **Dim**アプリケーション用の Visual Basic でのステートメント。 代わりに使用する必要があります、 **CreateObject**関数呼び出し。  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript の例  
 次のコードでは、Active Server Page (ASP) ファイルで VBScript サーバー側プログラミングの汎用例を示します。  
  
```vb
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 具体的な VBScript 例については、ADO のドキュメントに含まれています。 詳細については、次を参照してください。 [ADO のコード例では、Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md)します。  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript と Visual Basic の違い  
 ADO を使用して VBScript では、Visual Basic での構文を使用する方法など、さまざまな方法で ADO を使用してに似ています。 ただし、いくつかの重要な違いがあります。  
  
-   VBScript では、のみ、Variant データ型のさまざまな種類のデータを格納できるをサポートします。 バリアント データ型では、必要なデータを格納して、キャスト VBScript によって実行されるため、データは適切に機能します。 ADO では、必要な型を認識し、それに応じて、バリアントの値を変換します。  
  
-   使用することはできません**エラー goto で\<ラベル >** VBScript 内。  
  
-   VBScript のよういくつかの組み込みの Visual Basic の関数サポート**Msgbox**、**日付**、および**IsNumeric**します。 ただし、VBScript は、Visual Basic のサブセットであるために、すべての組み込み関数はサポートされます。 たとえば、VBScript はサポートされません、**形式**関数およびファイル I/O 関数。
