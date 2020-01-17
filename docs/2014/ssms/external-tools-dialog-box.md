---
title: '[外部ツール] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- adding external tools
- external tools [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], external tools
ms.assetid: ba797203-24d0-4922-9b97-8ab483f1db14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dc8f54bc4f6e7aaffa5d912fc9bc8f03fad71d03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245629"
---
# <a name="external-tools-dialog-box"></a>[外部ツール] ダイアログ ボックス
  **[外部ツール]** ダイアログ ボックスは、SQLCMD やメモ帳などの外部ツールを **[ツール]** メニューに追加するために使用します。 外部ツールを追加すると、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 環境で作業しながら、簡単に他のアプリケーションを起動できるようになります。 また、ツールを起動するときに引数や作業ディレクトリを指定できます。 また、一部のツールからの出力を **[出力]** ウィンドウに表示することもできます。 **[外部ツール]** ダイアログ ボックスは、 **[ツール]** メニューから使用できます。  
  
## <a name="options"></a>および  
 **[メニューの内容]**  
 **[ツール]** メニューに現在追加されている項目のタイトルを一覧表示します。 メニューに表示される項目の順序を変更するには、 **[上へ移動]** と **[下へ移動]** を使用します。 メニューから項目を削除するには、 **[削除]** ボタンを使用します。  
  
 **[上へ移動]**  
 **[ツール]** メニューで表示されるツールの一覧に、選択したツールを表示する位置を上へ移動します。  
  
 **[下へ移動]**  
 **[ツール]** メニューで表示されるツールの一覧に、選択したツールを表示する位置を下へ移動します。  
  
 **[追加]**  
 新しいツールを指定できるようにテキスト ボックスをクリアします。  
  
 **削除**  
 **[メニューの内容]** の一覧および **[ツール]** メニューから、ツールまたはコマンドを削除します。  
  
 **[タイトル]**  
 **[ツール]** メニューの **[外部メニュー]** サブメニューに表示されるツールまたはコマンドの名前を入力します。 ツール名の 1 文字の前にアンパサンド (&) を付けて、その文字をキーボード ショートカットとして指定します。 たとえば、"&SQLCMD" と指定した場合は、**[ツール]** メニューに &SQLCMD が表示されます。  
  
 **Command**  
 起動するファイルへのパスを指定します。  
  
 **引数**  
 メニューでツールが選択されたときにツールに渡される変数を指定します。 引数によって、ツールやコマンドの起動時に渡す値を指定できます。 たとえば、ファイル名またはディレクトリを指定できます。 矢印ボタンをクリックして表示される定義済みの引数の一覧から選択します。 複数の引数を追加できます。 定義済み引数および定義の完全な一覧については、「 [外部ツールの引数](menu-help/external-tools.md)」を参照してください。 使用するコマンドまたはツールに応じて、カスタム引数 (コマンド ライン スイッチなど) を入力することもできます。  
  
 **[出力ウィンドウを使用]**  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] の出力ウィンドウを開いて、実行中のコマンドの出力を表示します。 ツールによっては、出力ウィンドウに表示可能な形式の出力が提示されないものもあります。 詳細については、「 [[出力ウィンドウ]](../relational-databases/scripting/transact-sql-debugger-output-window.md)」を参照してください。  
  
 **[Unicode で出力を処理する]**  
 出力を Unicode として解釈します。  
  
 **[初期ディレクトリ]**  
 ツールの作業ディレクトリを指定します。 矢印ボタンを使用してディレクトリを選択します。 複数のディレクトリを選択できます。  
  
 **[起動時に引数を入力]**  
 外部ツールを起動するたびに **[引数]** ダイアログ ボックスを表示して、引数の値を入力したり編集したりできるようにします。  
  
 **[終了時にウィンドウを閉じる]**  
 ツールを閉じるときに、ツールを使用して開いたウィンドウを閉じます。  
  
## <a name="example"></a>例  
 **[外部ツール]** ダイアログ ボックスに次の値を入力すると、"DAC" というラベルが付いたメニュー項目が作成されます。このメニュー項目を選択すると、コマンド プロンプトが開き、専用管理者接続を使用して **sqlcmd** ユーティリティが実行されます。  
  
|ボックス|値|  
|---------|-----------|  
|**Title**|DAC (DAC)|  
|**Command**|[!INCLUDE[ssInstallPath](../includes/ssinstallpath-md.md)]Tools\Binn\SQLCMD.exe|  
|**引数**|-A|  
  
## <a name="see-also"></a>関連項目  
 [外部ツールの引数](menu-help/external-tools.md)   
 [一般的なユーザー インターフェイス要素](general-user-interface-elements.md)  
  
  
