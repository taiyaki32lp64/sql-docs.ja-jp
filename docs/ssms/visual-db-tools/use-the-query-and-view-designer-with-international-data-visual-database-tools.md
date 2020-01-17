---
title: クエリおよびビュー デザイナーで各種言語データを使用する方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Visual Database Tools [SQL Server], international data
- queries [SQL Server], international data
- languages [SQL Server], Query and View Designer
- international considerations [SQL Server], Query and View Designer
- Criteria pane
- View Designer, international data
- Query Designer [SQL Server], international data
- localized information in Query and View Designer [SQL Server]
- global considerations [SQL Server], Query and View Designer
- SQL pane [Visual Database Tools]
- multiple language support [SQL Server], Query and View Designer
ms.assetid: 4b51c56f-f902-4e72-b919-e36127369b63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ff5eafd8a0a150b40c2383523e269691f0a83b08
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267409"
---
# <a name="use-the-query-and-view-designer-with-international-data-visual-database-tools"></a>クエリおよびビュー デザイナーで各種言語データを使用する方法 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) は、あらゆる言語のデータ、および Windows オペレーティング システムのすべてのバージョンのデータに対応しています。 次のガイドラインでは、各種言語のアプリケーションの相違点を示し、そのデータを管理する方法について説明します。  
  
## <a name="localized-information-in-the-criteria-and-sql-panes"></a>抽出条件ペインおよび SQL ペインのローカライズされた情報  
抽出条件ペインを使用してクエリを作成する場合は、使用しているコンピューターの Windows 地域設定に対応する形式で情報を入力できます。 たとえば、データを検索する場合は、使い慣れている形式でデータを [抽出条件] 列に入力できます。ただし、次に示す場合を除きます。  
  
-   長いデータ形式はサポートされていません。  
  
-   抽出条件ペインに通貨記号を入力することはできません。  
  
-   通貨記号は結果ペインには表示されません。  
  
    > [!NOTE]  
    > 結果ペインでは、使用するコンピューターの Windows 地域設定に対応する通貨記号を入力できますが、その記号は削除され、結果ペインにも表示されません。  
  
-   [地域のオプション] での設定に関係なく、単項のマイナスは常に左側に表示されます (例 : -1)。  
  
一方、SQL ペインのデータとキーワードでは、常に ANSI (U.S.) 形式を使用する必要があります。 たとえば、クエリおよびビュー デザイナーがクエリを作成する場合、SELECT や FROM などの SQL キーワードはすべて ANSI 形式で挿入されます。 SQL ペインのステートメントに要素を追加する場合は、ANSI 標準規格の形式を使用してください。  
  
抽出条件ペインに入力した地域固有の形式のデータは、クエリおよびビュー デザイナーによって、SQL ペインでは自動的に ANSI 形式に変換されます。 たとえば、[ロケール (国または地域)] に [ドイツ語 (ドイツ)] が設定されている場合は、抽出条件ペインでは「31.12.96」のような形式で日付を入力できます。 しかし SQL ペインでは、このデータは `{ ts '1996-12-31 00:00:00' }.` のように ANSI 形式の日付で表示されます。SQL ペインに直接データを入力する場合は、ANSI 形式で入力する必要があります。  
  
## <a name="sort-order"></a>[並べ替え順序]  
クエリにおけるデータの並べ替え順序は、データベースによって決まります。 Windows の [地域のオプション] ダイアログ ボックスで設定したオプションは、クエリの並べ替え順序には影響を与えません。 ただし、特定のクエリで、特定の順序で行を返すように要求することはできます。  
  
## <a name="using-double-byte-characters"></a>2 バイト文字の使用  
リテラルとして、またはテーブル名、ビュー名、エイリアスなどのデータベース オブジェクト名として、DBCS (2 バイト文字セット) 文字を入力できます。 DBCS 文字は、パラメーター名およびパラメーター マーカー文字にも使用できます。 ただし、関数名や SQL キーワードなどの SQL 言語要素に DBCS 文字を使用することはできません。  
  
## <a name="see-also"></a>参照  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
