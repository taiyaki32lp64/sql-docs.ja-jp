---
title: コードの書式設定の管理
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- indenting code [SQL Server]
- displaying URLs
- code formatting [SQL Server Management Studio]
- collapsing text
- formats [SQL Server], code formatting in SQL Server Management Studio
- hiding text
- formats [SQL Server]
- text [SQL Server], code formats
- automatic indentation
- converting text to lower case
- Query Editor [SQL Server Management Studio], managing code formats
- URL displayed in code [SQL Server Management Studio]
- converting text to upper case
- text [SQL Server]
- unindenting code
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e25a5438eb147cfe5e3c7e4df3d3fe504cfcda48
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242020"
---
# <a name="manage-code-formatting"></a>コードの書式設定の管理
  エディターでは、コードに関して、インデント設定、テキストの非表示、URL などの書式設定を行えます。 スマート インジケーターを使用して、入力と同時にコードを自動的に書式設定することも可能です。  
  
## <a name="indenting"></a>インデント  
 テキストのインデントは、3 種類のスタイルから選択できます。 また、1 つのインデントまたはタブのスペース数や、エディターでタブとスペースのどちらの文字を使用してインデントするかを指定できます。  
  
#### <a name="to-choose-an-indenting-style"></a>インデントのスタイルを選択するには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[テキスト エディター]** をクリックします。  
  
3.  すべての言語のインデントを設定するために **[すべての言語]** フォルダーをクリックします。  
  
4.  
  **[タブ]** をクリックします。  
  
5.  以下のいずれかのオプションをクリックします。  
  
    -   **なし**。 カーソルは次の行の先頭に移動します。  
  
    -   **ブロック**。 次行のインデントは前行に合わせて設定されます。  
  
    -   **スマート**(既定値)。 適切なインデント スタイルが言語サービスによって決定されます。  
  
    > [!NOTE]  
    >  一部の言語では、3 種類のインデント オプションがすべて用意されているわけではありません。  
  
#### <a name="to-change-indent-tab-settings"></a>インデントのタブの設定を変更するには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[テキスト エディター]** をクリックします。  
  
3.  すべての言語のインデントを設定するために **[すべての言語]** フォルダーをクリックします。  
  
4.  
  **[タブ]** をクリックします。  
  
5.  タブ操作とインデント操作でタブ文字を使用するように指定するには、 **[タブの保持]** をクリックします。 スペース文字を使用するように指定するには、 **[空白の挿入]** をクリックします。  
  
     
  **[空白の挿入]** をクリックした場合は、各タブまたはインデントに相当するスペース文字の数を **[タブ サイズ]** または **[インデント サイズ]** に入力します。  
  
#### <a name="to-indent-code"></a>コードにインデントを設定するには  
  
1.  インデントを設定するテキストを選択します。  
  
2.  Tab キーを押すか、標準ツール バーの **[インデント]** をクリックします。  
  
#### <a name="to-unindent-code"></a>コードのインデントを解除するには  
  
1.  インデントを解除するテキストを選択します。  
  
2.  Shift キーを押しながら Tab キーを押すか、標準ツール バーの **[インデントの解除]** をクリックします。  
  
#### <a name="to-automatically-indent-all-of-your-code"></a>すべてのコードに自動的にインデントを設定するには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[テキスト エディター]** をクリックします。  
  
3.  
  **[すべての言語]** をクリックします。  
  
4.  
  **[タブ]** をクリックします。  
  
5.  
  **[スマート]** をクリックします。  
  
> [!NOTE]  
>  一部の言語では、 **[スマート]** オプションを使用できません。  
  
#### <a name="to-convert-white-space-to-tabs"></a>スペースをタブに変換するには  
  
1.  スペースをタブに変換するテキストを選択します。  
  
2.  
  **[編集]** メニューの **[詳細設定]** をポイントし、 **[選択行にタブを設定]** をクリックします。  
  
#### <a name="to-convert-tabs-to-spaces"></a>タブをスペースに変換するには  
  
1.  タブをスペースに変換するテキストを選択します。  
  
2.  
  **[編集]** メニューの **[詳細設定]** をポイントし、 **[選択行のタブの設定を解除]** をクリックします。  
  
 これらのコマンドの動作は、 **[オプション]** ダイアログ ボックスのタブ設定によって異なります。 たとえば、タブ設定が 4 の場合、 **[選択行にタブを設定]** をクリックすると 4 つの連続したスペースに対して 1 つのタブが作成され、 **[選択行のタブの設定を解除]** をクリックすると 1 つのタブに対して 4 つのスペースが作成されます。  
  
## <a name="converting-text-to-upper-and-lower-case"></a>大文字のテキストまたは小文字のテキストへの変換  
 テキストをすべて大文字または小文字に変換するためのコマンドを使用できます。  
  
#### <a name="to-switch-text-to-upper-or-lower-case"></a>テキストを大文字または小文字に切り替えるには  
  
1.  変換するテキストを選択します。  
  
2.  テキストを大文字に変換するには、Ctrl キーと Shift キーを押しながら U キーを押すか、 **[編集]** メニューの **[詳細設定]** サブメニューの **[大文字に変換]** をクリックします。  
  
3.  テキストを小文字に変換するには、Ctrl キーと Shift キーを押しながら L キーを押すか、 **[編集]** メニューの **[詳細設定]** サブメニューの **[小文字に変換]** をクリックします。  
  
> [!NOTE]  
>  キーボード ショートカット キーの完全な一覧については、「 [SQL Server Management Studio のキーボード ショートカット](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)」を参照してください。  
  
## <a name="displaying-and-linking-to-urls"></a>URL の表示とリンクの設定  
 クリック可能な URL をコード内に作成して、表示できます。 URL の既定の設定は以下のとおりです。  
  
-   下線が付きます。  
  
-   マウスのポインターを URL の上に置くと、ポインターが手の形に変わります。  
  
-   URL が有効な場合は、クリックするとその URL が開きます。  
  
#### <a name="to-display-a-clickable-url"></a>クリック可能な URL を表示するには  
  
1.  
  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  
  **[テキスト エディター]** をクリックします。  
  
3.  1 つの言語のオプションだけを変更する場合は、その言語のフォルダーをクリックし、 **[全般]** をクリックします。 すべての言語のオプションを変更する場合は、 **[すべての言語]** 、 **[全般]** の順にクリックします。  
  
4.  
  **[シングルクリックでの URL ナビゲーションを有効にする]** をオンにします。  
  
  
