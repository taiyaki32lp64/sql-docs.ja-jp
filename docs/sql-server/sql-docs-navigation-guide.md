---
title: SQL Server ドキュメント ナビゲーションのヒント
description: SQL Server 技術ドキュメントを参照する際のヒントとテクニックです。ハブ ページ、目次、ヘッダー、階層リンクの使用方法、バージョン フィルターの使用方法などについて説明します。
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e0a18b05395cffaa4154e8f4a7d74ed04750e430
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72904311"
---
# <a name="sql-server-docs-navigation-guide"></a>SQL Server ドキュメント ナビゲーション ガイド 

このトピックでは、SQL Server 技術ドキュメント領域を参照する際のヒントとテクニックについて説明します。  

## <a name="hub-page"></a>ハブ ページ

SQL Server のハブ ページは、[https://aka.ms/sqldocs](https://aka.ms/sqldocs) にあり、関連する SQL Server コンテンツを検索するためのエントリポイントです。

SQL Server 技術ドキュメント セット内の各ページの上部にあるヘッダーにある **[SQL ドキュメント]** を選択すると、いつでもこのページに戻ることができます。 

![ヘッダーの [SQL ドキュメント]](media/sql-server-docs-navigation-guide/sql-docs-in-header.png)

## <a name="offline-documentation"></a>オフライン ドキュメント

SQL Server のドキュメントをオフライン システムで表示するには、2 つのオプションがあります。 SQL Server 技術ドキュメントを使用中にいつでも PDF を作成できます。または、[SQL Server のオフラインのヘルプ ビューアー](sql-server-help-installation.md)を使用してオフラインのコンテンツをダウンロードできます。 

PDF を作成する場合は、すべての目次の下部にある **[Download PDF]\(PDF をダウンロード\)** リンクを選択します。


![[Download PDF]\(PDF をダウンロード\)](media/sql-server-docs-navigation-guide/download-pdf.png)

## <a name="toc-navigation-hints"></a>目次のナビゲーションのヒント

エントリの最後に `>` がある目次 (TOC) のエントリは、別の目次を含む技術ドキュメントにリンクされていることを示します。 

![目次のシングル キャロット](media/sql-server-docs-navigation-guide/single-carrots-in-sql-docs-toc.png)

`>>` がある目次のエントリは、docs.microsoft.com 以外にリンクされていることを示します。 

![目次のナビゲーション マーカー](media/sql-server-docs-navigation-guide/double-carrots-in-sql-docs-toc.png)

このようなページのいずれかに移動した場合、メインの SQL Server 技術ページと目次に戻るには、各目次の上部にある「Welcome to SQL Server >」(SQL Server へようこそ >) エントリを選択します。 

![SQL の目次に戻る](media/sql-server-docs-navigation-guide/navigate-back-to-sql-toc.png)

## <a name="toc-search-tip"></a>目次の検索のヒント
docs.microsoft.com では、上部にあるフィルター検索ボックスを使用して、目次内のコンテンツを検索できます。 

![フィルター ボックスを使用する](media/sql-server-docs-navigation-guide/sql-docs-toc-filter.gif)

## <a name="version-filter"></a>バージョン フィルター
SQL Server 技術ドキュメントには、SQL Server のいくつかのサポートされているバージョンとフレーバーのコンテンツが記載されています。 機能は SQL Server のバージョンとフレーバーによって異なる場合があります。そのため、コンテンツ自体が異なる場合があります。 

[バージョン フィルター](versioning-system-monikers-ui-sql-server.md)を使用すると、SQL Server の適切なバージョンとフレーバーのコンテンツを確実に表示できます。 

![SQL ドキュメントのバージョン フィルター](media/sql-server-docs-navigation-guide/sql-docs-version-filter.gif)

**[All SQL]\(すべての SQL\)** \> **[Hide nothing]\(すべて表示\)** を選択すると、すべてのコンテンツが表示され、バージョン フィルターによる非表示が解除されます。 「**Hide nothing**」オプションを選択すると、同じ記事内に複数の異なるバージョンの SQL Server に関連するコンテンツが表示されることがあり、矛盾したり、不明確であったり、紛らわしいことがあります。 そのため、[「**Hide nothing**」オプションは、通常の使用にはお勧めしません](versioning-system-monikers-ui-sql-server.md#anchor-allsql-hidenothing)。 

## <a name="breadcrumbs"></a>階層リンク

階層リンクは、ヘッダーの下と目次の上にあり、現在の記事が目次内のどこにあるかを示します。  これによって読んでいるコンテンツの種類にコンテキストを設定できるだけでなく、目次ツリーの上に戻ることもできます。

![SQL ドキュメントの階層リンク](media/sql-server-docs-navigation-guide/sql-docs-bread-crumbs.gif)


## <a name="article-section-navigation"></a>記事セクションのナビゲーション

右側のナビゲーション ウィンドウでは、記事内のセクションにすばやく移動したり、記事内の場所を特定したりすることができます。  

![右側のナビゲーション](media/sql-server-docs-navigation-guide/sql-docs-right-hand-navigation.gif)


## <a name="submit-docs-feedback"></a>ドキュメントのフィードバックを送信する

記事内に不適切な点を見つけた場合は、ページの下部までスクロールし、 **[Content feedback]\(コンテンツのフィードバック\)** を選択して、その記事の SQL コンテンツ チームにフィードバックを送信できます。

![[Git Issue content feedback]\(Git Issue コンテンツ フィードバック\)](media/sql-server-get-help/git-issues.png)

また、[https://aka.ms/sqldocsfeedback](https://aka.ms/sqldocsfeedback) で、一般的なドキュメントのフィードバックや提案を送信することもできます。 

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![SQL ドキュメントの編集](media/sql-server-docs-navigation-guide/edit-sql-docs.gif)

## <a name="next-steps"></a>次の手順

- [SQL Server の技術ドキュメント](index.yml)を使い始めます。
- SQL Server に関するフィードバックの送信方法または支援を受ける方法の詳細については、[支援を受ける方法](sql-server-get-help.md)のページを参照してください。 
- すべてのクイックスタートとチュートリアルにすばやくアクセスするには、[SQL Server 教育センター](../lp/sql-server/sql-education-center.md)をアクセスしてください。
