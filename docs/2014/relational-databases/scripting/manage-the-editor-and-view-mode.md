---
title: エディターと表示モードの管理
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], managing window behavior
- workbench view modes [SQL Server Management Studio]
- full screen mode [SQL Server Management Studio]
- fonts [SQL Server Management Studio]
- word wraps [SQL Server Management Studio]
- virtual space mode [SQL Server Management Studio]
- splitting document views
- displaying line numbers
- view modes [SQL Server Management Studio]
ms.assetid: 25c58a14-9f94-4296-9770-7d84c6bc3969
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67ca649678fcc099a2abf1b50866263d6494bec7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242042"
---
# <a name="manage-the-editor-and-view-mode"></a>エディターと表示モードの管理
  エディターには、コードの表示を制御するさまざまな方法が用意されています。  
  
## <a name="changing-the-view-mode"></a>表示モードの変更  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]には、**タブ付きドキュメント**と呼ばれるビューモードが用意されています。これにより、複数のエディターやドキュメントを同時に開いて、エディターの上部にあるタブからそれらにアクセスできます。 また、マルチドキュメント インターフェイス (MDI) モードで [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開くこともできます。この場合は、タブなしでウィンドウが統合され、各ウィンドウを並べて表示したり、最小化したりすることが可能になります。  
  
#### <a name="to-switch-between-view-modes"></a>表示モードを切り替えるには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[環境]** をクリックします。 [**一般**] をクリックします。  
  
3.  
  **[タブ付きドキュメント]** または **[MDI 環境]** をクリックします。  
  
    > [!NOTE]  
    >  変更内容を有効にするには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を再起動する必要があります。  
  
## <a name="splitting-the-view"></a>表示の分割  
 編集をしやすくするために、エディター ウィンドウを 2 つに分割することもできます。  
  
#### <a name="to-split-a-window"></a>ウィンドウを分割するには  
  
1.  スクロール バーの上にある分割バーをクリックします。  
  
2.  分割バーを下にドラッグします。  
  
3.  単一のペインに戻すには、2 つのペインに分割している分割バーをダブルクリックします。  
  
 新しいペインには同じドキュメントが含まれているので、そのペインにドキュメント内の同じ場所が表示されている間は、1 つのペインに対して行われた変更が他のペインに反映されます。  
  
## <a name="word-wrap"></a>右端で折り返す  
 [右端で折り返す] を有効にすると、水平スクロール バーが取り除かれ、エディターのウィンドウ幅を超えるコード行は、自動的に折り返されて次の行に表示されるので、表示できない部分がウィンドウの端に隠れてしまうことはありません。  
  
#### <a name="to-activate-word-wrap"></a>右端で折り返す機能を有効にするには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[テキスト エディター]** をクリックします。  
  
3.  適切な言語フォルダーを開きます (または **[すべての言語]** ですべての言語を対象にします)。  
  
4.  
  **[右端で折り返す]** を選択します。  
  
## <a name="enabling-virtual-space-mode"></a>仮想空間モードの有効化  
 
  **仮想空間** モードの場合、エディターは、各行の終わり以降の空間が無数のスペースで埋められているかのような処理を行い、コード行は画面の表示可能領域を超えて 1 行で表示されます。  
  
#### <a name="to-enable-virtual-space-mode"></a>仮想空間モードを有効にするには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[テキスト エディター]** をクリックします。  
  
3.  適切な言語フォルダーを開きます (または **[すべての言語]** ですべての言語を対象にします)。  
  
4.  
  **[仮想空間を使用]** を選択します。  
  
 仮想空間モードが無効な場合、カーソルは、ある行の最後から次の行の最初の文字に折り返されます。逆の場合も同様です。  
  
## <a name="displaying-line-numbers"></a>行番号の表示  
 コード行に行番号を付けることができます。 行番号は、コード内を移動する際に便利です。 詳細については、「 [コード内とテキスト内の移動](navigate-code-and-text.md)」を参照してください。  
  
> [!NOTE]  
>  行番号を有効にしても、ドキュメントの印刷時に行番号が印刷されるわけではありません。 行番号を印刷するには、 **[ファイル]** メニューの **[ページ設定]** コマンドを選択し、 **[行番号]** チェック ボックスをオンにする必要があります。  
  
#### <a name="to-display-line-numbers-in-code"></a>コードの行番号を表示するには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[テキスト エディター]** をクリックします。  
  
3.  
  **[すべての言語]** をクリックします。  
  
4.  [**一般**] をクリックします。  
  
5.  
  **[行番号]** を選択します。  
  
 一部のプログラミング言語のみで行番号を指定するには、該当する言語フォルダーの **[行番号]** を選択します。  
  
## <a name="enabling-full-screen-mode"></a>全画面モードの有効化  
 全画面モードを有効にすると、すべてのツール ウィンドウが隠れて、ドキュメント ウィンドウだけが表示されます。  
  
#### <a name="to-enable-full-screen-mode"></a>全画面モードを有効にするには  
  
1.  Alt キーと Shift キーを押しながら Enter キーを押すと、全画面モードが有効または無効になります。  
  
## <a name="using-auto-hide-all"></a>[すべて自動的に隠す] の使用  
  
#### <a name="to-hide-all-the-tool-windows-at-once"></a>すべてのツール ウィンドウを一度に隠すには  
  
1.  
  **[ウィンドウ]** メニューの **[すべて自動的に隠す]** を選択します。  
  
  
