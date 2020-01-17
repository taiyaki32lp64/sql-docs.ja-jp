---
title: 'HelloData: 単純な ADO アプリケーション |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e666f479d95e3915703dc539ba2731e95175488b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925139"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData: 単純な ADO アプリケーション
この単純なアプリケーションの 4 つの主要な ADO 操作の各ステップ: を取得する、確認、編集、およびデータを更新します。 これらの操作は、Microsoft® SQL Server に含まれている Northwind サンプル データベースに対して実行されます。 ADO の基礎に注目して、コードの煩雑さを回避するには、エラー処理の例では最小限です。  
  
### <a name="to-run-hellodata"></a>HelloData を実行するには  
  
1.  ADO ライブラリを参照する新しい標準 EXE Visual Basic プロジェクトを作成します。 詳細については、次を参照してください。 [ADO ライブラリを参照する](../../../ado/guide/referencing-the-ado-libraries.md)します。  
  
2.  フォームの上部にある 4 つのコマンド ボタンを作成、**名前**と**キャプション**プロパティの値をこのトピックの最後にある表に示すようにします。  
  
3.  ボタンの下に追加、 **Microsoft DataGrid コントロール**(Msdatgrd.ocx)。 Msdatgrd.ocx ファイルは、Visual Basic に含まれているされ、\windows\system32 または \winnt\system32 ディレクトリに置かれます。 DataGrid コントロールを Visual Basic のツールボックス ウィンドウに追加するには、選択**コンポーネント.** から、**プロジェクト**メニュー。 チェック ボックスをオンを横に"Microsoft DataGrid コントロール (SP3) 6.0 (OLEDB)"をクリックして **[ok]** 。 コントロールをプロジェクトに追加するには、Visual Basic フォームをツールボックスから DataGrid コントロールをドラッグします。  
  
4.  作成、**テキスト ボックス**グリッドの下のフォーム上の表に示すように、そのプロパティを設定するとします。 フォームが完了したら、次の図のようになります。  
  
5.  最後に記載されているコードをコピー [HelloData コード](../../../ado/guide/data/hellodata-code.md)フォームのコード エディター ウィンドウに貼り付けます。 キーを押して**F5**コードを実行します。  
  
> [!NOTE]
>  次の例と、このガイドでは、ユーザー id"123 abc"のパスワードを使用して「MyId」が、サーバーに対する認証に使用されます。 サーバーの有効なログオンの資格情報でこれらの値を置き換える必要があります。 また、サーバーの名前を持つ"MySQLServer"値に置き換えてください。  
  
 コードの詳細については、次を参照してください。 [HelloData に関するコメント](../../../ado/guide/data/comments-on-hellodata.md)します。  
  
 ![HelloData VB アプリケーションの Form1 を示しています](../../../ado/guide/data/media/hellodata.gif "HelloData。")  
  
|コントロールの種類|プロパティ|値|  
|------------------|--------------|-----------|  
|Form|名前|Form1|  
||[高さ]|6500|  
||[幅]|6500|  
|MS DataGrid|名前|grdDisplay1|  
|TextBox|名前|txtDisplay1|  
||複数行|true|  
|コマンド ボタン|名前|cmdGetData|  
||[キャプション]|Get Data|  
|コマンド ボタン|名前|cmdExamineData|  
||[キャプション]|データを調べる|  
|コマンド ボタン|名前|cmdEditData|  
||[キャプション]|データを編集します。|  
|コマンド ボタン|名前|cmdUpdateData|  
||[キャプション]|更新データ|
