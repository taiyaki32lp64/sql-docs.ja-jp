---
title: Microsoft Visual Basic で ADO を使用して |Microsoft Docs
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
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22286cbe571420475cf273ca377d16e79610fc3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926565"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>アプリケーションの Microsoft Visual Basic および Visual Basic と ADO の併用
ADO のプロジェクトを設定し、ADO コードの記述は似ていますアプリケーションの Visual Basic または Visual Basic を使用するかどうか。 このトピックでは、ADO を Visual Basic と Visual Basic の両方のアプリケーションを使用してアドレスし、相違点をメモします。

## <a name="referencing-the-ado-library"></a>ADO ライブラリを参照します。
 ADO ライブラリをプロジェクトに参照する必要があります。

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Microsoft Visual Basic から ADO を参照するには

1.  Visual basic での**プロジェクト**メニューの **参照.** .

2.  選択**Microsoft ActiveX Data Objects x.x ライブラリ**一覧から。 以上であることを確認も、次のライブラリが選択されます。

    -   Visual Basic for Applications

    -   Visual Basic ランタイム オブジェクトと手順

    -   Visual Basic のオブジェクトと手順

    -   OLE オートメーション

3.  **[OK]** をクリックします。

 ADO を使用でき同じくらい簡単に Visual Basic によるアプリケーションの場合、たとえば、Microsoft Access を使用しています。

#### <a name="to-reference-ado-from-microsoft-access"></a>Microsoft Access から ADO を参照するには

1.  Microsoft Access で選択するかからモジュールを作成、**モジュール** タブで、**データベース**ウィンドウ。

2.  **ツール**メニューの **参照.** .

3.  選択**Microsoft ActiveX Data Objects x.x ライブラリ**一覧から。 以上であることを確認も、次のライブラリが選択されます。

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 オブジェクト ライブラリ (またはそれ以降)

    -   3\.5 DAO オブジェクト ライブラリ (またはそれ以降)

4.  **[OK]** をクリックします。

## <a name="creating-ado-objects-in-visual-basic"></a>Visual Basic での ADO オブジェクトの作成
 Automation 変数とをその変数のオブジェクトのインスタンスを作成するには、2 つのメソッドを使用できます。**Dim**または**CreateObject**します。

### <a name="dim"></a>Dim
 使用することができます、**新規**キーワード**Dim**宣言し、1 つの手順で ADO オブジェクトのインスタンスを作成します。

```
Dim conn As New ADODB.Connection
```

 または、 **Dim**ステートメントの宣言とオブジェクトのインスタンス化は、2 つの手順をすることもできます。

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  明示的に使用する必要はありません、`ADODB`と progid、 **Dim**ステートメントでは、プロジェクトで ADO ライブラリを正しく参照するいると仮定するとします。 ただし、これを使用して保証する必要があるいないその他のライブラリで名前の競合。

> [!NOTE]
>  たとえば、ADO と DAO への参照を同じプロジェクトに含める場合は、インスタンス化するときに使用するオブジェクト モデルを指定する修飾子を含める必要があります**Recordset**オブジェクトは、次のコードのようにします。

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 **CreateObject**メソッドでは、宣言とオブジェクトのインスタンス化は 2 つの別個のステップである必要があります。

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 オブジェクトがインスタンス化された**CreateObject**遅延バインディングは厳密に型がありませんし、コマンドラインの入力候補が無効になっていることを意味します。 ただし、では ADO ライブラリをプロジェクトから参照をスキップすることし、特定のバージョンのオブジェクトをインスタンス化することができます。 以下に例を示します。

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 具体的には ADO バージョン 2.0 のタイプ ライブラリへの参照を作成し、オブジェクトを作成してこれを実現できました。

 使用してオブジェクトをインスタンス化する、 **CreateObject**メソッドは、一般に使用するよりも低速、 **Dim**ステートメント。

## <a name="handling-events"></a>イベントの処理
 Microsoft Visual Basic での ADO イベントを処理するために、モジュール レベル変数を使用してを宣言する必要があります、 **WithEvents**キーワード。 変数は、クラス モジュールの一部としてのみ宣言することができます、モジュール レベルで宣言する必要があります。 ADO イベントの処理の詳細については、次を参照してください。 [ADO イベントの処理](../../../ado/guide/data/handling-ado-events.md)します。

## <a name="visual-basic-examples"></a>Visual Basic の例
 多くの Visual Basic の例は、ADO のドキュメントに含まれています。 詳細については、次を参照してください。 [ADO のコード例では、Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)します。

## <a name="see-also"></a>関連項目
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [Microsoft Visual C で ADO を使用して](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [ADO スクリプト言語を使用します。](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
