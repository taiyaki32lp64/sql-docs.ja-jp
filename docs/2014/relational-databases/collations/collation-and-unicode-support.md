---
title: 照合順序と Unicode のサポート | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c63b7c0d1acad34bb273e4a49921d55818965e80
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688733"
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序により、並べ替え規則、大文字と小文字の区別、およびアクセントの区別のプロパティをデータで利用できるようになります。 `char` や `varchar` などの文字データ型に使用する照合順序は、そのデータ型で表すことのできるコード ページおよび対応する文字を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新しいインスタンスをインストールしているか、データベース バックアップを復元しているか、サーバーをクライアント データベースに接続しているかに関係なく、操作するデータのロケールの要件、並べ替え順序、および大文字と小文字の区別とアクセントの区別について理解することが重要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで使用可能な照合順序の一覧については、「 [sys」を参照してください。fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)」を参照してください。  
  
 サーバー、データベース、列、または式の照合順序を選択すると、データベースのさまざまな操作の結果に影響を与える特定の特性がデータに割り当てられます。 たとえば、ORDER BY を使用してクエリを構築する場合、結果セットの並べ替え順序は、データベースに適用される照合順序、またはクエリの式レベルで COLLATE 句に指定される照合順序に依存します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の照合順序サポートを最大限に活用するには、このトピックで定義されている用語と、それらがデータの特性にどのように関連しているかを理解する必要があります。  
  
  
###  <a name="Collation_Defn"></a> 照合順序  
 照合順序は、データセット内の各文字を表すビット パターンを指定します。 また、照合順序はデータの並べ替えおよび比較を行うための規則を決定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、単一のデータベース内で異なる照合順序を持つオブジェクトを格納できます。 非 Unicode 列の場合は、照合順序の設定によってデータのコード ページと表示可能な文字が指定されます。 非 Unicode 列の間を移動するデータは、移動元のコード ページから移動先のコード ページに変換する必要があります。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの結果は、それぞれ異なる照合順序が設定されている複数のデータベースのコンテキストでステートメントが実行される場合には、データベースごとに異なります。 可能であれば、組織全体で同じ照合順序を使用してください。 これにより、それぞれの文字または Unicode 表現について、照合順序を明示的に指定する必要がなくなります。 異なる照合順序とコード ページが設定されたオブジェクトを操作する場合は、照合の優先順位の規則を考慮してクエリを作成します。 詳細については、「 [照合順序の優先順位 (Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql)」を参照してください。  
  
 照合順序に関連するオプションは、大文字と小文字の区別、アクセントの区別、かなの区別、および文字幅の区別です。 これらのオプションは、照合順序の名前に付加することによって指定されます。 たとえば、 `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS` という照合順序では、大文字と小文字、アクセント、かな、および文字幅が区別されます。 次の表は、これらのオプションに関連付けられている動作を示しています。  
  
|オプション|[説明]|  
|------------|-----------------|  
|大文字と小文字を区別する (_CS)|大文字と小文字を区別します。 このオプションを選択すると、大文字より先に小文字が並べ替えられます。 このオプションを選択しないと、照合順序で大文字と小文字が区別されなくなります。 つまり、大文字と小文字は、並べ替えを行う際に同じものと見なされます。 大文字と小文字を区別しないことを明示的に選択するには、_CI と指定します。|  
|アクセントを区別する (_AS)|アクセントのある文字とアクセントのない文字を区別します。 たとえば、' a ' は '&#x1EA5;' と等しくありません。 このオプションを選択しないと、照合順序でアクセントが区別されなくなります。 つまり、アクセントのある文字とアクセントのない文字は、並べ替えを行う際に同じものと見なされます。 アクセントを区別しないことを明示的に選択するには、_AI と指定します。|  
|かなを区別する (_KS)|ひらがなとカタカナという日本語の 2 種類のかな文字を区別します。 このオプションを選択しないと、照合順序でかなが区別されません。 つまり、ひらがなとカタカナは、並べ替えを行う際に同じものと見なされます。 かなを区別しないように指定する唯一の方法は、このオプションを省略することです。|  
|文字幅を区別する (_WS)|全角文字と半角文字を区別します。 このオプションを選択しないと、同じ文字の全角表現と半角表現は、並べ替えを行う際に同じものと見なされます。 文字幅を区別しないように指定する唯一の方法は、このオプションを省略することです。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次の照合順序のセットをサポートしています。  
  
 Windows 照合順序  
 Windows 照合順序は、関連する Windows システム ロケールに基づく文字データを格納するための規則を定義します。 Windows 照合順序では、非 Unicode データの比較が、Unicode データと同じアルゴリズムを使用して実装されます。 基本の Windows 照合順序規則では、辞書順の並べ替えが適用される場合に使用される文字または言語と、非 Unicode 文字データの格納に使用されるコード ページを指定します。 Unicode 順の並べ替えと非 Unicode 順の並べ替えは、いずれも、特定のバージョンの Windows の文字列比較と互換性があります。 このしくみによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内のデータ型に一貫性が生まれ、開発者が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と同一の規則を使用してアプリケーションで文字列を並べ替えることが可能になります。 詳細については、「[Windows 照合順序名 &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)」を参照してください。  
  
 バイナリ照合順序  
 バイナリ照合順序では、ロケールおよびデータ型によって定義されるコーディングされた値の順序に基づいてデータを並べ替えます。 バイナリ照合順序では大文字と小文字が区別されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバイナリ照合順序は、使用するロケールおよび ANSI コード ページを定義します。 また、バイナリ並べ替え順を実施します。 これらは比較的単純なので、バイナリ照合順序はアプリケーションのパフォーマンスを向上させるために役立ちます。 非 Unicode データ型の場合は、ANSI コード ページで定義されているコード ポイントに基づいてデータが比較されます。 Unicode データ型の場合は、Unicode コード ポイントに基づいてデータが比較されます。 Unicode データ型のバイナリ照合順序では、データを並べ替える際にロケールが考慮されません。 たとえば、Unicode データに対して Latin_1_General_BIN と Japanese_BIN を使用した場合、並べ替え結果はどちらも同じになります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、古い `BIN` 照合順序と新しい `BIN2` 照合順序という 2 種類のバイナリ照合順序があります。 `BIN2` 照合順序では、すべての文字はコード ポイントに従って並べ替えられます。 `BIN` 照合順序では、最初の文字のみがコード ポイントに従って並べ替えられ、残りの文字はバイト値に従って並べ替えられます。 (Intel プラットフォームはリトル エンディアン アーキテクチャであるため、Unicode コード文字は常にバイト スワップして格納されます)。  
  
 SQL Server 照合順序  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序 (SQL_*) では、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と互換性のある並べ替え順が使用されます。 非 Unicode データについては、辞書順での並べ替え規則は Windows オペレーティング システムによって提供されるどの並べ替えルーチンとも互換性はありません。 ただし、Unicode データの並べ替えは、特定のバージョンの Windows 並べ替え規則と互換性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序では非 Unicode データと Unicode データで別々の比較規則を使用するため、基本となるデータ型によっては、同一データの比較で異なる結果が得られる場合があります。 詳細については、「[SQL Server 照合順序名 &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)」を参照してください。  
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の英語インスタンスをアップグレードするときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既存インスタンスとの互換性のために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]照合順序 (SQL_*) を指定することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの既定照合順序がセットアップ時に定義されるため、次のいずれかに該当する場合は、照合順序の設定を注意深く指定するようにしてください。  
> 
>  -   アプリケーション コードが以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の動作に依存している場合。  
> -   複数の言語に対応する文字データを格納する必要がある場合。  
  
 照合順序の設定は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの次のレベルでサポートされます。  
  
 サーバーレベルの照合順序  
 既定のサーバー照合順序は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時に設定され、システム データベースおよびすべてのユーザー データベースの既定の照合順序にもなります。 なお、Unicode 専用の照合順序はサーバーレベルの照合順序としてサポートされないため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時に選択することはできません。  
  
 サーバーに照合順序を指定した後は、照合順序を簡単には変更できません。変更するには、すべてのデータベース オブジェクトとデータをエクスポートし、`master` データベースを再構築してから、すべてのデータベース オブジェクトとデータをインポートする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの既定の照合順序を変更する代わりに、新しいデータベースまたはデータベース列の作成時に、目的の照合順序を指定することができます。  
  
 データベースレベルの照合順序  
 データベースを作成または修正する際には、CREATE DATABASE または ALTER DATABASE ステートメントの COLLATE 句を使用して、データベースの既定の照合順序を指定できます。 照合順序が指定されない場合、データベースにはサーバーの照合順序が割り当てられます。  
  
 サーバーの照合順序を変更すること以外に、システム データベースの照合順序を変更する方法はありません。  
  
 データベースの照合順序は、データベース内のすべてのメタデータで使用され、データベース内で使用されるすべての文字列型の列、一時オブジェクト、変数名、およびその他のすべての文字列の既定値になります。 ユーザー データベースの照合順序を変更する場合は、データベースのクエリが一時テーブルにアクセスするときに照合順序が競合する可能性があります。 一時テーブルは常に `tempdb` システム データベースに格納され、このデータベースではインスタンスの照合順序が使用されます。 ユーザー データベースと `tempdb` の文字データを比較するクエリは、文字データの評価で照合順序が競合すると、失敗します。 この問題は、クエリに COLLATE 句を指定することで解決できます。 詳細については、「[COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)」を参照してください。  
  
 列レベルの照合順序  
 テーブルを作成または変更するときに、COLLATE 句を使用して、文字列型の各列に対して照合順序を指定できます。 照合順序を指定しない場合、データベースの既定の照合順序が列に割り当てられます。  
  
 式レベルの照合順序  
 式レベルの照合順序は、ステートメントの実行時に設定され、結果セットが返される方法に影響を及ぼします。 これにより、ORDER BY の並べ替え結果をロケール固有のものにすることができます。 式レベルの照合順序を実装するには、次のような COLLATE 句を使用します。  
  
```  
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;  
```  
  
  
###  <a name="Locale_Defn"></a> ロケール  
 ロケールは、場所またはカルチャに関連付けられる一連の情報です。 これには、言語の名前や ID、言語の記述に使用される文字表記、文化的慣習などがあります。 照合順序は、1 つ以上のロケールに関連付けることができます。 詳細については、「[Microsoft によって割り当てられているロケール ID](https://msdn.microsoft.com/goglobal/bb964664.aspx)」を参照してください。  
  
  
###  <a name="Code_Page_Defn"></a> Code Page  
 コード ページは、特定の文字表記の順序付けられた文字のセットです。コード ページでは、数値インデックス (コード ポイント値) が各文字に関連付けられます。 Windows コード ページは、通常は *文字セット* または *charset*と呼ばれています。 コード ページは、各種の Windows システム ロケールで使用される文字セットおよびキーボード レイアウトをサポートするために使用されます。  
  
  
###  <a name="Sort_Order_Defn"></a> Sort Order  
 並べ替え順序は、データ値の並べ替え方法を指定します。 これは、データ比較の結果に影響を及ぼします。 データは、照合順序を使用して並べ替えられ、インデックスを使用して最適化することができます。  
  
  
##  <a name="Unicode_Defn"></a> Unicode のサポート  
 Unicode は、コード ポイントを文字にマップするための標準です。 Unicode は世界中のすべての言語のすべての文字を処理できるようにデザインされているので、異なる文字のセットを扱うために他のコード ページを必要とすることがありません。 複数の言語を反映する文字データを格納する場合は、非 Unicode データ型 (`nchar`、`nvarchar`、および `ntext`) ではなく、Unicode データ型 (`char`、`varchar`、および `text`) を常に使用してください。  
  
 非 Unicode データ型には、多くの制限が関連付けられています。 これは、Unicode に対応していないコンピューターではコード ページの使用が 1 つに制限されているためです。 Unicode コードを使用すると、必要なコード ページ変換が少なくなるので、パフォーマンスの向上が期待できます。 Unicode 照合順序は、サーバー レベルではサポートされないため、データベース、列、式の各レベルで個別に選択する必要があります。  
  
 クライアントが使用するコード ページは、オペレーティング システムの設定によって決まります。 Windows オペレーティング システムでクライアント コード ページを設定するには、コントロール パネルの **[地域と言語のオプション]** を使用します。  
  
 データをサーバーからクライアントに移動するとき、古いクライアント ドライバーでサーバー照合順序が認識されないことがあります。 これは、データを Unicode サーバーから非 Unicode クライアントに移動する場合に発生する可能性があります。 最善の対処方法は、クライアント オペレーティング システムをアップグレードして、基になるシステムの照合順序を更新することです。 クライアントにデータベース クライアント ソフトウェアがインストールされている場合は、データベース クライアント ソフトウェアにサービスの更新プログラムを適用する方法もあります。  
  
 また、サーバー上のデータに異なる照合順序を使用してみることもできます。 クライアントのコード ページにマップする照合順序を選択します。  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]で提供される UTF-16 照合順序を使用するには、Unicode 文字の並べ替えと検索の機能を向上させるために、補助文字の `_SC` 照合順序 (Windows 照合順序のみ) の 1 つを選択します。  
  
 Unicode または非 Unicode データ型の使用に関連する問題点を評価するには、使用環境におけるパフォーマンスの違いを測定するためのシナリオをテストする必要があります。 組織内のシステムで使用する照合順序を標準化し、可能であれば Unicode サーバーおよびクライアントを配置するようにしてください。  
  
 さまざまな状況で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は他のサーバーまたはクライアントとやり取りし、組織ではアプリケーションやサーバー インスタンス間で複数のデータ アクセス標準を使用する可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントは次の 2 つの主要タイプのいずれかになります。  
  
-   OLE DB および Open Database Connectivity (ODBC) Version 3.7 以降のバージョンを使用する**Unicode クライアント**  
  
-   DB ライブラリおよび ODBC Version 3.6 以前のバージョンを使用する**非 Unicode クライアント**  
  
 以下の表は、Unicode 型サーバーと非 Unicode 型サーバーの各種の組み合わせにおける多言語データの使用に関する情報を示しています。  
  
|Server|クライアント|利点または制限事項|  
|------------|------------|-----------------------------|  
|Unicode|Unicode|このシナリオでは、システム全体で Unicode データが使用されるため、最高のパフォーマンスが実現され、取得されるデータが破損から保護されます。 これは、ActiveX Data Objects (ADO)、OLE DB、および ODBC Version 3.7 以降のバージョンの場合に該当します。|  
|Unicode|非 Unicode|このシナリオで、特に新しいオペレーティング システムを実行しているサーバーと、古いバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または古いオペレーティング システムを実行しているクライアントが接続されている場合、データをクライアント コンピューターに移動するときに制約やエラーが生じることがあります。 サーバー上の Unicode データは、非 Unicode クライアント上の対応するコード ページにマップしてデータを変換しようと試みます。|  
|非 Unicode|Unicode|これは、多言語データの使用に理想的な構成とはいえません。 Unicode データを非 Unicode サーバーに書き込むことはできません。 サーバーのコード ページ内に存在しないサーバーにデータを送信すると、問題が発生する可能性があります。|  
|非 Unicode|非 Unicode|これは、多言語データに関して非常に制限的なシナリオです。 使用できるコード ページは 1 つだけです。|  
  
  
##  <a name="Supplementary_Characters"></a> 補助文字  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Unicode データの格納用に、`nchar`、`nvarchar` などのデータ型が用意されています。 これらのデータ型は、 *UTF-16*と呼ばれる形式でテキストをエンコードします。 Unicode コンソーシアムは、各文字に一意のコード ポイント (0x0000 から 0x10FFFF の範囲の値) を割り当てています。 最もよく使用される一連の文字にはメモリとディスク上で 16 ビット ワードに収まるコード ポイント値がありますが、コード ポイント値が 0xFFFF を超える文字は、連続した 2 つの 16 ビット ワードを必要とします。 これらの文字は *補助文字*と呼ばれ、2 つの連続する 16 ビット ワードは *サロゲート ペア*と呼ばれます。  
  
 補助文字を使用する場合は、以下の点に注意してください。  
  
-   補助文字は、90 以上の照合順序バージョンで、並べ替えと比較の操作に使用できます。  
  
-   すべての _100 レベルの照合順序で、補助文字の言語的な並べ替えがサポートされています。  
  
-   補助文字は、データベース オブジェクトの名前など、メタデータ内で使用することはできません。  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、新しい補助文字 (SC) の照合順序が、`nchar`、`nvarchar`、および `sql_variant` の各データ型で使用できます。 たとえば、 `Latin1_General_100_CI_AS_SC`や、日本語の照合順序を使用する場合は `Japanese_Bushu_Kakusu_100_CI_AS_SC`を使用できます。  
  
     SC フラグは、以下に適用できます。  
  
    -   バージョン 90 の Windows 照合順序  
  
    -   バージョン 100 の Windows 照合順序  
  
     SC フラグは、以下には適用できません。  
  
    -   バージョン 80 バージョンなしの Windows 照合順序  
  
    -   BIN または BIN2 バイナリ照合順序  
  
    -   SQL* 照合順序  
  
 次の表では、一部の文字列関数と文字列演算子で、補助文字が SC 照合順序ありで使用される場合と SC 照合順序なしで使用される場合の動作を比較しています。  
  
|文字列関数または演算子|SC の照合順序あり|SC の照合順序なし|  
|---------------------------------|--------------------------|-----------------------------|  
|[CHARINDEX](/sql/t-sql/functions/charindex-transact-sql)<br /><br /> [LEN](/sql/t-sql/functions/len-transact-sql)<br /><br /> [PATINDEX](/sql/t-sql/functions/patindex-transact-sql)|UTF-16 サロゲート ペアは、1 つのコード ポイントとしてカウントされます。|UTF-16 サロゲート ペアは、2 つのコード ポイントとしてカウントされます。|  
|[LEFT](/sql/t-sql/functions/left-transact-sql)<br /><br /> [REPLACE](/sql/t-sql/functions/replace-transact-sql)<br /><br /> [REVERSE](/sql/t-sql/functions/reverse-transact-sql)<br /><br /> [RIGHT](/sql/t-sql/functions/right-transact-sql)<br /><br /> [SUBSTRING](/sql/t-sql/functions/substring-transact-sql)<br /><br /> [STUFF](/sql/t-sql/functions/stuff-transact-sql)|これらの関数は、各サロゲート ペアを 1 つのコード ポイントとして処理し、期待どおりに動作します。|これらの関数では、サロゲート ペアが分割され、予期しない結果が生じることがあります。|  
|[NCHAR](/sql/t-sql/functions/nchar-transact-sql)|0 ～ 0x10FFFF の範囲の指定した Unicode コード ポイント値に対応する文字を返します。 指定された値が 0 ～ 0xFFFF の範囲内にある場合、1 つの文字だけが返されます。 値が大きい場合、対応するサロゲート ペアが返されます。|0 xFFFF よりも高い値の場合は、対応するサロゲートの代わりに NULL が返されます。|  
|[UNICODE](/sql/t-sql/functions/unicode-transact-sql)|0 から 0x10FFFF の範囲の UTF-16 コード ポイントが返されます。|0 から 0xFFFF の範囲の UCS-2 コード ポイントが返されます。|  
|[1 文字に一致するワイルドカード](/sql/t-sql/language-elements/wildcard-match-one-character-transact-sql)<br /><br /> [ワイルドカード - 一致しない文字列](/sql/t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql)|補助文字は、すべてのワイルドカード操作でサポートされています。|補助文字は、これらのワイルドカード操作でサポートされていません。 その他のワイルドカード演算子がサポートされます。|  
  
  
##  <a name="GB18030"></a> GB18030 のサポート  
 GB18030 は中華人民共和国が単独で中国語の文字のエンコードに使用している標準規格です。 GB18030 文字の長さは 1 バイト、2 バイト、4 バイトのいずれかです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、クライアント側アプリケーションからサーバーに GB18030 でエンコードした文字が入力されたときに文字を認識し、内部的には Unicode 文字に変換して格納することで GB18030 文字をサポートしています。 サーバーに格納された GB18030 文字は、それ以降の操作では Unicode 文字として処理されます。 任意の中国語の照合順序を使用できますが、最新の 100 バージョンの使用をお勧めします。 すべての _100 レベルの照合順序は、GB18030 文字の言語的な並べ替えをサポートしています。 データに補助文字 (サロゲート ペア) が含まれている場合は、検索や並べ替えの機能を向上させるために、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で利用可能な SC 照合順序を使用できます。  
  
  
##  <a name="Complex_script"></a> 複雑な文字表記のサポート  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、複雑な文字表記の入力、格納、変更、および表示をサポートできます。 複雑な文字表記には、次の種類があります。  
  
-   アラビア語テキストと英語テキストの組み合わせなど、右から左に記述されるテキストと左から右に記述されるテキストの両方の組み合わせを含む文字表記。  
  
-   アラビア語、インド諸語、タイ語の文字など、位置によって、または別の種類の文字と組み合わせた場合に、文字が変形する文字表記。  
  
-   タイ語など、単語間に区切りがないため、単語を識別するための内部辞書を必要とする言語。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を操作するデータベース アプリケーションは、複雑な文字表記をサポートするコントロールを使用する必要があります。 マネージド コードで作成される標準の Windows フォーム コントロールは、複雑な文字表記を使用できます。  
  
  
##  <a name="Related_Tasks"></a> 関連タスク  
  
|タスク|トピック|  
|----------|-----------|  
|SQL Server のインスタンスの照合順序を設定または変更する方法について説明します。|[サーバーの照合順序の設定または変更](set-or-change-the-server-collation.md)|  
|ユーザー データベースの照合順序を設定または変更する方法について説明します。|[データベースの照合順序の設定または変更](set-or-change-the-database-collation.md)|  
|データベース内の列の照合順序を設定または変更する方法について説明します。|[列の照合順序の設定または変更](set-or-change-the-column-collation.md)|  
|サーバー、データベース、または列のレベルでの照合順序の情報を取得する方法について説明します。|[照合順序情報の表示](view-collation-information.md)|  
|Transact-SQL ステートメントを、ある言語から別の言語に容易に移行したり、複数の言語を簡単にサポートしたりできるように記述する方法について説明します。|[国際化に対応した Transact-SQL ステートメントの記述](write-international-transact-sql-statements.md)|  
|エラー メッセージの言語と、日付、時刻、通貨データを使用および表示する際の設定を変更する方法について説明します。|[セッション言語の設定](set-a-session-language.md)|  
  
  
##  <a name="Related_Content"></a> 関連コンテンツ  
 [SQL Server ベスト プラクティス照合順序の変更](https://go.microsoft.com/fwlink/?LinkId=113891)  
  
 [SQL Server ベスト プラクティス Unicode への移行](https://go.microsoft.com/fwlink/?LinkId=113890)  
  
 [Unicode コンソーシアムの Web サイト](https://go.microsoft.com/fwlink/?LinkId=48619)  
  
## <a name="see-also"></a>参照  
 [Contained Database Collations](../databases/contained-database-collations.md)   
 [フルテキスト インデックス作成時の言語の選択](../search/choose-a-language-when-creating-a-full-text-index.md)   
 [sys.fn_helpcollations (Transact-SQL)](https://msdn.microsoft.com/library/ms187963(SQL.130).aspx)  
  
  
