---
title: オプション (テキスト エディターの TRANSACT-SQL - タブ ページ) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Tabs
dev_langs:
- TSQL
ms.assetid: a4499784-67f7-46ef-9f7c-2d0fdd117a52
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: cc649ee021012774a0f199b97ea3cbf6bae4adef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089135"
---
# <a name="options-text-editor---transact-sql---tabs-page"></a>オプション ([テキスト エディターの TRANSACT-SQL - タブ] ページ)
  このダイアログ ボックスを使用すると、[!INCLUDE[ssDE](../includes/ssde-md.md)] スクリプトのプログラミングに使用される[!INCLUDE[tsql](../includes/tsql-md.md)] クエリ エディターのタブの動作を変更できます。 この設定を表示するには、 **[ツール]** メニューの **[オプション]** をクリックして、 **[テキスト エディター]** フォルダーを展開し、さらに **[Transact-SQL]** サブフォルダーを展開して、 **[タブ]** をクリックします。  
  
## <a name="setting-options-in-multiple-locations"></a>複数の場所でのオプション設定  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] クエリ エディターのオプションは、 **[すべての言語] の [タブ]** ダイアログで設定することもできます。 ただし、DMX エディターや MDX エディターなど、他の **エディターに対し、** [すべての言語] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のダイアログを使用して異なるオプションを設定する場合は、ここで紹介したダイアログを使用して [!INCLUDE[ssDE](../includes/ssde-md.md)] クエリ エディターのオプションを設定し直す必要があります。  
  
## <a name="indenting"></a>インデント  
 **None**  
 このオプションが選択されている場合、Enter キーを押したときに作成される新しい行は、インデントされません。 カーソルは、新しい行の 1 列目に置かれます。  
  
 **ブロック**  
 このオプションが選択されている場合、Enter キーを押したときに作成される新しい行は、直前の行と同じ位置まで自動的にインデントされます。  
  
 **スマート**  
 このオプションは使用できません。  
  
## <a name="tabs"></a>タブ  
 **[タブ サイズ]**  
 タブ ストップ間の間隔をスペース数で設定します。 既定値は、スペースが 4 つです。  
  
 **インデントのサイズ**  
 自動インデントのサイズをスペース数で設定します。 既定値は、スペースが 4 つです。 指定されたサイズになるように、タブ文字、スペース文字、またはその両方が挿入されます。  
  
 **スペースを挿入します。**  
 このオプションを選択すると、タブ文字を使用せずにスペース文字だけを挿入してインデントします。 たとえば **[インデント サイズ]** が 5 に設定されている場合、 のメイン ウィンドウで **キーを押すか、ツール バーの [** インデント [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ] ボタンを押すごとに、5 つのスペース文字が挿入されます。  
  
 **タブを保持します。**  
 このオプションを選択すると、インデントするときにできる限り多くのタブ文字を挿入します。 それぞれのタブ文字が、 **[タブ サイズ]** で指定された数のスペースを満たします。 **[インデント サイズ]** が **[タブ サイズ]** の倍数でない場合は、その差を埋めるためにスペース文字が追加されます。  
  
  
