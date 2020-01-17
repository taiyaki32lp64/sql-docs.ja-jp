---
title: 照合順序と Unicode のサポート | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
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
- UTF-8
- UTF-16
- UTF8
- UTF16
- UCS2
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: pmasl
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 862147cfb7620999bf3e56a90fae0e90fbb1be45
ms.sourcegitcommit: 0d34b654f0b3031041959e87f5b4d4f0a1af6a29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74901940"
---
# <a name="collation-and-unicode-support"></a>照合順序と Unicode のサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序により、並べ替え規則、大文字と小文字の区別、およびアクセントの区別のプロパティをデータで利用できるようになります。 **char** や **varchar** などの文字データ型に使用する照合順序は、そのデータ型で表すことのできるコード ページおよび対応する文字を指定します。 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンスをインストールしているか、データベース バックアップを復元しているか、サーバーをクライアント データベースに接続しているかに関係なく、操作するデータのロケールの要件、並べ替え順序、および大文字と小文字の区別とアクセントの区別について理解することが重要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで使用可能な照合順序の一覧については、「[sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)」を参照してください。    
    
サーバー、データベース、列、または式の照合順序を選択すると、特定の特性がデータに割り当てられます。 これらの特性は、データベースのさまざまな操作の結果に影響を与えます。 たとえば、`ORDER BY` を使用してクエリを構築する場合、結果セットの並べ替え順序は、データベースに適用される照合順序、またはクエリの式レベルで `COLLATE` 句に指定される照合順序に依存します。    
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序サポートを最大限に利用するには、このトピックで定義されている用語と、それらがデータの特性にどのように関連しているかを理解する必要があります。    
    
##  <a name="Terms"></a> 照合順序の用語    
    
-   [Collation](#Collation_Defn) 
    - [照合順序セット](#Collation_sets)
    - [照合順序レベル](#Collation_levels)
-   [ロケール](#Locale_Defn)    
-   [コード ページ](#Code_Page_Defn)    
-   [並べ替え順序](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> 照合順序    
照合順序では、データセット内の各文字を表すビット パターンが指定されます。 また、照合順序はデータの並べ替えおよび比較を行うための規則を決定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、単一のデータベース内で異なる照合順序を持つオブジェクトを格納できます。 非 Unicode 列の場合は、照合順序の設定によってデータのコード ページと表示可能な文字が指定されます。 非 Unicode 列の間でデータを移動する場合は、移動元のコード ページから移動先のコード ページに変換する必要があります。    
    
[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの結果は、それぞれ異なる照合順序が設定されている複数のデータベースのコンテキストでステートメントが実行される場合には、データベースごとに異なります。 可能であれば、組織全体で同じ照合順序を使用します。 これにより、すべての文字または Unicode 表現で照合順序を指定する必要がなくなります。 異なる照合順序とコード ページが設定されたオブジェクトを操作する場合は、照合の優先順位の規則を考慮してクエリを作成します。 詳細については、「 [照合順序の優先順位 (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)」を参照してください。    
    
照合順序に関連するオプションは、大文字と小文字の区別、アクセントの区別、かなの区別、および文字幅の区別、バリエーションの選択の区別です。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、[UTF-8](https://www.wikipedia.org/wiki/UTF-8) エンコードのための追加のオプションが導入されています。 

これらのオプションは、照合順序の名前に付加することによって指定できます。 たとえば、**Japanese_Bushu_Kakusu_100_CS_AS_KS_WS_UTF8** という照合順序では、大文字と小文字、アクセント、かな、文字幅、UTF-8 エンコードが区別されます。 また、**Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS** という照合順序では、大文字小文字とアクセントが区別されず、かな、文字幅、異体字セレクターが区別され、非 Unicode エンコードが使用されます。 

次の表では、これらのさまざまなオプションに関連付けられている動作を説明します。    
    
|オプション|[説明]|    
|------------|-----------------|    
|大文字と小文字を区別する (\_CS)|大文字と小文字を区別します。 このオプションを選択すると、大文字より先に小文字が並べ替えられます。 このオプションを選択しないと、照合順序で大文字と小文字が区別されません。 つまり、大文字と小文字は、並べ替えを行う際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって同じものと見なされます。 大文字と小文字を区別しないことを明示的に選択するには、\_CI と指定します。|   
|アクセントを区別する (\_AS)|アクセントのある文字とアクセントのない文字を区別します。 たとえば、"a" と "ấ" は等しくありません。 このオプションを選択しないと、照合順序でアクセントが区別されません。 つまり、アクセントのある文字とアクセントのない文字は、並べ替えを行う際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって同じものと見なされます。 アクセントを区別しないことを明示的に選択するには、\_AI と指定します。|    
|かなを区別する (\_KS)|次の 2 種類の日本語かな文字を区別します。ひらがなとカタカナ。 このオプションを選択しないと、照合順序でかなが区別されません。 つまり、ひらがなとカタカナは、並べ替えを行う際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって同じものと見なされます。 かなを区別しないように指定する唯一の方法は、このオプションを省略することです。|   
|文字幅を区別する (\_WS)|全角文字と半角文字を区別します。 このオプションを選択しないと、同じ文字の全角表現と半角表現は、並べ替えを行うときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって同じものと見なされます。 文字幅を区別しないように指定する唯一の方法は、このオプションを省略することです。|  
|異体字の選択を区別する (\_VSS)|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] で導入された日本語の照合順序 **Japanese_Bushu_Kakusu_140** と **Japanese_XJIS_140** で、多様な表意文字のバリエーションの選択を区別します。 バリエーションのシーケンスは、基本文字と追加のバリエーションの選択で構成されます。 この \_VSS オプションを選択しない場合、照合順序で異体字の選択が区別されず、比較において異体字の選択が考慮されることはありません。 つまり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、並べ替えが同じになるように、バリエーションの選択が異なる同じ基本文字に基づいて構築された文字が考慮されています。 詳細については、「[Unicode 表意文字のバリエーション データベース](https://www.unicode.org/reports/tr37/)」を参照してください。<br/><br/> 異体字セレクターを区別する (\_VSS) 照合順序は、全文検索インデックスではサポートされていません。 フルテキスト検索インデックスでは、アクセントを区別する (\_AS)、かなを区別する (\_KS)、文字幅を区別する (\_WS) オプションのみがサポートされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML と CLR のエンジンでは、(\_VSS) 異体字セレクターはサポートされていません。|      
|バイナリ (\_BIN) <sup>1</sup>|各文字に定義されているビット パターンに基づいて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルのデータが並べ替えられ、比較されます。 バイナリ並べ替え順では、大文字と小文字が区別され、アクセントが区別されます。 また、バイナリは最速の並べ替え順です。 詳細については、この記事の「[バイナリ照合順序](#Binary-collations)」セクションを参照してください。|      
|バイナリコード ポイント (\_BIN2) <sup>1</sup> | Unicode データの Unicode コード ポイントに基づいて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル内のデータが並べ替えられ、比較されます。 非 Unicode データの場合、バイナリ コード ポイントではバイナリ並べ替えと同一の比較が使用されます。<br/><br/> バイナリ コード ポイント並べ替え順を使用すると、並べ替えられた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データを比較するアプリケーションでデータを再度並べ替える必要がないという利点があります。 このため、バイナリ コード ポイント並べ替え順を使用すると、アプリケーション開発が簡略化され、パフォーマンスを向上させることができます。 詳細については、この記事の「[バイナリ照合順序](#Binary-collations)」セクションを参照してください。|
|UTF-8 (\_UTF8)|UTF-8 でエンコードされたデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に格納できるようにします。 このオプションを選択しなかった場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、適用可能なデータ型に対して既定の非 Unicode エンコード形式が使用されます。 詳細については、この記事の「[UTF-8 サポート](#utf8)」セクションを参照してください。| 

<sup>1</sup> バイナリまたはバイナリ コード ポイントが選択されている場合、大文字と小文字を区別する (\_CS)、アクセントを区別する (\_AS)、かなを区別する (\_KS)、文字幅を区別する (\_WS) オプションは使用できません。      

#### <a name="examples-of-collation-options"></a>照合順序オプションの例
各照合順序は、大文字小文字、アクセント、文字幅、かなの区別を定義する一連のサフィックスとして組み合わせられます。 次の例で、サフィックスのさまざまな組み合わせに対応する並べ替え順の動作を説明します。

|Windows 照合順序サフィックス|並べ替え順の説明|
|------------|-----------------| 
|\_BIN<sup>1</sup>|バイナリ並べ替え|
|\_BIN2<sup>1、2</sup>|バイナリコード ポイント並べ替え順|
|\_CI_AI<sup>2</sup>|大文字小文字を区別しない、アクセントを区別しない、かなを区別しない、文字幅を区別しない|
|\_CI_AI_KS<sup>2</sup>|大文字小文字を区別しない、アクセントを区別しない、かなを区別する、文字幅を区別しない|
|\_CI_AI_KS_WS<sup>2</sup>|大文字小文字を区別しない、アクセントを区別しない、かなを区別する、文字幅を区別する|
|\_CI_AI_WS<sup>2</sup>|大文字小文字を区別しない、アクセントを区別しない、かなを区別しない、文字幅を区別する|
|\_CI_AS<sup>2</sup>|大文字小文字を区別しない、アクセントを区別する、かなを区別しない、文字幅を区別しない|
|\_CI_AS_KS<sup>2</sup>|大文字小文字を区別しない、アクセントを区別する、かなを区別する、文字幅を区別しない|
|\_CI_AS_KS_WS<sup>2</sup>|大文字小文字を区別しない、アクセントを区別する、かなを区別する、文字幅を区別する|
|\_CI_AS_WS<sup>2</sup>|大文字小文字を区別しない、アクセントを区別する、かなを区別しない、文字幅を区別する|
|\_CS_AI<sup>2</sup>|大文字小文字を区別する、アクセントを区別しない、かなを区別しない、文字幅を区別しない|
|\_CS_AI_KS<sup>2</sup>|大文字小文字を区別する、アクセントを区別しない、かなを区別する、文字幅を区別しない|
|\_CS_AI_KS_WS<sup>2</sup>|大文字小文字を区別する、アクセントを区別しない、かなを区別する、文字幅を区別する|
|\_CS_AI_WS<sup>2</sup>|大文字小文字を区別する、アクセントを区別しない、かなを区別しない、文字幅を区別する|
|\_CS_AS<sup>2</sup>|大文字小文字を区別する、アクセントを区別する、かなを区別しない、文字幅を区別しない|
|\_CS_AS_KS<sup>2</sup>|大文字小文字を区別する、アクセントを区別する、かなを区別する、文字幅を区別しない|
|\_CS_AS_KS_WS<sup>2</sup>|大文字小文字を区別する、アクセントを区別する、かなを区別する、文字幅を区別する|
|\_CS_AS_WS<sup>2</sup>|大文字小文字を区別する、アクセントを区別する、かなを区別しない、文字幅を区別する|

<sup>1</sup> バイナリまたはバイナリ コード ポイントが選択されている場合、大文字と小文字を区別する (\_CS)、アクセントを区別する (\_AS)、かなを区別する (\_KS)、文字幅を区別する (\_WS) オプションは使用できません。    

<sup>2</sup> UTF-8 オプション (\_UTF8) を追加することで、UTF-8 を使用して Unicode データをエンコードできます。 詳細については、この記事の「[UTF-8 サポート](#utf8)」セクションを参照してください。 

### <a name="Collation_sets"></a> 照合順序セット

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次の照合順序のセットをサポートしています。    

-  [Windows 照合順序](#Windows-collations)
-  [バイナリ照合順序](#Binary-collations)
-  [SQL Server 照合順序](#SQL-collations)
    
#### <a name="Windows-collations"></a> Windows 照合順序    
Windows 照合順序では、関連する Windows システム ロケールに基づく文字データを格納するための規則が定義されています。 Windows 照合順序では、非 Unicode データの比較を、Unicode データと同じアルゴリズムを使用して実装できます。 基本の Windows 照合順序規則では、辞書順の並べ替えが適用される場合に使用されるアルファベットまたは言語が指定されています。 また、規則では非 Unicode 文字データの格納に使用されるコード ページも指定されています。 Unicode 順の並べ替えと非 Unicode 順の並べ替えは、いずれも、特定のバージョンの Windows の文字列比較と互換性があります。 このしくみによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内のデータ型に一貫性が生まれ、開発者が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と同一の規則を使用してアプリケーションで文字列を並べ替えることが可能になります。 詳細については、「[Windows 照合順序名 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)」を参照してください。    
    
#### <a name="Binary-collations"></a> バイナリ照合順序    
バイナリ照合順序では、ロケールおよびデータ型によって定義されるコーディングされた値の順序に基づいてデータを並べ替えます。 大文字と小文字が区別されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバイナリ照合順序では、使用されるロケールおよび ANSI コード ページが定義されています。 また、バイナリ並べ替え順を実施します。 これらは比較的単純なので、バイナリ照合順序はアプリケーションのパフォーマンスを向上させるために役立ちます。 非 Unicode データ型の場合は、ANSI コード ページで定義されているコード ポイントに基づいてデータが比較されます。 Unicode データ型の場合は、Unicode コード ポイントに基づいてデータが比較されます。 Unicode データ型のバイナリ照合順序では、データを並べ替える際にロケールが考慮されません。 たとえば、Unicode データに対して **Latin_1_General_BIN** と **Japanese_BIN** を使用した場合、並べ替え結果はどちらも同じになります。 詳細については、「[Windows 照合順序名 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)」を参照してください。   
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、次の 2 種類のバイナリ照合順序があります。

-  以前の **BIN** 照合順序では、Unicode データに対して不完全なコード ポイント間比較が行われていました。 以前のこのようなバイナリ照合順序では、最初の文字が WCHAR として比較された後、続いてバイト単位の比較が行われていました。 BIN 照合順序では、最初の文字のみがコード ポイントに従って並べ替えられ、残りの文字はバイト値に従って並べ替えられます。

-  新しい **BIN2** 照合順序では、純粋なコード ポイント比較が実装されます。 BIN2 照合順序では、すべての文字がコード ポイントに従って並べ替えられます。 Intel プラットフォームはリトル エンディアン アーキテクチャであるため、Unicode コード文字は常にバイト スワップして格納されます。     
    
#### <a name="SQL-collations"></a> SQL Server 照合順序    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序 (SQL_\*) では、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と互換性のある並べ替え順が使用されます。 非 Unicode データについては、辞書順での並べ替え規則は Windows オペレーティング システムによって提供されるどの並べ替えルーチンとも互換性はありません。 ただし、Unicode データの並べ替えは、特定のバージョンの Windows 並べ替え規則と互換性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序では非 Unicode データと Unicode データで別々の比較規則を使用するため、基本となるデータ型によっては、同一データの比較で異なる結果が得られる場合があります。 詳細については、「[SQL Server 照合順序名 (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)」を参照してください。 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中、既定のインストール照合順序設定はオペレーティング システム (OS) ロケールによって決定されます。 サーバーレベルの照合順序は、セットアップ中に変更するか、インストール前に OS ロケールを変更することで変更できます。 下位互換性のため、既定の照合順序は、特定のロケール別に関連付けられている中で最も古いバージョンに設定されます。 そのため、これが常に推奨される照合順序になるとは限りません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能を活用するには、Windows 照合順序を使用するように既定のインストール設定を変更します。 たとえば、OS のロケールが "英語 (米国)" (コード ページ 1252) の場合、セットアップ中、既定の照合順序は **SQL_Latin1_General_CP1_CI_AS** になります。これは Windows 照合順序でそれに最も近い **Latin1_General_100_CI_AS_SC** に変更できます。
    
> [!NOTE]    
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の英語インスタンスをアップグレードするときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既存インスタンスとの互換性のために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序 (SQL_\*) を指定することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの既定照合順序がセットアップ時に定義されるため、次の条件に該当する場合は、照合順序の設定を注意深く指定するようにしてください。    
>     
> -   アプリケーション コードが以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の動作に依存している場合。    
> -   複数の言語に対応する文字データを格納する必要がある場合。    
    
### <a name="Collation_levels"></a> 照合順序レベル
照合順序の設定は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの次のレベルでサポートされます。    

-  [サーバーレベルの照合順序](#Server-level-collations)
-  [データベースレベルの照合順序](#Database-level-collations)
-  [列レベルの照合順序](#Column-level-collations)
-  [式レベルの照合順序](#Expression-level-collations)

#### <a name="Server-level-collations"></a> サーバーレベルの照合順序   
既定のサーバー照合順序は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時に決定され、システム データベースとすべてのユーザー データベースの既定の照合順序になります。 

次の表は、オペレーティング システム (OS) ロケールによって決定される既定の照合順序指定をまとめたものです。Windows と SQL 言語コード識別子 (LCID) が含まれています。

|Windows ロケール|Windows LCID|SQL LCID|既定の照合順序|
|---------------|---------|---------|---------------|
|アフリカーンス語 (南アフリカ)|0x0436|0x0409|Latin1_General_CI_AS|
|アルバニア語 (アルバニア)|0x041c|0x041c|Albanian_CI_AS|
|アルザス語 (フランス)|0x0484|0x0409|Latin1_General_CI_AS|
|アムハラ語 (エチオピア)|0x045e|0x0409|Latin1_General_CI_AS|
|アラビア語 (アルジェリア)|0x1401|0x0401|Arabic_CI_AS|
|アラビア語 (バーレーン)|0x3c01|0x0401|Arabic_CI_AS|
|アラビア語 (エジプト)|0x0c01|0x0401|Arabic_CI_AS|
|アラビア語 (イラク)|0x0801|0x0401|Arabic_CI_AS|
|アラビア語 (ヨルダン)|0x2c01|0x0401|Arabic_CI_AS|
|アラビア語 (クウェート)|0x3401|0x0401|Arabic_CI_AS|
|アラビア語 (レバノン)|0x3001|0x0401|Arabic_CI_AS|
|アラビア語 (リビア)|0x1001|0x0401|Arabic_CI_AS|
|アラビア語 (モロッコ)|0x1801|0x0401|Arabic_CI_AS|
|アラビア語 (オマーン)|0x2001|0x0401|Arabic_CI_AS|
|アラビア語 (カタール)|0x4001|0x0401|Arabic_CI_AS|
|アラビア語 (サウジアラビア)|0x0401|0x0401|Arabic_CI_AS|
|アラビア語 (シリア)|0x2801|0x0401|Arabic_CI_AS|
|アラビア語 (チュニジア)|0x1c01|0x0401|Arabic_CI_AS|
|アラビア語 (U.A.E.)|0x3801|0x0401|Arabic_CI_AS|
|アラビア語 (イエメン)|0x2401|0x0401|Arabic_CI_AS|
|アルメニア語 (アルメニア)|0x042b|0x0419|Latin1_General_CI_AS|
|アッサム語 (インド)|0x044d|0x044d|サーバー レベルでは利用できません|
|アゼルバイジャン語 (アゼルバイジャン、キリル文字)|0x082c|0x082c|非推奨。サーバー レベルでは利用できません|
|アゼルバイジャン語 (アゼルバイジャン、ラテン文字)|0x042c|0x042c|非推奨。サーバー レベルでは利用できません|
|バシキール語 (ロシア)|0x046d|0x046d|Latin1_General_CI_AI|
|バスク語 (バスク)|0x042d|0x0409|Latin1_General_CI_AS|
|ベラルーシ語 (ベラルーシ)|0x0423|0x0419|Cyrillic_General_CI_AS|
|ベンガル語 (バングラデシュ)|0x0845|0x0445|サーバー レベルでは利用できません|
|ベンガル語 (インド)|0x0445|0x0439|サーバー レベルでは利用できません|
|ボスニア語 (ボスニア・ヘルツェゴビナ、キリル文字)|0x201a|0x201a|Latin1_General_CI_AI|
|ボスニア語 (ボスニア・ヘルツェゴビナ、ラテン文字)|0x141a|0x141a|Latin1_General_CI_AI|
|ブルトン語 (フランス)|0x047e|0x047e|Latin1_General_CI_AI|
|ブルガリア語 (ブルガリア)|0x0402|0x0419|Cyrillic_General_CI_AS|
|カタルニア語 (カタルニア)|0x0403|0x0409|Latin1_General_CI_AS|
|中国語 (中華人民共和国香港特別行政区)|0x0c04|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|中国語 (中華人民共和国マカオ特別行政区)|0x1404|0x1404|Latin1_General_CI_AI|
|中国語 (マカオ)|0x21404|0x21404|Latin1_General_CI_AI|
|中国語 (中華人民共和国)|0x0804|0x0804|Chinese_PRC_CI_AS|
|中国語 (中華人民共和国)|0x20804|0x20804|Chinese_PRC_Stroke_CI_AS|
|中国語 (シンガポール)|0x1004|0x0804|Chinese_PRC_CI_AS|
|中国語 (シンガポール)|0x21004|0x20804|Chinese_PRC_Stroke_CI_AS|
|中国語 (台湾)|0x30404|0x30404|Chinese_Taiwan_Bopomofo_CI_AS|
|中国語 (台湾)|0x0404|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|コルシカ語 (フランス)|0x0483|0x0483|Latin1_General_CI_AI|
|クロアチア語 (ボスニア・ヘルツェゴビナ、ラテン文字)|0x101a|0x041a|Croatian_CI_AS|
|クロアチア語 (クロアチア)|0x041a|0x041a|Croatian_CI_AS|
|チェコ語 (チェコ共和国)|0x0405|0x0405|Czech_CI_AS|
|デンマーク語 (デンマーク)|0x0406|0x0406|Danish_Norwegian_CI_AS|
|ダリー語 (アフガニスタン)|0x048c|0x048c|Latin1_General_CI_AI|
|ディベヒ語 (モルディブ)|0x0465|0x0465|サーバー レベルでは利用できません|
|オランダ語 (ベルギー)|0x0813|0x0409|Latin1_General_CI_AS|
|オランダ語 (オランダ)|0x0413|0x0409|Latin1_General_CI_AS|
|英語 (オーストラリア)|0x0c09|0x0409|Latin1_General_CI_AS|
|英語 (ベリーズ)|0x2809|0x0409|Latin1_General_CI_AS|
|英語 (カナダ)|0x1009|0x0409|Latin1_General_CI_AS|
|英語 (カリブ)|0x2409|0x0409|Latin1_General_CI_AS|
|英語 (インド)|0x4009|0x0409|Latin1_General_CI_AS|
|英語 (アイルランド)|0x1809|0x0409|Latin1_General_CI_AS|
|英語 (ジャマイカ)|0x2009|0x0409|Latin1_General_CI_AS|
|英語 (マレーシア)|0x4409|0x0409|Latin1_General_CI_AS|
|英語 (ニュージーランド)|0x1409|0x0409|Latin1_General_CI_AS|
|英語 (フィリピン)|0x3409|0x0409|Latin1_General_CI_AS|
|英語 (シンガポール)|0x4809|0x0409|Latin1_General_CI_AS|
|英語 (南アフリカ)|0x1c09|0x0409|Latin1_General_CI_AS|
|英語 (トリニダード・トバゴ)|0x2c09|0x0409|Latin1_General_CI_AS|
|ウェールズ語 (イギリス)|0x0809|0x0409|Latin1_General_CI_AS|
|英語 (米国)|0x0409|0x0409|SQL_Latin1_General_CP1_CI_AS|
|英語 (ジンバブエ)|0x3009|0x0409|Latin1_General_CI_AS|
|エストニア語 (エストニア)|0x0425|0x0425|Estonian_CI_AS|
|フェロー語 (フェロー諸島)|0x0438|0x0409|Latin1_General_CI_AS|
|フィリピノ語 (フィリピン)|0x0464|0x0409|Latin1_General_CI_AS|
|フィンランド語 (フィンランド)|0x040b|0x040b|Finnish_Swedish_CI_AS|
|フランス語 (ベルギー)|0x080c|0x040c|French_CI_AS|
|フランス語 (カナダ)|0x0c0c|0x040c|French_CI_AS|
|フランス語 (フランス)|0x040c|0x040c|French_CI_AS|
|フランス語 (ルクセンブルク)|0x140c|0x040c|French_CI_AS|
|フランス語 (モナコ)|0x180c|0x040c|French_CI_AS|
|フランス語 (スイス)|0x100c|0x040c|French_CI_AS|
|フリジア語 (オランダ)|0x0462|0x0462|Latin1_General_CI_AI|
|ガリシア語 (スペイン)|0x0456|0x0409|Latin1_General_CI_AS|
|グルジア語 (グルジア)|0x10437|0x10437|Georgian_Modern_Sort_CI_AS|
|グルジア語 (グルジア)|0x0437|0x0419|Latin1_General_CI_AS|
|ドイツ語 - 電話帳ソート (DIN)|0x10407|0x10407|German_PhoneBook_CI_AS|
|ドイツ語 (オーストリア)|0x0c07|0x0409|Latin1_General_CI_AS|
|ドイツ語 (ドイツ)|0x0407|0x0409|Latin1_General_CI_AS|
|ドイツ語 (リヒテンシュタイン)|0x1407|0x0409|Latin1_General_CI_AS|
|ドイツ語 (ルクセンブルク)|0x1007|0x0409|Latin1_General_CI_AS|
|ドイツ語 (スイス)|0x0807|0x0409|Latin1_General_CI_AS|
|ギリシャ語 (ギリシャ)|0x0408|0x0408|Greek_CI_AS|
|グリーンランド語 (グリーンランド)|0x046f|0x0406|Danish_Norwegian_CI_AS|
|グジャラート語 (インド)|0x0447|0x0439|サーバー レベルでは利用できません|
|ハウサ語 (ナイジェリア、ラテン文字)|0x0468|0x0409|Latin1_General_CI_AS|
|ヘブライ語 (イスラエル)|0x040d|0x040d|Hebrew_CI_AS|
|ヒンディー語 (インド)|0x0439|0x0439|サーバー レベルでは利用できません|
|ハンガリー語 (ハンガリー)|0x040e|0x040e|Hungarian_CI_AS|
|ハンガリー語 (技術的な並べ替え)|0x1040e|0x1040e|Hungarian_Technical_CI_AS|
|アイスランド語 (アイスランド)|0x040f|0x040f|Icelandic_CI_AS|
|イボ語 (ナイジェリア)|0x0470|0x0409|Latin1_General_CI_AS|
|インドネシア語 (インドネシア)|0x0421|0x0409|Latin1_General_CI_AS|
|イヌクティトット語 (カナダ、ラテン文字)|0x085d|0x0409|Latin1_General_CI_AS|
|イヌクティトット語 (音節文字) カナダ|0x045d|0x045d|Latin1_General_CI_AI|
|アイルランド語 (アイルランド)|0x083c|0x0409|Latin1_General_CI_AS|
|イタリア語 (イタリア)|0x0410|0x0409|Latin1_General_CI_AS|
|イタリア語 (スイス)|0x0810|0x0409|Latin1_General_CI_AS|
|日本語 (日本 XJIS)|0x0411|0x0411|Japanese_CI_AS|
|日本語 (日本)|0x040411|0x40411|Latin1_General_CI_AI|
|カンナダ語 (インド)|0x044b|0x0439|サーバー レベルでは利用できません|
|カザフ語 (カザフスタン)|0x043f|0x043f|Kazakh_90_CI_AS|
|クメール語 (カンボジア)|0x0453|0x0453|サーバー レベルでは利用できません|
|キチェ語 (グアテマラ)|0x0486|0x0c0a|Modern_Spanish_CI_AS|
|キニヤルワンダ語 (ルワンダ)|0x0487|0x0409|Latin1_General_CI_AS|
|コーンクニー語 (インド)|0x0457|0x0439|サーバー レベルでは利用できません|
|韓国語 (韓国語辞書並べ替え)|0x0412|0x0412|Korean_Wansung_CI_AS|
|キルギス語 (キルギスタン共和国)|0x0440|0x0419|Cyrillic_General_CI_AS|
|ラオス語 (ラオス人民民主共和国)|0x0454|0x0454|サーバー レベルでは利用できません|
|ラトビア語 (ラトビア)|0x0426|0x0426|Latvian_CI_AS|
|リトアニア語 (リトアニア)|0x0427|0x0427|Lithuanian_CI_AS|
|下ソルブ語 (ドイツ)|0x082e|0x0409|Latin1_General_CI_AS|
|ルクセンブルク語 (ルクセンブルク)|0x046e|0x0409|Latin1_General_CI_AS|
|マケドニア語 (マケドニア、FYROM)|0x042f|0x042f|Macedonian_FYROM_90_CI_AS|
|マレー語 (ブルネイ・ダルサラーム国)|0x083e|0x0409|Latin1_General_CI_AS|
|マレー語 (マレーシア)|0x043e|0x0409|Latin1_General_CI_AS|
|マラヤーラム語 (インド)|0x044c|0x0439|サーバー レベルでは利用できません|
|マルタ語 (マルタ)|0x043a|0x043a|Latin1_General_CI_AI|
|マオリ語 (ニュージーランド)|0x0481|0x0481|Latin1_General_CI_AI|
|マプ語 (チリ)|0x047a|0x047a|Latin1_General_CI_AI|
|マラーティー語 (インド)|0x044e|0x0439|サーバー レベルでは利用できません|
|モホーク語 (カナダ)|0x047c|0x047c|Latin1_General_CI_AI|
|モンゴル語 (モンゴル)|0x0450|0x0419|Cyrillic_General_CI_AS|
|モンゴル語 (PRC)|0x0850|0x0419|Cyrillic_General_CI_AS|
|ネパール語 (ネパール)|0x0461|0x0461|サーバー レベルでは利用できません|
|ノルウェー語 (ブークモール、ノルウェー)|0x0414|0x0414|Latin1_General_CI_AI|
|ノルウェー語 (ニーノシュク、ノルウェー)|0x0814|0x0414|Latin1_General_CI_AI|
|オクシタン語 (フランス)|0x0482|0x040c|French_CI_AS|
|オリヤー語 (インド)|0x0448|0x0439|サーバー レベルでは利用できません|
|パシュトゥー語 (アフガニスタン)|0x0463|0x0463|サーバー レベルでは利用できません|
|ペルシア語 (イラン)|0x0429|0x0429|Latin1_General_CI_AI|
|ポーランド語 (ポーランド)|0x0415|0x0415|Polish_CI_AS|
|ポルトガル語 (ブラジル)|0x0416|0x0409|Latin1_General_CI_AS|
|ポルトガル語 (ポルトガル)|0x0816|0x0409|Latin1_General_CI_AS|
|パンジャーブ語 (インド)|0x0446|0x0439|サーバー レベルでは利用できません|
|ケチュア語 (ボリビア)|0x046b|0x0409|Latin1_General_CI_AS|
|ケチュア語 (エクアドル)|0x086b|0x0409|Latin1_General_CI_AS|
|ケチュア語 (ペルー)|0x0c6b|0x0409|Latin1_General_CI_AS|
|ルーマニア語 (ルーマニア)|0x0418|0x0418|Romanian_CI_AS|
|ロマンシュ語 (スイス)|0x0417|0x0417|Latin1_General_CI_AI|
|ロシア語 (ロシア)|0x0419|0x0419|Cyrillic_General_CI_AS|
|サーミ語 (イナリ、フィンランド)|0x243b|0x083b|Latin1_General_CI_AI|
|サーミ語 (ルレ、ノルウェー)|0x103b|0x043b|Latin1_General_CI_AI|
|サーミ語 (ルレ、スウェーデン)|0x143b|0x083b|Latin1_General_CI_AI|
|サーミ語 (北、フィンランド)|0x0c3b|0x083b|Latin1_General_CI_AI|
|サーミ語 (北、ノルウェー)|0x043b|0x043b|Latin1_General_CI_AI|
|サーミ語 (北、スウェーデン)|0x083b|0x083b|Latin1_General_CI_AI|
|サーミ語 (スコルト、フィンランド)|0x203b|0x083b|Latin1_General_CI_AI|
|サーミ語 (南、ノルウェー)|0x183b|0x043b|Latin1_General_CI_AI|
|サーミ語 (南、スウェーデン)|0x1c3b|0x083b|Latin1_General_CI_AI|
|サンスクリット語 (インド)|0x044f|0x0439|サーバー レベルでは利用できません|
|セルビア語 (ボスニア・ヘルツェゴビナ、キリル文字)|0x1c1a|0x0c1a|Latin1_General_CI_AI|
|セルビア語 (ボスニア・ヘルツェゴビナ、ラテン文字)|0x181a|0x081a|Latin1_General_CI_AI|
|セルビア語 (セルビア、キリル文字)|0x0c1a|0x0c1a|Latin1_General_CI_AI|
|セルビア語 (セルビア、ラテン文字)|0x081a|0x081a|Latin1_General_CI_AI|
|セソト サ レボア語/北ソト語 (南アフリカ)|0x046c|0x0409|Latin1_General_CI_AS|
|セツワナ語/ツワナ語 (南アフリカ)|0x0432|0x0409|Latin1_General_CI_AS|
|シンハラ語 (スリランカ)|0x045b|0x0439|サーバー レベルでは利用できません|
|スロバキア語 (スロバキア)|0x041b|0x041b|Slovak_CI_AS|
|スロベニア語 (スロベニア)|0x0424|0x0424|Slovenian_CI_AS|
|スペイン語 (アルゼンチン)|0x2c0a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (ボリビア)|0x400a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (チリ)|0x340a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (コロンビア)|0x240a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (コスタリカ)|0x140a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (ドミニカ共和国)|0x1c0a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (エクアドル)|0x300a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (エルサルバドル)|0x440a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (グアテマラ)|0x100a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (ホンジュラス)|0x480a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (メキシコ)|0x080a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (ニカラグア)|0x4c0a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (パナマ)|0x180a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (パラグアイ)|0x3c0a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (ペルー)|0x280a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (プエルトリコ)|0x500a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (スペイン)|0x0c0a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (スペイン、トラディショナル ソート)|0x040a|0x040a|Traditional_Spanish_CI_AS|
|スペイン語 (米国)|0x540a|0x0409|Latin1_General_CI_AS|
|スペイン語 (ウルグアイ)|0x380a|0x0c0a|Modern_Spanish_CI_AS|
|スペイン語 (ベネズエラ)|0x200a|0x0c0a|Modern_Spanish_CI_AS|
|スワヒリ語 (ケニア)|0x0441|0x0409|Latin1_General_CI_AS|
|スウェーデン語 (フィンランド)|0x081d|0x040b|Finnish_Swedish_CI_AS|
|スウェーデン語 (スウェーデン)|0x041d|0x040b|Finnish_Swedish_CI_AS|
|シリア語 (シリア)|0x045a|0x045a|サーバー レベルでは利用できません|
|タジク語 (タジキスタン)|0x0428|0x0419|Cyrillic_General_CI_AS|
|タマジット語 (アルジェリア、ラテン文字)|0x085f|0x085f|Latin1_General_CI_AI|
|タミール語 (インド)|0x0449|0x0439|サーバー レベルでは利用できません|
|タタール語 (ロシア)|0x0444|0x0444|Cyrillic_General_CI_AS|
|テルグ語 (インド)|0x044a|0x0439|サーバー レベルでは利用できません|
|タイ語 (タイ)|0x041e|0x041e|Thai_CI_AS|
|チベット語 (PRC)|0x0451|0x0451|サーバー レベルでは利用できません|
|トルコ語 (トルコ)|0x041f|0x041f|Turkish_CI_AS|
|トルクメン語 (トルクメニスタン)|0x0442|0x0442|Latin1_General_CI_AI|
|ウイグル語 (PRC)|0x0480|0x0480|Latin1_General_CI_AI|
|ウクライナ語 (ウクライナ)|0x0422|0x0422|Ukrainian_CI_AS|
|上ソルブ語 (ドイツ)|0x042e|0x042e|Latin1_General_CI_AI|
|ウルドゥー語 (パキスタン)|0x0420|0x0420|Latin1_General_CI_AI|
|ウズベク語 (ウズベキスタン、キリル文字)|0x0843|0x0419|Cyrillic_General_CI_AS|
|ウズベク語 (ウズベキスタン、ラテン文字)|0x0443|0x0443|Uzbek_Latin_90_CI_AS|
|ベトナム語 (ベトナム)|0x042a|0x042a|Vietnamese_CI_AS|
|ウェールズ語 (イギリス)|0x0452|0x0452|Latin1_General_CI_AI|
|ウォロフ語 (セネガル)|0x0488|0x040c|French_CI_AS|
|コサ語 (南アフリカ)|0x0434|0x0409|Latin1_General_CI_AS|
|ヤクート語 (ロシア)|0x0485|0x0485|Latin1_General_CI_AI|
|イ語 (PRC)|0x0478|0x0409|Latin1_General_CI_AS|
|ヨルバ語 (ナイジェリア)|0x046a|0x0409|Latin1_General_CI_AS|
|ズールー語 (南アフリカ)|0x0435|0x0409|Latin1_General_CI_AS|

> [!NOTE]
> Unicode 専用の照合順序はサーバーレベルの照合順序としてサポートされないため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時に選択することはできません。    
    
サーバーに照合順序を割り当てた後は、照合順序を簡単には変更できません。変更するには、すべてのデータベース オブジェクトとデータをエクスポートし、*master* データベースを再構築してから、すべてのデータベース オブジェクトとデータをインポートする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの既定の照合順序を変更する代わりに、新しいデータベースまたはデータベース列の作成時に、目的の照合順序を指定することができます。    

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのサーバー照合順序を問い合わせるには、`SERVERPROPERTY` 関数を使用します。

```sql
SELECT CONVERT(varchar, SERVERPROPERTY('collation'));
```

使用可能なすべての照合順序についてサーバーに照会するには、次の `fn_helpcollations()` 組み込み関数を使用します。

```sql
SELECT * FROM sys.fn_helpcollations();
```
    
#### <a name="Database-level-collations"></a> データベースレベルの照合順序    
データベースを作成または変更するときに、`CREATE DATABASE` または `ALTER DATABASE` ステートメントの `COLLATE` 句を使用して、データベースの既定の照合順序を指定できます。 照合順序が指定されない場合、データベースにはサーバーの照合順序が割り当てられます。    
    
サーバーの照合順序を変更する以外に、システム データベースの照合順序を変更する方法はありません。
    
データベースの照合順序は、データベース内のすべてのメタデータで使用され、データベース内で使用されるすべての文字列型の列、一時オブジェクト、変数名、およびその他のすべての文字列の既定値になります。 ユーザー データベースの照合順序を変更する場合は、データベースのクエリが一時テーブルにアクセスするときに照合順序が競合する可能性があります。 一時テーブルは常に *tempdb* システム データベースに格納され、このデータベースではインスタンスの照合順序が使用されます。 ユーザー データベースと *tempdb* の文字データを比較するクエリは、文字データの評価で照合順序が競合すると、失敗します。 この問題は、クエリで `COLLATE` 句を指定することにより解決できます。 詳細については、「[COLLATE (Transact-SQL)](~/t-sql/statements/collations.md)」を参照してください。    

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でデータベースを作成した後は、照合順序を変更できません。

ユーザー データベースの照合順序は、次のような `ALTER DATABASE` ステートメントを使用して変更できます。

```sql
ALTER DATABASE myDB COLLATE Greek_CS_AI;
```

> [!IMPORTANT]
> データベース レベルの照合順序を変更しても、列レベルの照合順序や式レベルの照合順序には影響しません。

データベースの現在の照合順序は、次のようなステートメントを使用して取得できます。

```sql
SELECT CONVERT (VARCHAR(50), DATABASEPROPERTYEX('database_name','collation'));
```

#### <a name="Column-level-collations"></a> 列レベルの照合順序    
テーブルを作成または変更するときに、`COLLATE` 句を使用して、文字列型の各列に対して照合順序を指定できます。 照合順序を指定しない場合、列には、データベースの既定の照合順序が指定されます。    

列の照合順序は、次のような `ALTER TABLE` ステートメントを使用して変更できます。

```sql
ALTER TABLE myTable ALTER COLUMN mycol NVARCHAR(10) COLLATE Greek_CS_AI;
```
    
#### <a name="Expression-level-collations"></a> 式レベルの照合順序    
式レベルの照合順序は、ステートメントの実行時に設定され、結果セットが返される方法に影響を及ぼします。 これにより、`ORDER BY` の並べ替え結果をロケール固有のものにすることができます。 式レベルの照合順序を実装するには、次のような `COLLATE` 句を使用します。    
    
```sql    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> ロケール    
ロケールは、場所またはカルチャに関連付けられる一連の情報です。 その情報には、言語の名前や ID、言語の記述に使用される文字表記、文化的慣習などが含まれる場合があります。 照合順序は、1 つ以上のロケールに関連付けることができます。 詳細については、「 [Microsoft によって割り当てられているロケール ID](https://msdn.microsoft.com/goglobal/bb964664.aspx)」を参照してください。    
    
###  <a name="Code_Page_Defn"></a> コード ページ    
コード ページは、特定の文字表記の順序付けられた文字のセットです。コード ページでは、数値インデックス (コード ポイント値) が各文字に関連付けられます。 Windows コード ページは、通常は "*文字セット*" または *charset* と呼ばれています。 コード ページは、各種の Windows システム ロケールで使用される文字セットおよびキーボード レイアウトをサポートするために使用されます。     
 
###  <a name="Sort_Order_Defn"></a> 並べ替え順序    
並べ替え順序は、データ値の並べ替え方法を指定します。 その順序により、データ比較の結果が影響を受けます。 データは、照合順序を使用して並べ替えられ、インデックスを使用して最適化することができます。    
    
##  <a name="Unicode_Defn"></a> Unicode のサポート    
Unicode は、コード ポイントを文字にマップするための標準です。 Unicode は世界中のすべての言語のすべての文字を処理できるようにデザインされているので、異なる文字のセットを扱うために異なるコード ページは必要ありません。

### <a name="unicode-basics"></a>Unicode の基礎
1 つのデータベースに複数言語のデータを格納する場合、文字データとコード ページのみを使用すると、管理が困難になります。 また、データベース用に必要なすべての言語固有の文字を格納できる、単一のコード ページを見つけることも困難です。 さらに、さまざまなコード ページを実行するさまざまなクライアントによって読み取りや更新が行われるときに、特殊な文字が正しく翻訳されるようにすることも困難です。 さまざまな国のクライアントをサポートするデータベースでは、非 Unicode データ型ではなく常に Unicode データ型を使用する必要があります。

たとえば、次の 3 つの主要言語を扱う必要がある北米の顧客データベースについて考えてみましょう。

-  メキシコ向けのスペイン語の名前と住所
-  ケベック向けのフランス語の名前と住所
-  カナダの他の地域と米国向けの英語の名前と住所

文字型の列とコード ページのみを使用するときは、3 つの言語すべての文字を処理できるコード ページを使用してデータベースが確実にインストールされるようにする必要があります。 また、上記の中のいずれかの言語の文字が、別の言語のコード ページを実行しているクライアントで読み取られる場合は、その文字が正しく変換されるように注意する必要があります。
   
> [!NOTE]
> クライアントが使用するコード ページは、オペレーティング システム (OS) の設定によって決まります。 Windows オペレーティング システムでクライアント コード ページを設定するには、コントロール パネルの **[地域と言語のオプション]** を使用します。    

世界中のユーザーが要求するすべての文字をサポートする文字データ型のコード ページを 1 つ選択することは困難です。 国をまたぐデータベースで文字データを管理する最も簡単な方法は、Unicode をサポートするデータ型を常に使用することです。 

### <a name="unicode-data-types"></a>Unicode データ型
複数の言語を反映する文字データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降) に格納する場合は、非 Unicode データ型 (**char**、**varchar**、**text**) ではなく、Unicode データ型 (**nchar**、**nvarchar**、**ntext**) を使用してください。 

> [!NOTE]
> Unicode データ型の場合、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]では、UCS-2 を使うと最大 65,535 文字を表すことができ、補助文字を使った場合は Unicode の全範囲 (1,114,111 文字) を表すことができます。 補助文字の有効化について詳しくは、「[補助文字](#Supplementary_Characters)」をご覧ください。

代わりに、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、UTF 8 対応の照合順序 (\_UTF8) を使用した場合に、以前の非 Unicode データ型 (**char** と **varchar**) が UTF-8 エンコードを使用した Unicode データ型になります。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、UCS-2 エンコードまたは UTF-16 エンコードを引き続き使用する、以前の既存の Unicode データ型 (**nchar**、**nvarchar**、**ntext**) の動作は変わりません。 詳しくは、「[UTF-8 と UTF-16 でのストレージの相違点](#storage_differences)」をご覧ください。

### <a name="unicode-considerations"></a>Unicode の注意点
非 Unicode データ型には、多くの制限が関連付けられています。 これは、Unicode に対応していないコンピューターではコード ページの使用が 1 つに制限されているためです。 Unicode コードを使用すると、必要なコード ページ変換が少なくなるので、パフォーマンスの向上が期待できます。 Unicode 照合順序は、サーバー レベルではサポートされないため、データベース、列、式の各レベルで個別に選択する必要があります。    

データをサーバーからクライアントに移動するとき、古いクライアント ドライバーでサーバー照合順序が認識されないことがあります。 これは、データを Unicode サーバーから非 Unicode クライアントに移動する場合に発生する可能性があります。 最善の対処方法は、クライアント オペレーティング システムをアップグレードして、基になるシステムの照合順序を更新することです。 クライアントにデータベース クライアント ソフトウェアがインストールされている場合は、データベース クライアント ソフトウェアにサービスの更新プログラムを適用する方法もあります。    
    
> [!TIP]
> また、サーバー上のデータに異なる照合順序を使用してみることもできます。 クライアントのコード ページにマップする照合順序を選択します。    
>
> 一部の Unicode 文字の検索と並べ替えの機能を向上させるために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降) で使用可能な UTF-16 照合順序を使用するには (Windows 照合順序のみ)、補助文字 (\_SC) の照合順序の 1 つ、またはバージョン 140 の照合順序の 1 つを選択できます。    
 
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] で使用可能な UTF-8 照合順序を使用し、一部の Unicode 文字の検索と並べ替えの機能を向上させるには (Windows 照合順序のみ)、UTF-8 エンコード対応の照合順序 (\_UTF8) を選択する必要があります。
 
-   UTF8 フラグは、以下に適用できます。    
    -   バージョン 90 照合順序 
        > [!NOTE]
        > 補助文字 (\_SC) または異体字セレクター (\_VSS) を区別する照合順序がこのバージョンに既に存在している場合に限られます。
    -   バージョン 100 照合順序    
    -   バージョン 140 照合順序   
    -   BIN2<sup>1</sup> バイナリ照合順序
    
-   UTF8 フラグは、以下には適用できません。    
    -   補助文字 (\_SC) または異体字セレクター (\_VSS) をサポートしていないバージョン 90 照合順序    
    -   BIN または BIN2<sup>2</sup> バイナリ照合順序    
    -   SQL\_* 照合順序  
    
<sup>1</sup>[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3 以降。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0 では、照合順序 **UTF8_BIN2** が **Latin1_General_100_BIN2_UTF8** に置き換えられました。        
<sup>2</sup>[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3 まで。    
    
Unicode または非 Unicode データ型の使用に関連する問題点を評価するには、使用環境におけるパフォーマンスの違いを測定するためのシナリオをテストする必要があります。 組織内のシステムで使用する照合順序を標準化し、可能であれば Unicode サーバーおよびクライアントを配置するようにしてください。    
    
さまざまな状況で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって他のサーバーまたはクライアントとのやり取りが行われ、組織ではアプリケーションやサーバー インスタンス間で複数のデータ アクセス標準を使用する可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントは次の 2 つの主要タイプのいずれかになります。    
    
-   OLE DB および Open Database Connectivity (ODBC) バージョン 3.7 以降を使用する **Unicode クライアント**。    
-   DB ライブラリおよび ODBC バージョン 3.6 以前を使用する**非 Unicode クライアント**。    
    
以下の表では、Unicode 型サーバーと非 Unicode 型サーバーの各種の組み合わせにおける多言語データの使用に関する情報を示します。    
    
|サーバー|Client|利点または制限事項|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|このシナリオでは、システム全体で Unicode データが使用されるため、最高のパフォーマンスが実現され、取得されるデータが破損から保護されます。 これは、ActiveX Data Objects (ADO)、OLE DB、および ODBC バージョン 3.7 以降の場合に該当します。|    
|Unicode|非 Unicode|このシナリオで、特に新しいオペレーティング システムを実行しているサーバーと、古いバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または古いオペレーティング システムを実行しているクライアントが接続されている場合、データをクライアント コンピューターに移動するときに制約やエラーが発生することがあります。 サーバー上の Unicode データは、非 Unicode クライアント上の対応するコード ページにマップしてデータを変換しようと試みます。|    
|非 Unicode|Unicode|これは、多言語データの使用に理想的な構成とはいえません。 Unicode データを非 Unicode サーバーに書き込むことはできません。 サーバーのコード ページ内に存在しないサーバーにデータを送信すると、問題が発生する可能性があります。|    
|非 Unicode|非 Unicode|これは、多言語データに関して非常に制限的なシナリオです。 使用できるコード ページは 1 つだけです。|    
    
##  <a name="Supplementary_Characters"></a> 補助文字    
Unicode Consortium では、各文字に一意のコード ポイント (000000 – 10FFFF の範囲の値) が割り当てられています。 最もよく使われる文字のコード ポイント値は 000000 – 00FFFF の範囲で (65,535 文字)、これはメモリおよびディスク上の 8 ビットまたは 16 ビット ワードに適合します。 この範囲は、通常、基本多言語面 (BMP) として指定されます。 

ただし、Unicode Consortium では、さらに 16 個の文字の "面" が確立されており、それぞれ BMP と同じサイズです。 この定義により、Unicode では、000000 – 10FFFF までのコード ポイントで 1,114,112 個の文字 (つまり、2<sup>16</sup> * 17 文字) を表すことができます。 コード ポイント値が 00FFFF より大きい文字では、2 から 4 個の連続する 8 ビット ワード (UTF-8)、または 2 個の連続する 16 ビット ワード (UTF-16) が必要です。 BMP を越えて存在するこれらの文字は "*補助文字*" と呼ばれ、追加の連続する 8 ビット ワードまたは 16 ビット ワードは "*サロゲート ペア*" と呼ばれます。 補助文字、サロゲート、およびサロゲート ペアについて詳しくは、[Unicode 標準](http://www.unicode.org/standard/standard.html)をご覧ください。    

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、BMP 範囲 (000000 – 00FFFF) の Unicode データを格納するために、**nchar** や **nvarchar** などのデータ型が提供されています。これらは、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]では UCS-2 を使ってエンコードされます。 

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、完全な Unicode 文字範囲 (000000 – 10FFFF) を表すために、**nchar**、**nvarchar**、**sql_variant** の各データ型で使用できる補助文字 (\_SC) 照合順序の新しいファミリが導入されました。 次に例を示します。**Latin1_General_100_CI_AS_SC** や、日本語の照合順序を使用する場合は **Japanese_Bushu_Kakusu_100_CI_AS_SC** を使用できます。 
 
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、新しい UTF-8 対応の照合順序 ([\_UTF8](#utf8)) を使用して、補助文字のサポートが **char** および **varchar** データ型まで拡張されています。 これらのデータ型では、完全な Unicode 文字範囲を表すこともできます。   

> [!NOTE]
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降では、すべての新しい \_140 照合順序で補助文字が自動的にサポートされます。

補助文字を使用する場合は、以下の点に注意してください。    
    
-   補助文字は、90 以上の照合順序バージョンで、並べ替えと比較の操作に使用できます。    
-   すべてのバージョン 100 の照合順序で、補助文字の言語的な並べ替えがサポートされています。    
-   補助文字は、データベース オブジェクトの名前など、メタデータ内で使用することはできません。    
-   補助文字 (\_SC) を含む照合順序を使用しているデータベースでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーションを有効にすることはできません。 これは、レプリケーション用に作成されるシステム テーブルとストアド プロシージャの一部で、補助文字をサポートしていない古い **ntext** データ型が使われているためです。  

-   SC フラグは、以下に適用できます。    
    -   バージョン 90 照合順序    
    -   バージョン 100 照合順序    
    
-   SC フラグは、以下に適用できます。    
    -   バージョン 80 バージョンなしの Windows 照合順序    
    -   BIN または BIN2 バイナリ照合順序    
    -   SQL\* 照合順序    
    -   バージョン 140 照合順序 (これらでは、補助文字が既にサポートされているので、SC フラグは必要ありません)    
    
次の表では、一部の文字列関数と文字列演算子で、補助文字が SC 照合順序ありで使用される場合と、補助文字対応 (SCA) 照合順序なしで使用される場合の動作を比較しています。    
    
|文字列関数または演算子|SCA 照合順序あり|SCA 照合順序なし|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|UTF-16 サロゲート ペアは、1 つのコード ポイントとしてカウントされます。|UTF-16 サロゲート ペアは、2 つのコード ポイントとしてカウントされます。|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|これらの関数は、各サロゲート ペアを 1 つのコード ポイントとして処理し、期待どおりに動作します。|これらの関数では、サロゲート ペアが分割され、予期しない結果が生じることがあります。|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|0 – 0x10FFFF の範囲の指定した Unicode コード ポイント値に対応する文字が返されます。 指定した値が 0 – 0xFFFF の範囲内にある場合、1 つの文字が返されます。 値が大きい場合、対応するサロゲート ペアが返されます。|0 xFFFF よりも高い値の場合は、対応するサロゲートの代わりに NULL が返されます。|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|0 – 0x10FFFF の範囲の UTF-16 コード ポイントが返されます。|0 – 0xFFFF の範囲の UCS-2 コード ポイントが返されます。|    
|[1 文字に一致するワイルドカード](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [ワイルドカード - 一致しない文字列](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|補助文字は、すべてのワイルドカード操作でサポートされています。|補助文字は、これらのワイルドカード操作でサポートされていません。 その他のワイルドカード演算子がサポートされます。|    
    
## <a name="GB18030"></a> GB18030 のサポート    
GB18030 は中華人民共和国が単独で中国語の文字のエンコードに使用している標準規格です。 GB18030 文字の長さは 1 バイト、2 バイト、4 バイトのいずれかです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、クライアント側アプリケーションからサーバーに GB18030 でエンコードした文字が入力されたときに文字を認識し、内部的には Unicode 文字に変換して格納することで GB18030 文字をサポートしています。 それらがサーバーに格納されると、それ以降の操作では Unicode 文字として処理されます。 

任意の中国語の照合順序を使用できますが、最新の 100 バージョンの使用をお勧めします。 すべての \_100 レベルの照合順序は、GB18030 文字の言語的な並べ替えをサポートしています。 データに補助文字 (サロゲート ペア) が含まれている場合は、検索や並べ替えの機能を向上させるために、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で利用可能な SC 照合順序を使用できます。    

> [!NOTE]
> GB18030 でエンコードされた文字を含む文字列が正しく表示されるように、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] などのクライアント ツールでは確実に Dengxian フォントを使用します。
    
## <a name="Complex_script"></a> 複雑な文字表記のサポート    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、複雑な文字表記の入力、格納、変更、および表示をサポートできます。 複雑な文字表記には、次の種類があります。    
    
-   アラビア語テキストと英語テキストの組み合わせなど、右から左に記述されるテキストと左から右に記述されるテキストの両方の組み合わせを含む文字表記。    
-   アラビア語、インド諸語、タイ語の文字など、位置によって、または別の種類の文字と組み合わせた場合に、文字が変形する文字表記。    
-   タイ語など、単語間に区切りがないため、単語を識別するための内部辞書を必要とする言語。    
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を操作するデータベース アプリケーションは、複雑な文字表記をサポートするコントロールを使用する必要があります。 マネージド コードで作成される標準の Windows フォーム コントロールは、複雑な文字表記を使用できます。    

## <a name="Japanese_Collations"></a>[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] に追加された日本語照合順序
 
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降では、各種オプションの順列 (\_CS、\_AS、\_KS、\_WS、\_VSS) で、新しい日本語照合順序がサポートされています。 

これらの照合順序を一覧表示するには、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に対してクエリを実行します。      

```sql 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

すべての新しい照合順序には補助文字の組み込みサポートがあるので、どの新しい **\_140** 照合順序にも SC フラグはありません (または必要ありません)。

これらの照合順序は、[!INCLUDE[ssde_md](../../includes/ssde_md.md)] インデックス、メモリ最適化テーブル、列ストア インデックス、ネイティブ コンパイル モジュールでサポートされています。

<a name="ctp23"></a>

## <a name="utf8"></a> UTF-8 のサポート
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、インポートまたはエクスポートのエンコードとして、および文字列データのデータベース レベルまたは列レベルの照合順序として、広く使用されている UTF-8 文字エンコードの完全なサポートが導入されています。 UTF-8 は、**char** および **varchar** データ型で許可されており、*UTF8* サフィックスを持つようにオブジェクトの照合順序を作成するか変更すると有効になります。 たとえば、**LATIN1_GENERAL_100_CI_AS_SC** を **LATIN1_GENERAL_100_CI_AS_SC_UTF8** に変更します。 

UTF-8 は、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で導入された補助文字をサポートする Windows 照合順序にのみ使用できます。 **nchar** および **nvarchar** データ型では、UCS-2 または UTF-16 エンコードのみが許可され、変更されていません。

### <a name="storage_differences"></a> UTF-8 と UTF-16 でのストレージの相違点
Unicode Consortium では、各文字に一意のコード ポイント (000000 – 10FFFF の範囲の値) が割り当てられています。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、完全な範囲を表すために、UTF-8 エンコードと UTF-16 エンコードの両方を使用できます。    
-  UTF-8 エンコードでは、ASCII 範囲 (000000 – 00007F) の文字には 1 バイト、コード ポイント 000080 – 0007FF には 2 バイト、コード ポイント 000800 – 00FFFF には 3 バイト、コード ポイント 0010000 – 0010FFFF には 4 バイトが、それぞれ必要です。 
-  UTF-16 エンコードでは、コード ポイント 000000 – 00FFFF には 2 バイト、コード ポイント 0010000 – 0010FFFF には 4 バイトが必要です。 

次の表では、各文字範囲およびエンコード種類に対するエンコード ストレージ バイトの一覧を示します。

|コードの範囲 (16 進)|コードの範囲 (10 進)|UTF-8 でのストレージ バイト数 <sup>1</sup>|UTF-16 でのストレージ バイト数 <sup>1</sup>|    
|---------------------------------|---------------------------------|--------------------------|-----------------------------|   
|000000 – 00007F|0 – 127|1|2|
|000080 – 00009F<br />0000A0 – 0003FF<br />000400 – 0007FF|128 – 159<br />160 – 1,023<br />1,024 – 2,047|2|2|
|000800 – 003FFF<br />004000 – 00FFFF|2,048 – 16,383<br />16,384 – 65,535|3|2|
|010000 – 03FFFF<sup>2</sup><br /><br />040000 – 10FFFF<sup>2</sup>|65,536 – 262,143<sup>2</sup><br /><br />262,144 – 1,114,111<sup>2</sup>|4|4|

<sup>1</sup> "*ストレージ バイト数*" は、データ型のディスク上でのストレージ サイズではなく、エンコード済みのバイト長を示します。 ディスク上のストレージ サイズについて詳しくは、「[nchar および nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)」と「[char および varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)」をご覧ください。

<sup>2</sup>[補助文字](#Supplementary_Characters)のコード ポイント範囲。

> [!TIP]   
> [CHAR(*n*) および VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)、または[NCHAR(*n*) および NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) では、*n* は文字数を定義すると考えるのが一般的です。 これは、CHAR (10) 列の例では、0 – 127 の範囲の 10 個の ASCII 文字を **Latin1_General_100_CI_AI** などの照合順序を使用して格納できるためで、この範囲内の各文字が 1 バイトのみを使用するためです。
>    
> ただし、[CHAR(*n*) および VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) では、*n* によって "*バイト*" での文字列のサイズ (0 – 8,000) が定義され、[NCHAR(*n*) および NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) では *n* によって "*バイトペア*" での文字列のサイズ (0 – 4,000) が定義されます。 *n* は、格納できる文字数を定義しません。

見たように、使われている文字セットによっては、適切な Unicode エンコードとデータ型を選択することで、ストレージを大幅に節約したり、現在のストレージの占有領域を増やしたりする可能性があります。 たとえば、**Latin1_General_100_CI_AI_SC_UTF8** など、UTF-8 対応のラテン語の照合順序を使用する場合、`CHAR(10)` 列に 10 バイトが格納され、0 – 127 の範囲に 10 個の ASCII 文字を保持できます。 ただし、128 – 2047 の範囲では 5 文字のみ、2048 – 65535 の範囲では 3 文字のみ保持できます。 これに対して、`NCHAR(10)` 列には 10 バイトペア (20 バイト) が格納されるため、0 – 65535 の範囲に 10 文字を保持できます。  

データベースまたは列に UTF-8 または UTF-16 のどちらのエンコードを使うかを選択する前に、格納される文字列データの分布を考慮してください。
-  主に 0 – 127 の ASCII 範囲の場合は (英語など)、各文字に UTF-8 では 1 バイト、UTF-16 では 2 バイトが必要です。 UTF-8 を使う方がストレージに関してメリットがあります。 0 – 127 の範囲の ASCII 文字の既存の列データ型を、UTF-8 対応の照合順序を使って `NCHAR(10)` から `CHAR(10)` に変更すると、必要なストレージが 50% 削減されます。 このように減るのは、`NCHAR(10)` を保存するには 20 バイト必要であるのに対し、`CHAR(10)` では同じ Unicode 文字列表現に 10 バイトしか必要ないためです。    
-  ASCII の範囲の上の、ほぼすべてのラテン語系スクリプト、およびギリシャ語、キリル語、コプト語、アルメニア語、ヘブライ語、アラビア語、シリア語、Tāna、N’Ko では、UTF-8 および UTF-16 のどちらでも、1 文字あたり 2 バイトが必要です。 これらの場合は、対応するデータ型で大きなストレージの違いはありません (たとえば、**char** または **nchar** を使う場合)。
-  主に東アジア言語のスクリプト (韓国語、中国語、日本語) の場合は、各文字に UTF-8 では 3 バイト、UTF-16 では 2 バイトが必要です。 UTF-16 を使う方がストレージに関してメリットがあります。 
-  010000 – 10FFFF の範囲の文字には、UTF-8 と UTF-16 のどちらでも 4 バイト必要です。 これらの場合は、対応するデータ型でストレージの違いはありません (たとえば、**char** または **nchar** を使う場合)。

その他の考慮事項については、「[国際化に対応した Transact-SQL ステートメントの記述](../../relational-databases/collations/write-international-transact-sql-statements.md)」をご覧ください。

### <a name="converting"></a>UTF-8 への変換
[CHAR(*n*) と VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)、または [NCHAR(*n*) と NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) では、*n* によって、格納できる文字数ではなく、バイト ストレージのサイズが決定するため、データの切り捨てを回避するために、変換が必要なデータ型のサイズを決定することが重要です。 

たとえば、日本語の文字を 180 バイト格納する **NVARCHAR (100)** として定義された列について考えてみましょう。 この例では現在、列データは、1 文字あたり 2 バイトを使用する UCS-2 または UTF-16 を使用してエンコードされています。 列の型を **VARCHAR (200)** に変換しても、データの切り捨てを防ぐことはできません。新しいデータ型で格納できるのは 200 バイトだけですが、日本語の文字は、UTF-8 でエンコードされている場合には 3 バイト必要となるからです。 そのため、データの切り捨てによるデータの損失を回避するために、列を **VARCHAR(270)** として定義する必要があります。

したがって、既存のデータを UTF-8 に変換する前に、予想される列定義のバイトサイズを事前に把握し、それに応じて新しいデータ型のサイズを調整する必要があります。 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 関数と [COLLATE](../../t-sql/statements/collations.md) ステートメントを使用して、既存のデータベースでの UTF-8 変換操作に必要なデータ長の適正な要件を決定するには、[Data Samples GitHub](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/unicode) の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトまたは SQL Notebook を参照してください。

既存のテーブル内の列の照合順序とデータ型を変更するには、「[列の照合順序の設定または変更](../../relational-databases/collations/set-or-change-the-column-collation.md)」で説明されているいずれかの方法を使用します。

データベースの照合順序を変更して、新しいオブジェクトが既定でデータベースの照合順序を継承できるようにするか、またはサーバーの照合順序を変更して、新しいデータベースが既定でシステムの照合順序を継承できるようにするには、この記事の「[関連タスク](#Related_Tasks)」セクションを参照してください。 

##  <a name="Related_Tasks"></a> 関連タスク    
    
|タスク|トピック|    
|----------|-----------|    
|SQL Server のインスタンスの照合順序を設定または変更する方法について説明します。 サーバーの照合順序を変更しても、既存のデータベースの照合順序は変更されないことに注意してください。|[サーバーの照合順序の設定または変更](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|ユーザー データベースの照合順序を設定または変更する方法について説明します。 データベースの照合順序を変更しても、既存のテーブル列の照合順序は変更されないことに注意してください。|[データベースの照合順序の設定または変更](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|データベース内の列の照合順序を設定または変更する方法について説明します|[列の照合順序の設定または変更](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|サーバー、データベース、または列のレベルでの照合順序の情報を取得する方法について説明します|[照合順序情報の表示](../../relational-databases/collations/view-collation-information.md)|    
|Transact-SQL ステートメントを、ある言語から別の言語に容易に移行したり、複数の言語を簡単にサポートしたりできるように記述する方法について説明します|[国際化に対応した Transact-SQL ステートメントの記述](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|エラー メッセージの言語と、日付、時刻、通貨データを使用および表示する際の設定を変更する方法について説明します|[セッション言語の設定](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> Related content    
詳細については、次の関連コンテンツを参照してください。
* [SQL Server ベスト プラクティス照合順序の変更](https://go.microsoft.com/fwlink/?LinkId=113891)  
* [Unicode 文字形式を使用したデータのインポートまたはエクスポート (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
* [国際化に対応した Transact-SQL ステートメントの記述](../../relational-databases/collations/write-international-transact-sql-statements.md)  
* [SQL Server ベスト プラクティス Unicode への移行](https://go.microsoft.com/fwlink/?LinkId=113890) (今後は維持されません)   
* [Unicode コンソーシアム](https://go.microsoft.com/fwlink/?LinkId=48619)  
* [Unicode 標準](http://www.unicode.org/standard/standard.html)  
* [OLE DB Driver for SQL Server の UTF-8 のサポート](../../connect/oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
* [SQL Server 照合順序名 (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)  
* [Windows 照合順序名 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)  
* [SQL Server 用の UTF-8 サポートの概要](https://techcommunity.microsoft.com/t5/SQL-Server/Introducing-UTF-8-support-for-SQL-Server/ba-p/734928)       
    
## <a name="see-also"></a>参照    
[包含データベースの照合順序](../../relational-databases/databases/contained-database-collations.md)     
[フルテキスト インデックス作成時の言語の選択](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
[sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)       
[1 バイト文字セットとマルチバイト文字セット](https://docs.microsoft.com/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)      
 
