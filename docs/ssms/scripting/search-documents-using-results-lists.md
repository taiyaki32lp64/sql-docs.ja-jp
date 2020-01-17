---
title: 結果一覧を使用してドキュメントを検索する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], result lists
- result list searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], multiple files
- Query Editor [SQL Server Management Studio], search multiple files
ms.assetid: 275e1b6c-fbd0-4408-af77-35903f90657c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc59fb8f6771f2fc11eb940b98396edd09ad6e26
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264182"
---
# <a name="search-documents-using-results-lists"></a>結果一覧を使用してドキュメントを検索する方法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **[検索と置換]** ダイアログ ボックスでは、プロジェクト内、ソリューション内、ファイル システム フォルダー内のすべてのファイルを対象にしてテキストの検索と置換を実行できます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で開いていないファイルも対象になります。 **[検索と置換]** ダイアログ ボックスで実行した検索の一致項目は、[検索結果 1] ウィンドウと [検索結果 2] ウィンドウに表示されるので、一致項目を含んだ行のテキストを実際に確認できます。  
  
### <a name="to-search-in-multiple-files"></a>複数のファイルで検索を実行するには  
  
1.  **[編集]** メニューの **[検索と置換]** をポイントし、 **[フォルダーを指定して検索]** をクリックします。  
  
2.  **[検索する文字列]** テキスト ボックスに検索テキストを入力します。  
  
3.  **[検索対象]** 一覧で、 **[すべての開かれているドキュメント]** 、 **[現在のプロジェクト]** 、 **[ソリューション全体]** のいずれかをクリックするか、ディレクトリ パスを入力します。  
  
4.  **[次のファイルの種類を参照]** 一覧で、表示されているファイル拡張子のセットのいずれかを選択するか、検索対象のファイルの種類を示す拡張子をセミコロンで区切って入力します。 **[検索対象]** ドロップダウン リストに表示されているディレクトリ内のすべてのファイルを検索する場合は、\*.\* を使います。  
  
5.  検索の精度を上げるために、他の検索オプションの中から適切な項目を選択します。  
  
6.  **[検索]** をクリックして検索を開始します。  
  
 既定では、[検索結果 1] ウィンドウに検索の一致項目が表示されます。 検索の一致項目を確認するには、[検索結果 1] ウィンドウ内の各項目をダブルクリックします。 検索結果を新しいウィンドウに表示するには、 **[検索結果 2 ウィンドウ]** を選択します。  
  
#### <a name="to-replace-across-multiple-files-or-folders"></a>複数のファイルまたはフォルダーで置換を実行するには  
  
1.  **[編集]** メニューの **[検索と置換]** をポイントし、 **[フォルダーを指定して置換]** をクリックします。  
  
2.  **[検索する文字列]** テキスト ボックスに検索テキストを入力します。  
  
3.  **[置換後の文字列]** ボックスに置換後のテキストを入力します。  
  
4.  **[検索対象]** 一覧で、 **[すべての開かれているドキュメント]** 、 **[現在のプロジェクト]** 、 **[ソリューション全体]** のいずれかをクリックするか、ディレクトリ パスを入力します。  
  
5.  **[置換]** をクリックすると、現在の検索一致項目が **[置換後の文字列]** ボックス内のテキストに置換されます。 1 つの一致項目をスキップする場合は **[次を検索]** をクリックし、ファイル全体をスキップする場合は **[ファイルのスキップ]** をクリックします。  
  
     \- - または -  
  
     **[すべて置換]** をクリックすると、すべての検索一致項目が **[置換後の文字列]** ボックス内のテキストに置換されます。 後から一部の置換項目を元に戻す可能性がある場合は、 **[置換後に、変更したファイルを閉じない]** を選択します。  
  
    > [!NOTE]  
    >  **[すべて置換]** は、すべての検索一致項目を対象としており、その中には **[ファイルのスキップ]** や **[次を検索]** によってスキップしたファイル内の一致項目も含まれます。 **[元に戻す]** を使用できるのは、置換操作後に開いたままにしておいたファイル内の置換項目に限られます。  
  
 既定では、[検索結果 1] ウィンドウに置換情報が表示されます。 置換項目を確認するには、[検索結果 1] ウィンドウ内の各項目をダブルクリックします。  
  
## <a name="see-also"></a>参照  
 [検索と置換](../../relational-databases/scripting/search-and-replace.md)   
 [ドキュメントの対話形式の検索](../../relational-databases/scripting/search-documents-interactively.md)   
 [ワイルドカードを使用したテキスト検索](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [正規表現によるテキストの検索](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
