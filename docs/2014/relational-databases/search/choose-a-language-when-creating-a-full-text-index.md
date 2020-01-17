---
title: フルテキスト インデックス作成時の言語の選択 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text indexes [SQL Server], languages
- international considerations [full-text search]
- stemmers [full-text search]
- global considerations [full-text search]
- full-text search [SQL Server], international considerations
- languages [SQL Server], full-text indexes
- word breakers [full-text search]
ms.assetid: 670a5181-ab80-436a-be96-d9498fbe2c09
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5f045933735d2a26b1e9007868f96680bef4fc47
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012732"
---
# <a name="choose-a-language-when-creating-a-full-text-index"></a>フルテキスト インデックス作成時の言語の選択
  フルテキスト インデックスを作成する際には、列レベルの言語をインデックス列に対して指定する必要があります。 指定した言語の [ワード ブレーカーとステマー](configure-and-manage-word-breakers-and-stemmers-for-search.md) が、列のフルテキスト クエリで使用されます。 フルテキスト インデックスの作成時に列の言語を選択する際には、注意点が 2 つあります。 これらの注意点は、テキストをトークン化する方法と、Full-Text Engine によるインデックス作成の方法にかかわるものです。  
  
> [!NOTE]  
>  列レベルの言語をフルテキスト インデックス列に対して指定するには、列の指定時に LANGUAGE *language_term* 句を使用します。 詳細については、「[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)」および「[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)」を参照してください。  
  
##  <a name="langsupp"></a> フルテキスト検索の言語サポート  
 ここでは、ワード ブレーカーとステミング機能の概要を示し、列レベルの言語の LCID がフルテキスト検索で使用されるしくみについて説明します。  
  
### <a name="introduction-to-word-breakers-and-stemmers"></a>ワード ブレーカーとステミング機能の概要  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンは、ワード ブレーカーとステミング機能、以前よりもはるかに優れているの完全な新しいファミリと[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。  
  
> [!NOTE]  
>  これらの新しい言語コンポーネントは、Microsoft Natural Language Group (MS NLG) によって実装およびサポートされています。  
  
 新しいワード ブレーカーには次の利点があります。  
  
-   堅牢性  
  
     負荷の高いクエリ環境における新しいワード ブレーカーの堅牢性が、テストによって明らかにされています。  
  
-   セキュリティ  
  
     新しいワード ブレーカーが既定で有効に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]言語コンポーネントのセキュリティが向上します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の全体的なセキュリティと堅牢性を強化するためには、ワード ブレーカーやフィルターなどの外部コンポーネントに署名することを強くお勧めします。 次のようにフルテキストを構成すると、これらのコンポーネントが署名されていることを確認できます。  
  
    ```  
    EXEC sp_fulltext_service 'verify_signature';  
    ```  
  
-   品質  
  
     ワード ブレーカーの設計が変更されました。新しいワード ブレーカーのセマンティクスの品質が以前よりも向上したことが、テストによって明らかにされています。 このため、再呼び出しの精度が向上します。  
  
-   カバレッジの言語の膨大な一覧については、ワード ブレーカーに含まれる[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ボックスの既定で有効にするとします。  
  
 対象の言語の一覧については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ワード ブレーカーとステミング機能が含まれていますを参照してください[sys.fulltext_languages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)します。  
  

  
### <a name="how-full-text-search-uses-the-name-of-the-column-level-language"></a>列レベルの言語の名前がフルテキスト検索で使用されるしくみ  
 フルテキスト インデックスの作成時には、有効な言語名を各列に対して指定する必要があります。 言語名が有効であっても [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) カタログ ビューによって返されない場合、同じ言語ファミリに使用可能な言語名があれば、最も近いものがフルテキスト検索に使用されます。 それ以外の場合は、代わりにニュートラル ワード ブレーカーがフルテキスト検索に使用されます。 このフォールバック動作は、再呼び出しの精度に影響する可能性があります。 したがって、フルテキスト インデックスの作成時には、有効かつ使用可能な言語名を各列に対して指定することを強くお勧めします。  
  
> [!NOTE]  
>  LCID は、フルテキスト インデックス作成で有効なすべてのデータ型 (`char` 型や `nchar` 型など) に適用されます。 `char`、`varchar`、`text` 型の列の並べ替え順を、LCID で識別された言語とは異なる言語に設定した場合でも、それらの列に対してフルテキスト インデックスを作成したりクエリを実行したりするときには LCID が使用されます。  
  

  
##  <a name="breaking"></a> 単語分割  
 インデックス作成の対象テキストを単語の境界でトークン化するのは、言語固有のワード ブレーカーです。 したがって、単語を区切る動作は言語によって異なります。 1 つの言語 (x) を使用して複数の言語 (x、y、および z) のインデックスを作成した場合、予期しない動作結果が生じることがあります。 たとえば、ダッシュ (-) やコンマ (,) などの単語区切り要素は、言語によって無視されたりされなかったりします。 また、まれに、ある単語の語幹が言語によって異なる場合に、予期しない語幹検索の動作が生じることがあります。 たとえば、英語では通常、単語の境界は空白またはなんらかの句読点になります。 ドイツ語などの他の言語では、複数の単語や文字を組み合わせることができます。 したがって、列レベルで言語を選択する場合は、その列の行に格納されると予想される言語を選択する必要があります。  
  
### <a name="western-languages"></a>西洋言語  
 西洋言語の場合、列に格納される言語がわからないときや複数の言語が格納されるときは、一般的な回避策として、列に格納される可能性がある言語のうち最も複雑な言語のワード ブレーカーを使用します。 たとえば、1 つの列に、英語、スペイン語、およびドイツ語の内容が格納される予定であるとします。 これら 3 つの西洋言語は単語の区切り方がよく似ていますが、ドイツ語の場合が最も複雑です。 したがって、この例では、ドイツ語のワード ブレーカーを使用することをお勧めします。そうすれば、英語とスペイン語のテキストも正しく処理できます。 一方、英語のワード ブレーカーを使用した場合は、複合語を持つドイツ語のテキストを完璧には処理できないことがあります。  
  
 言語ファミリ内の最も複雑な言語のワード ブレーカーを使用しても、ファミリ内のすべての言語で完璧なインデックスを作成できるとは限りません。 最も複雑なワード ブレーカーでも、別言語のテキストを正しく処理できないような場合があります。  
  

  
### <a name="non-western-languages"></a>西洋以外の言語  
 西洋以外の言語 (中国語、日本語、ヒンディー語など) では、言語の特性上、前に示した回避策が必ずしも機能しません。 西洋以外の言語の場合は、次のいずれかの回避策を検討してください。  
  
-   異なるファミリに属する複数の言語の場合  
  
     類似性のない複数の言語 (たとえばスペイン語と日本語) が 1 つの列に格納される可能性がある場合は、格納する列を言語ごとに分けることを検討してください。 このようにすると、各列で言語固有のワード ブレーカーを使用できます。 この回避策を選択した場合に、クエリ時にクエリ言語が判明していないときは、両方の列に対してクエリを実行し、適切な行やドキュメントを検索できるようにする必要があります。  
  
-   バイナリ コンテンツ (Microsoft Word 文書など) の場合  
  
     インデックス付きコンテンツが `binary` 型の場合、ワード ブレーカーへの送信前にテキスト コンテンツを処理するフルテキスト検索フィルターによって、バイナリ ファイル内に存在する特定の言語タグが使用されることがあります。 その場合、インデックスの作成時に、ドキュメントまたはドキュメント セクションの正しい LCID がフィルターによって生成されます。 次に、その LCID を持つ言語のワード ブレーカーが Full-Text Engine によって呼び出されます。 ただし、複数の言語のコンテンツにインデックスを作成した後は、コンテンツのインデックスが正しく作成されたかどうかを確認することをお勧めします。  
  
-   プレーン テキスト コンテンツの場合  
  
     コンテンツがプレーンテキストの場合は、`xml` データ型に変換して、各ドキュメントまたはドキュメント セクションに対応する言語を示す言語タグを追加できます。 ただし、そのためには、フルテキスト インデックスの作成前に言語を把握しておく必要があります。  
  

  
##  <a name="stemming"></a> ステミング  
 列レベルで言語を選択する際には、ステミングについても考慮します。 フルテキスト クエリでの*ステマー* は、特定の言語の単語に対し、語幹から派生した語形 (変化形) をすべて検索するプロセスです。 汎用のワード ブレーカーで複数の言語を処理する場合、列に対して指定された言語に対してのみステミング プロセスが機能します。列内のその他の言語に対しては、ステミング プロセスが機能しません。 たとえば、ドイツ語のステミング機能は、英語やスペイン語などに対して機能しません。 このため、クエリ時に選択した言語によっては、再呼び出しに影響する場合があります。  
  

  
##  <a name="type"></a> 列の型がフルテキスト検索に及ぼす影響  
 言語を選択する際のもう 1 つの注意点は、データの表記方法に関連するものです。 `varbinary(max)` 列に格納されていないデータについては、特別なフィルター処理は実行されません。 テキストはそのままの形で単語を分解するコンポーネント (ワード ブレーカー) に渡されます。  
  
 また、ワード ブレーカーは主に記述されたテキストを処理することを目的として設計されています。 したがって、HTML などのなんらかのマークアップがテキストに含まれている場合には、言語面での精度が高いインデックス作成と検索は期待できません。 メソッドがテキスト データを格納するだけですがである場合は、2 つの選択肢の優先`varbinary(max)` 列でフィルター処理することがありますので、ドキュメントの種類を指定したりします。 この方法を選択できない場合は、ニュートラル ワード ブレーカーの使用を検討してください。また、可能であれば、ノイズ ワードの一覧にマークアップ データ (HTML の「br」など) を追加します。  
  
> [!NOTE]  
>  ニュートラル言語を指定した場合、言語ベースのステミングは使用できません。  
  

  
##  <a name="nondef"></a> フルテキスト クエリにおける既定以外の列レベル言語の指定  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の既定のフルテキスト検索では、フルテキスト句内に含まれている各列に対して指定した言語を使用して、クエリ用語が解析されます。 この動作をオーバーライドするには、クエリ時に既定以外の言語を指定します。 言語がサポートされていて、そのリソースがインストールされていれば、 *CONTAINS* 、 [CONTAINSTABLE](/sql/t-sql/queries/contains-transact-sql)、 [FREETEXT](/sql/relational-databases/system-functions/containstable-transact-sql)、 [FREETEXTTABLE](/sql/t-sql/queries/freetext-transact-sql)クエリの LANGUAGE [language_term](/sql/relational-databases/system-functions/freetexttable-transact-sql) 句を使用して、クエリ用語の単語区切り、ステマー、類義語辞典、およびストップワードの処理に使用する言語を指定できます。  
  

  
## <a name="see-also"></a>関連項目  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [検索用フィルターの構成と管理](configure-and-manage-filters-for-search.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [検索用のワード ブレーカーとステミング機能の構成と管理](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
