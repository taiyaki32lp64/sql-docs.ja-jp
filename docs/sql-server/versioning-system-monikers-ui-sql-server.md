---
title: SQL ドキュメントのバージョン管理システム | Microsoft Docs
ms.date: 10/15/2019
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: conceptual
ms.reviewer: ''
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||>=sql-server-linux-2017||=sql-server-previousversions||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f175e9639b07c945b92b6fd715fa8b34ebea60c3
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049905"
---
# <a name="versioning-system-for-sql-documentation"></a>SQL ドキュメントのバージョン管理システム

[!INCLUDE[includes_appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

この記事では、SQL ドキュメントの "_バージョン管理システム_" について説明します。 バージョン管理システムでは、製品とそのバージョンについて認識しています。 ユーザーは、システムで関心のある製品とバージョンを選択できます。 その後、システムによって適切なドキュメントが表示されます。

## <a name="applies-to-products"></a>適用対象の製品

SQL Server のほとんどの記事には、タイトルの下に「**適用対象**」という語があります。 同じ行に、続けて、SQL "_製品_" の一覧と、記事がその製品に関連するかどうかを示す記号が記載されています。 たとえば、製品 SQL Server は記事に関係ありと示されていて、Azure SQL Database は関係なしと示されていることがあります。

「**適用対象**」の行では、製品の "_バージョン_" はわかりません。 「**適用対象**」の行とバージョン管理システム構成の製品に関しては食い違いがないように努めています。

## <a name="history-of-separate-file-sets"></a>個別のファイル セットの履歴

SQL Server 2014 以前のバージョンでは、バージョンごとにドキュメント ファイルの完全に独立したコピーがあります。 たとえば、SQL Server 2014 のドキュメントは、SQL Server 2012 のドキュメントのコピーとして始まりました。 その後、製品開発サイクルの間に 2014 のコピーが編集されました。

この古いアプローチでは、2014 のドキュメントで欠陥が見つかった場合、その欠陥は 2012 や 2008 にも存在する可能性があることを意味しました。 これにより、欠陥の修正や一般的な保守の困難さが増していました。

## <a name="multiple-versions-in-the-same-files"></a>同じファイル内の複数のバージョン

これや他の理由により、SQL Server 2016 を対象とするドキュメント ファイルは、2017、2019、そしておそらくは \<vNext\> も対象になっています。 この統合は、SQL Server のドキュメント ファイルに "_バージョン管理モニカー_" を割り当てることで実現されています。 特定のドキュメント ファイルごとに、どのようなレベルでも細分化することに意味がある箇所には、バージョン管理モニカーが割り当てられ (明示的に埋め込まれ) ます。

## <a name="versioning-control-in-the-ui"></a>UI でのバージョン管理コントロール

:::no-loc text="Docs"::: Web サイトを使用して SQL ドキュメントの記事を表示すると、目次 (TOC) の上に現在選択されているバージョン管理モニカーが表示されます。 コントロールはドロップダウン リストです。

![media_versioning-control-10-sql-server-2017.png](media/versioning-control-10-sql-server-2017.png)

異なるバージョンの SQL Server のドキュメントを見たい場合は、現在のバージョン モニカーの末尾にある展開矢印をクリックします。 次に、目的の製品とバージョンの組み合わせをクリックして選択します。 異なるバージョンをクリックすると、表示されているドキュメントがすぐに変化し、新しく選択したバージョンの違いが表示されます。 違いがある場合もない場合もあり、どちらも普通のことです。

![media_versioning-control-20-expanded.png](media/versioning-control-20-expanded.png)

### <a name="https-parameter-no-loc-textview"></a>HTTPS パラメーター :::no-loc text="view=":::

Web アドレスが `https://docs.microsoft.com/sql/` で始まっている各記事では、`?view=` という名前のパラメーターがアドレスに付加されています。 このパラメーター値は、バージョン管理モニカー コードです。

`https` アドレス内のモニカー "_コード_" は、バージョン管理コントロールに表示されるモニカー "_名_" と常に一致します。

## <a name="products-not-editions"></a>エディションではなく製品

### <a name="editions"></a>エディション

1990 年代から 2000 年代にかけては、Microsoft SQL Server には 1 つの製品しかありませんでした。 SQL Server 2008 の _Developer_ エディションや _Enterprise_ エディションなど、SQL Server の各バージョンにはさまざまな "_エディション_" がありました。 エディションでは、わずかに異なる機能セットが示されていましたが、コア製品は同じでした。 新しい SQL Server のリリースにも、さまざまなエディションが含まれている場合があります。

### <a name="products"></a>Products

最近のクラウド コンピューティングと Microsoft Azure の登場により、Microsoft は Azure SQL Database 製品をリリースしました。 従来の SQL Server オンプレミス製品と Azure SQL Database 製品では多くのコードが共有されていますが、これらは 2 つの完全に独立した製品です。

SQL のバージョン管理モニカーでは、製品間で区別されますが、エディション間は区別されません。

#### <a name="azure-cloud-sql-products"></a>Azure クラウド SQL 製品

Web アドレスが `https://docs.microsoft.com/sql/` で始まっている記事のほとんどすべては、SQL Server という名前の製品の少なくとも 1 つのバージョンに適用されます。 それらの記事の大きなサブセットは、Azure クラウドでホストされている 1 つ以上の SQL サービス製品にも当てはまります。 そのような SQL クラウド製品の 1 つは Azure SQL Database という名前です。

当然ながら、Azure SQL Database 製品にはバージョンが 1 つしかありません。 Azure SQL Database に適用されて、SQL Server には適用されない記事のほとんどすべては、Web アドレスが `https://docs.microsoft.com/azure/sql-database/` で始まっています。

## <a name="scenarios-of-version-filtering"></a>バージョンのフィルター処理のシナリオ

バージョン管理システムは、現在アクティブなモニカーに適用されないすべてのドキュメント コンテンツをフィルターで除外することにより機能します。 ユーザーが異なるバージョン管理モニカーを選択するたびに、非表示になるコンテンツのセットが変わります。 フィルター処理により、コンテンツは次のレベルで非表示になります。

- 記事内のセクションまたはセンテンス。
- 目次 (TOC) 内の記事のエントリ。

次に、別のモニカーを選択した場合の影響について説明します。

### <a name="scenario-1-within-the-current-article"></a>シナリオ 1:現在の記事内

次のシナリオでは、現在の記事内のセクションに焦点を当てています。

1. 現在のバージョン管理モニカーは **SQL Server 2017** です。
2. SQL Server のバージョン 2017 で最初に追加された機能について説明されているセクションを読んでいます。
3. モニカーを **SQL Server 2016** に変更します。
4. 読んでいたセクションが消えていることがわかります。
5. もう一度、今度は **SQL Server 2019** にモニカーを変更します。
6. 読んでいた 2017 のセクションが再び表示されるようになったことがわかります。

上のシナリオでは、2017 の新機能に関するセクションは、おそらく、次のモニカー コードを含む "_モニカー範囲_" でマークされています。

- `>=sql-server-2017`

モニカー **SQL Server 2019** を選択したときは、バージョン管理システムによって 2019 が 2017 以上であることが認識され、セクションが表示されました。

### <a name="scenario-2-click-a-link-to-a-hidden-article"></a>シナリオ 2: 非表示の記事へのリンクをクリックする

次の一般的ではないシナリオでは、現在目次 (TOC) で非表示になっている記事へのリンクをクリックした場合の動作について説明します。 簡単に言えば、リンクは次のように機能します。

1. 現在のバージョン管理モニカーは **SQL Server 2017** です。
2. 現在の記事 :::no-loc text="A"::: で、SQL Server 2016 にのみ適用される記事 :::no-loc text="B"::: へのリンクをクリックします。
    - クリックする前は、目次には記事 :::no-loc text="B"::: に対するエントリは表示されていません。
3. クリックすると、記事 :::no-loc text="B"::: が表示されます。
    - 記事 :::no-loc text="B"::: が表示されることで、バージョン管理コントロールは強制的に **SQL Server 2016** モニカーに切り替わります。
    - 元のモニカー **SQL Server 2017** を破棄する必要があったためです。 この破棄により、情報メッセージが Web ページの上部付近に表示されます。 [メッセージ](#anchor-message-unavailable-for-moniker)では、新しい記事 :::no-loc text="B"::: に対応するために現在のモニカーを切り替える必要があったことが説明されています。

### <a name="scenario-3-navigate-to-an-https-address"></a>シナリオ 3: HTTPS アドレスに移動する

次の記事は、SQL Server 2017 で新しく追加されました。 記事では、バージョン 2017 の SQL Server に追加された機能について説明されています。 それらの新機能のほとんどまたはすべては、バージョン 2019 にも含まれます。 記事の属性は次のとおりです。

| 属性 | [値] |
| :-------- | :---- |
| [タイトル] | SQL Server 2017 の新機能 |
| モニカー範囲 | `>= sql-server-2017 || = sqlallproducts-allversions` |
| `https` アドレス | `https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017` |
| &nbsp; | &nbsp; |

次の表では、ベース アドレスが `https` の場合に、ユーザーが `?view=` パラメーターとさまざまな値を追加したときの動作について説明します。

| `?view=` の値 | `https` アドレス ナビゲーションの動作 |
| :---------------- | :------------------------------ |
| _(パラメーターなし。)_ | バージョン管理システムでは、既定のモニカー値が試されます。 通常、これは SQL Server のプレビュー版ではない最新バージョンに設定されています。<br/><br/>SQL Server 2017 または 2019 の既定値では、属性 `>= sql-server-2017` が満たされます。<br/><br/>システムでは、`https` アドレスにパラメーターが追加されます (`?view=sql-server-2017` など)。<br/>その後、バージョン管理ドロップダウン リスト コントロールが、一致するモニカー名に設定されます。 |
| `sql-server-2016` | バージョン管理システムでは、記事のモニカー範囲にバージョン 2016 が含まれていないことが認識されます。<br/><br/>次に、システムで範囲を満たすモニカーのいずれかが選択されます。<br/><br/>次に、バージョン 2016 の場合と同様に、パラメーター `?view=` が追加され、コントロール名がパラメーター値と一致するように設定されます。 |
| `sql-server-2017` | バージョン管理システムで、パラメーター値が記事のモニカー範囲に含まれることが認識されます。<br/><br/>バージョン管理コントロールは、パラメーター値と一致するように設定されます。 |
| `sql-server-2019` | パラメーターとコントロールが 2019 に設定されることを除き、値 `sql-server-2017` の場合と同じです。 |
| &nbsp; | &nbsp; |

### <a name="anchor-allsql-hidenothing"></a> All SQL - 何も非表示にしない、特別なモニカー

**All SQL** という 1 つの特殊なモニカー製品名があり、その唯一のバージョンは **Hide nothing** です。 このモニカーの目的は、特定の変更の内部テスト用です。 お客様がこのモニカーを使用した場合、情報提供というよりは誤解される可能性が高くなります。

記事の中には、SQL Server の複数のバージョンに関する情報が含まれるものがあります。 通常のすべてのモニカーでは、モニカーのバージョンについて正確でない、紛らわしい、または矛盾している情報が表示される可能性があるバージョン管理されたセクションは表示されません。 特別な **All SQL** モニカーでは、すべてのバージョンのセクションが表示され、不正確な情報が表示されていることが明らかでない場合があります。

## <a name="anchor-message-unavailable-for-moniker"></a> メッセージ: リクエストされたページは \<モニカー\> で表示できません

次のシナリオでは、:::no-loc text="Docs"::: Web ページの上部に情報メッセージが表示されます。

1. 現在のバージョン管理モニカーは **SQL Server 2017** です。
2. あなたは SQL Server 2017 に関する記事を読んでいます。
    - 記事は、製品 Azure SQL Database には関連して "_いません_"。
3. あなたはモニカーを **Azure SQL Database - current** に変更しようとします。
4. 試行が拒否され、メッセージが表示されます。

このシナリオの最後に、ドキュメント Web ページの上部に次のような情報メッセージが表示されます。

> リクエストされたページは Azure SQL Database - current で表示できません 最新の製品バージョンで表示できるこのページにリダイレクトされました。

"_最新_" バージョンでは、まだ完全にリリースされておらず、"_プレビュー_" 状態にあるバージョンが除外される場合があります。

![media_versioning-control-30-viewfallbackfrom.png](media/versioning-control-30-viewfallbackfrom.png)

## <a name="previous-versions-of-sql-server"></a>SQL Server の以前のバージョン

バージョン管理システムは、SQL Server バージョン 2016 以降で完全に実装されています。

- _2012 以前:_ &nbsp; バージョン管理システムは、SQL Server 2012 以前のバージョンでは使用されません。
    - 特別なモニカー **SQL Server - older** では、ほとんどすべての記事が非表示になります。 まれに例外として、以前のバージョンのお客様がかつて必要としたことがある記事が表示されます。
    - [SQL Server の以前のバージョン、2012 - 2005](../toc/previous-versions-sql-server.md)

- _2014:_ &nbsp; バージョン管理システムは、SQL Server 2014 では半分実装されています。 バージョン管理コントロールで SQL Server 2014 を選択することができ、動作します。 ただし、内部的には、2008 のファイルが 2008 専用であるのと同じように、2014 のファイルは 2014 のみを対象としています。
    - [SQL Server 2014 のドキュメント](/sql/2014-toc/books-online-for-sql-server-2014?view=sql-server-2014)

- _2016 以降:_ &nbsp; バージョン管理システムは、SQL Server バージョン 2016 以降のバージョンでは完全に実装されています。
    - [SQL Server 2016 以降のドキュメントへようこそ](/sql/sql-server/?view=sql-server-2016)

## <a name="see-also"></a>参照

[SQL Server の以前のバージョン、2014 - 2005](../toc/previous-versions-sql-server.md)  
[SQL Server ドキュメント ナビゲーション ガイド](sql-docs-navigation-guide.md)  
[SQL Server のドキュメントに投稿する方法](sql-server-docs-contribute.md)  
