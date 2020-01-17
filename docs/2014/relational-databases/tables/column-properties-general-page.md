---
title: '[列のプロパティ] ([全般] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.columnproperties.general.f1
ms.assetid: a745890b-994e-4c23-8028-5c83751e60c4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 741c8633a9b7eed9fcd253918c34a27119e51ee4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62854905"
---
# <a name="column-properties-general-page"></a>[列のプロパティ] \([全般] ページ)
  このページを使用すると、選択されている列のプロパティを表示できます。  
  
 このページの情報は読み取り専用です。 列を変更するには、 **[列のプロパティ]** ダイアログ ボックスを閉じて、オブジェクト エクスプローラーでそのテーブルを展開して [列] を展開します。次に、列を右クリックして、 **[デザイン]** をクリックします。  
  
## <a name="options"></a>および  
 **名前**  
 列の名前です。  
  
 **[データ型]**  
 列が保持できるデータ型です。 データ型がユーザー定義データ型である場合は、ユーザー定義データ型が表示されます。 データ型がユーザー定義データ型でない場合は、システム データ型が表示されます。 詳細については、「[データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)」を参照してください。  
  
 **[システム型]**  
 列が保持できるデータ型です。 データ型がシステム データ型である場合は、システム データ型が表示されます。 データ型がユーザー定義型である場合は、ユーザー定義データ型を形成するシステム データ型が表示されます。  
  
 **主キー**  
 列が主キーであるかどうかを示します。 指定できる値は、 **[True]** および **[False]** です。  
  
 **Null を許容**  
 列が NULL 値を許容するかどうかを示します。 指定できる値は、 **[True]** および **[False]** です。  
  
 **[計算値]**  
 列の値が、計算された式の結果であるかどうかを示します。  
  
 **[計算されたテキスト]**  
 列テキストの計算に使用されたステートメントを示します。 詳細については、「 [テーブルの計算列の指定](specify-computed-columns-in-a-table.md)」を参照してください。  
  
 **[ID]**  
 列がテーブルの ID 列であるかどうかを示します。 指定できる値は、 **[True]** および **[False]** です。  
  
 **[IDENTITY シード]**  
 ID 列の最初の行の値を示します。  
  
 **[IDENTITY インクリメント]**  
 **[ID の増分値]** プロパティは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で挿入される行の ID 値が生成されるときに、既存の行の最大 ID 値に追加される値を指定します。  
  
 **[既定のバインド]**  
 列にバインドされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定値です。 既定値がバインドされていない場合、このオプションは空白になります。  
  
 **[既定のスキーマ]**  
 参照される列にバインドされた既定値を所有するデータベース スキーマを識別します。 既定値がバインドされていない場合、このオプションは空白になります。  
  
 **Rule**  
 列にバインドされたデータ整合性制約を識別します。 ルールがバインドされていない場合、このオプションは空白になります。  
  
 **[ルール スキーマ]**  
 参照される列にバインドされたルールを所有する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース スキーマを表示します。 ルールがバインドされていない場合、このオプションは空白になります。  
  
 **Length**  
 列によって許容される文字またはバイトの最大数を示します。  
  
 **[照合順序]**  
 列の現在の照合順序を表示します。 空白の場合、照合順序プロパティはオブジェクトから継承されます。  
  
 **[数値有効桁数]**  
 固定精度の数値データ型における最大桁数を示します。  
  
 **[数値の小数点以下桁数]**  
 固定精度の数値データ型における小数点以下桁数を示します。  
  
 **[XML スキーマ名前空間]**  
 XML Schema Definition Language (XSD) 検証で XML 列の種類を定義します。  
  
 **[XML スキーマ名前空間スキーマ]**  
 XML スキーマ名前空間を所有する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スキーマです。  
  
> [!NOTE]  
>  一般にスキーマという語にはいくつかの異なる意味があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベース オブジェクトを編成する場合にスキーマを使用します。 これは所有権に似ています。 XML は、スキーマを使用して XML 情報の編成を一連の名前空間に定義します。 このスキーマは、XML コードをまとめてグループ化する方法です。  
  
 **[スパース]**  
 列がスパース列であるかどうかを示します。 指定できる値は、 **[True]** および **[False]** です。 詳細については、「 [スパース列の使用](use-sparse-columns.md)」を参照してください。  
  
 **[列セット]**  
 列が列セットであるかどうかを示します。 指定できる値は、 **[True]** および **[False]** です。 詳細については、「 [列セットの使用](use-column-sets.md)」を参照してください。  
  
 **[ANSI PADDING の状態]**  
 ANSI PADDING が有効かどうかを示します。 詳細については、「[SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)」を参照してください。  
  
 **[フルテキスト]**  
 列がフルテキスト クエリに参加するかどうかを表示します。  
  
 **[統計的セマンティクス]**  
 列に対する統計的セマンティック検索を有効にするかどうかを示します。 詳細については、「[セマンティック検索 &#40;SQL Server&#41;](../search/semantic-search-sql-server.md)」を参照してください。  
  
 **[レプリケーションでは使用しない]**  
 列をレプリケーションに使用できるかどうかを示します。 指定できる値は、 **[True]** および **[False]** です。  
  
  
