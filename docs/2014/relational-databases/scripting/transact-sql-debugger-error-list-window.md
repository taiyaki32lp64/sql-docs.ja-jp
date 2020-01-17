---
title: '[エラー一覧] ウィンドウ'
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- error list window
- SQL Server Management Studio [SQL Server], error list window
ms.assetid: fae6327d-e268-44ae-a474-4a8f8f843129
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1eb74eca33bc92152ea08fad2303b9a8b4ba48e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243087"
---
# <a name="error-list-window-management-studio"></a>[エラー一覧] ウィンドウ (Management Studio)
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **エラー一覧**には、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]クエリエディターの IntelliSense コードから生成された構文エラーとセマンティックエラーが表示されます。  
  
## <a name="features-of-the-error-list"></a>[エラー一覧] の機能  
 
  **[エラー一覧]** は、次の機能を提供します。  
  
-   スクリプトを編集すると、 **クエリ エディターの IntelliSense によって生成されたエラーと警告が** [エラー一覧] [!INCLUDE[ssDE](../../includes/ssde-md.md)] に表示されます。  
  
-   任意のエラー メッセージ エントリをダブルクリックして、エラーを生成したスクリプト ファイルのタブにフォーカスを設定し、エラーの場所に移動することができます。  
  
-   どのエントリを表示するか、および各エントリにどの情報列を表示するかをフィルター選択できます。  
  
-   エラーを修正すると、そのエラー エントリが **[エラー一覧]** から削除されます。  
  
-   
  [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルのタブを閉じると、そのファイルのエラーが **[エラー一覧]** から削除されます。  
  
## <a name="working-with-the-error-list"></a>[エラー一覧] の操作  
 
  **[エラー一覧]** を表示するには、次のいずれかの操作を行います。  
  
-   
  **[表示]** メニューの **[エラー一覧]** をクリックします。  
  
-   Ctrl キーを押しながら\\キーを押し、次に Ctrl キーを押しながら E キーを押します。  
  
 
  **[エラー一覧]** が開いたら、次の操作を行うことで表示をカスタマイズできます。  
  
-   一覧を並べ替えるには、任意の列ヘッダーをクリックします。 並べ替えに使用する列を追加するには、&lt;localizedText&gt;Shift&lt;/localizedText&gt; キーを押しながら、他の列ヘッダーをクリックします。  
  
-   表示する列と非表示にする列を選択するには、ショートカット メニューの **[列の表示]** をクリックします。  
  
-   列の表示順を変更するには、列ヘッダーを左右にドラッグします。  
  
 
  **[エラー一覧]** は特定のエラーに関する詳細情報にリンクしていません。  
  
## <a name="transact-sql-errors-in-management-studio"></a>Management Studio の Transact-SQL エラー  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトのエラーが次の場所に表示されます。  
  
-   
  **[エラー一覧]** には、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] エディターの IntelliSense によって検出されたすべての構文エラーとセマンティック エラーが含まれます。 このエラーの一覧は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトの編集に伴って動的に更新されます。 一覧には、各 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトでエディターが検出したすべてのエラーが含まれます。 エディターは、スクリプト内でエラーを検出した後に、ファイルの解析を停止しません。 
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] エディターの IntelliSense はすべての [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文要素をサポートするわけではありません。 
  **[エラー一覧]** には、IntelliSense がサポートする [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文のエラーのみが含まれます。  
  
-   
  **クエリ エディター ウィンドウの下部にある** [メッセージ] [!INCLUDE[ssDE](../../includes/ssde-md.md)] タブには、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] スクリプトの実行時に [!INCLUDE[tsql](../../includes/tsql-md.md)] から返されたすべてのエラーとメッセージが表示されます。 この一覧は、スクリプトが再び実行されるまで変更されません。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、1 つまたは 2 つのコンパイル エラーを検出すると、バッチの解析を停止します。そのため、 **[メッセージ]** タブにはスクリプトのすべてのエラーが一覧表示されない可能性があります。  
  
 エラーが両方の場所に一覧表示されることがあります。 たとえば、 **[エラー一覧]** に表示されている構文エラーがスクリプト ファイルに含まれている場合があります。 このスクリプトを、エラーを修正する前に実行すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] パーサーが同じ状態を検出し、エラー メッセージの別のコピーを **[メッセージ]** タブに返す可能性があります。  
  
> [!NOTE]  
>  
  **[エラー一覧]** に表示されるのは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターからのエラーのみです。MDX、DMX、または XML/A エディターからのエラーは表示されません。 MDX、DMX、および XML/A のすべてのエラーは、それらのエディターの **[メッセージ]** タブに表示されます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 
  **[エラー一覧]** を開くと、次の列に情報が表示されます。  
  
 **既定の順序**  
 エントリの作成順を示す整数を表示します。  
  
 **記述**  
 エラー エントリのテキストを表示します。 説明文が長い場合には、追加の行に折り返されます。  
  
 **拡張子**  
 エラーを生成したスクリプト ファイルの名前を表示します。  
  
 **直線**  
 エラーを含むコード行を示す整数を表示します。  
  
 **項目**  
 コード行におけるエラーの位置を示す整数を表示します。  
  
 **作品**  
 スクリプト ファイルを含むプロジェクトの名前を表示します。  
