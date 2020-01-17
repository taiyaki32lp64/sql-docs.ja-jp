---
title: フルテキスト検索に使用する類義語辞典ファイルの構成と管理 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], configuring
- thesaurus [full-text search]
ms.assetid: 3ef96a63-8a52-45be-9a1f-265bff400e54
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e52399dc77fce220bf33939b7c7921e32cd2438c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011476"
---
# <a name="configure-and-manage-thesaurus-files-for-full-text-search"></a>フルテキスト検索に使用する類義語辞典ファイルの構成と管理
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではフルテキスト クエリで類義語辞典を使用し、指定した用語のシノニムを検索できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の*類義語辞典*では、特定の言語の一連のシノニムを定義します。 システム管理者は、拡張セットと置換セットという 2 つの形式のシノニムを定義できます。 フルテキスト データに合わせた類義語辞典を作成すると、そのデータのフルテキスト クエリのスコープを効果的に拡張できます。 類義語辞典の照合は、FORMSOF THESAURUS 句を指定する [CONTAINS](/sql/t-sql/queries/freetext-transact-sql) クエリと [CONTAINSTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) クエリの場合、およびすべての [FREETEXT](/sql/t-sql/queries/contains-transact-sql) クエリと [FREETEXTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) クエリの場合に行われます。  
  
##  <a name="tasks"></a> 類義語辞典ファイルを設定するための基本的なタスク  
 サーバー インスタンス上のフルテキスト検索クエリで特定の言語のシノニムを検索するには、その言語の類義語辞典のマッピング (シノニム) を定義しておく必要があります。 各類義語辞典は、次の内容を定義するために手動で構成する必要があります。  
  
-   分音文字の設定  
  
     すべての検索パターンは機密性の高いまたはチルダなどの分音記号の区別に関する特定の類義語辞典の ( **~** )、アキュート アクセント記号 ( **??** )、またはウムラウト ( **??** ) (つまり、*アクセントの区別*または*アクセントを区別しない*)。 たとえば、「カフェ??」というパターンを指定します。 フルテキスト クエリでは、他のパターンによって置き換えられます。 類義語辞典は、アクセントを区別しない場合、フルテキスト検索では、パターン「カフェ??」が置き換えられます 「カフェ」。 類義語辞典がアクセントを区別する場合は、フルテキスト検索にのみ、パターン「カフェ??」が置き換えられます。 既定では、類義語辞典でアクセントは区別されません。  
  
-   拡張セット  
  
     拡張セットには、フルテキスト クエリで相互に置き換えられる "writer"、"author"、"journalist" などのシノニムのグループが格納されます。 拡張セット内のシノニムと一致するクエリは、拡張セット内の他のシノニムもすべて含むように拡張されます。  
  
     詳細については、このトピックの後半の「拡張セットの XML 構造」をご覧ください。  
  
-   置換セット  
  
     置換セットには、代替セットによって置き換えられるテキストのパターンが格納されます。 このトピックの後半で説明する「置換セットの XML 構造」の例をご覧ください。  
  
  
##  <a name="initial_thesaurus_files"></a> 類義語辞典ファイルの初期コンテンツ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には XML 類義語辞典ファイルのセットが用意されており、サポートされている各言語に対して 1 つのファイルが存在します。 これらのファイルは基本的に空です。 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類義語辞典およびコメント アウトされたサンプル類義語辞典に共通する最上位の XML 構造のみが格納されています。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でリリースされている類義語辞典ファイルには、すべて次の XML コードが含まれています。  
  
```  
<XML ID="Microsoft Search Thesaurus">  
  
<!--  Commented out  
  
    <thesaurus xmlns="x-schema:tsSchema.xml">  
<diacritics_sensitive>0</diacritics_sensitive>  
        <expansion>  
            <sub>Internet Explorer</sub>  
            <sub>IE</sub>  
            <sub>IE5</sub>  
        </expansion>  
        <replacement>  
            <pat>NT5</pat>  
            <pat>W2K</pat>  
            <sub>Windows 2012</sub>  
        </replacement>  
        <expansion>  
            <sub>run</sub>  
            <sub>jog</sub>  
        </expansion>  
    </thesaurus>  
-->  
</XML>  
```  
  
  
##  <a name="location"></a> 類義語辞典ファイルの場所  
 類義語辞典ファイルの既定の場所は次のとおりです。  
  
 *<SQL_Server_data_files_path>* \MSSQL12.MSSQLSERVER\MSSQL\FTDATA\  
  
 この既定の場所には、次のファイルが格納されています。  
  
-   言語固有の類義語辞典ファイル  
  
     セットアップ中に、空の類義語辞典ファイルが前述の場所にインストールされます。 サポートされている言語ごとに個別のファイルが用意されています。 システム管理者は、これらのファイルをカスタマイズできます。  
  
     類義語辞典ファイルの既定のファイル名には、次の形式が使用されます。  
  
     'ts' + \<three-letter language-abbreviation> + '.xml'  
  
     特定の言語の類義語辞典ファイルの名前は、レジストリで HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<instance-name>\MSSearch\\<language-abbrev> と指定されています。  
  
-   グローバル類義語辞典ファイル  
  
     tsGlobal.xml は空のグローバル類義語辞典ファイルです。  
  
 類義語辞典ファイルの場所および名前を変更するには、そのレジストリ キーを変更します。 各言語の類義語辞典ファイルの場所は、レジストリで次のように指定されています。  
  
 HKLM、ソフトウェア、Microsoft または Microsoft SQL Server/\<インスタンス名>/MSSearch/言語/\<言語の省略形 >/TsaurusFile  
  
 グローバル類義語辞典ファイルは、LCID 0 のニュートラル言語に対応します。 この値は、管理者のみが変更できます。  
  
  
##  <a name="how_queries_use_tf"></a> クエリの使用の類義語辞典ファイルをする方法  
 類義語辞典クエリでは、言語固有の類義語辞典とグローバル類義語辞典の両方が使用されます。 まず、言語固有のファイルが参照されて処理のために読み込まれ (まだ読み込まれていない場合)、 類義語辞典ファイル内の拡張セットおよび置換セットのルールで指定された言語固有のシノニムを含むようにクエリが拡張されます。 この手順がグローバル類義語辞典に対して繰り返されます。 ただし、言語固有の類義語辞典ファイルで既に一致するものが見つかった用語は、グローバル類義語辞典では照合されません。  
  
  
##  <a name="structure"></a> 類義語辞典ファイルの構造を理解します。  
 各類義語辞典ファイルでは、ID が `Microsoft Search Thesaurus` の XML コンテナー、およびサンプル類義語辞典を含むコメント `<!--`...`-->` が定義されます。 類義語辞典がで定義されている、\<類義語辞典 > 要素を次のように分音文字の設定、拡張セット、および置換セットを定義する子要素のサンプルが含まれています。  
  
-   分音文字の設定の XML 構造  
  
     類義語辞典の分音文字の設定は、単一の <diacritics_sensitive> 要素で指定されます。 この要素には、次のようにアクセントの区別を制御する整数値が含まれます。  
  
    |分音文字の設定|値|XML|  
    |------------------------|-----------|---------|  
    |アクセントを区別しない|0|`<diacritics_sensitive>0</diacritics_sensitive>`|  
    |アクセントを区別する|1|`<diacritics_sensitive>1</diacritics_sensitive>`|  
  
    > [!NOTE]  
    >  この設定はファイルで 1 回のみ適用でき、ファイル内のすべての検索パターンに適用されます。 この設定は個別のパターンには指定できません。  
  
-   拡張セットの XML 構造  
  
     囲まれている各拡張セット、\<拡張 > 要素。 この要素内で 1 つまたは複数の置換を指定する、 \<sub > 要素。 拡張セットでは、互いにシノニムとなる代替文字列のグループを指定できます。  
  
     たとえば、拡張のセクションを編集して、代替文字列 "writer"、"author"、および "journalist" をシノニムとして扱うことができます。 1 つの代替文字列と一致するフルテキスト検索クエリは、拡張セット内の他の代替文字列もすべて含むように拡張されます。 したがって、上記の例では、"author" という語に対して FORMS OF THESAURUS クエリまたは FREETEXT クエリを実行すると、フルテキスト検索では "writer" と "journalist" という語も含む検索結果が返されます。  
  
     上記の例の拡張セットのセクションを次に示します。  
  
    ```  
    <expansion>  
            <sub>writer</sub>  
            <sub>author</sub>  
            <sub>journalist</sub>  
    </expansion>  
    ```  
  
-   置換セットの XML 構造  
  
     各置換セットがで囲まれた、\<置換 > 要素。 この要素内で 1 つまたは複数のパターンを指定することができます、 \<pat > 要素と 0 個以上の代替で\<sub > 要素、シノニムごとに 1 つ。 ここで指定するパターンが代替セットで置き換えられます。 パターンと代替文字列には、語または語の並びを含めることができます。 パターンに対して代替文字列が指定されていない場合は、ユーザー クエリからパターンが削除されます。  
  
     たとえば、"Win8" というパターンを検索するクエリを、"Windows Server 2012" または "Windows 8.0" という代替文字列に置き換えるとします。 この場合、"Win8" に対してフルテキスト クエリを実行すると、フルテキスト検索からは "Windows Server 201" または "Windows 8.0" だけを含む検索結果が返されます。 "Win8" を含む結果は返されません。 これは、"Win8" が "Windows Server 2012" と "Windows 8.0" というパターンに置換されるためです。  
  
     上記の例の置換セットのセクションを次に示します。  
  
    ```  
    <replacement>  
            <pat>Win8</pat>  
            <sub>Windows Server 2012</sub>  
            <sub>Windows 8.0</sub>  
    </replacement>  
    ```  
  
     類似するパターンを含む 2 つの置換セットが一致する場合、2 つのうちで長い置換セットが優先されます。 たとえば、"Internet Explorer online community" に対して FORMS OF THESAURUS クエリを実行し、次の置換セットを使用すると、"Internet Explorer" 置換セットの方が "Internet" 置換セットよりも優先されます。 したがって、このクエリは "IE online community" または "IE 9 online community" として処理されます。  
  
    ```  
    <replacement>  
             <pat>Internet</pat>  
             <sub>intranet</sub>  
    </replacement>  
    ```  
  
     、  
  
    ```  
    <replacement>  
             <pat>Internet Explorer</pat>  
             <sub>IE</sub>  
             <sub>IE 9</sub>  
    </replacement>  
    ```  
  
  
##  <a name="working_with_thesaurus_files"></a> 類義語辞典ファイルの使用  
 **類義語辞典ファイルを編集するには**  
  
-   [類義語辞典ファイルを編集します。](#editing)  
  
 **更新された類義語辞典ファイルを読み込む**  
  
-   [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql)  
  
 **ワード ブレーカー、類義語辞典、およびストップ リストの組み合わせのトークン化の結果を表示するには**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
  
##  <a name="editing"></a> 類義語辞典ファイルを編集します。  
 特定の言語の類義語辞典は、類義語辞典ファイル (XML ファイル) を編集することによって構成できます。 セットアップ中に、空の類義語辞典ファイルのみが含まれている、 \<xml > コンテナーおよびコメント アウトされたサンプル\<類義語辞典 > 要素をインストールします。 順序で、フルテキスト検索クエリを正常に機能するシノニムを検索する必要がありますを作成、実際\<類義語辞典 > 一連のシノニムを定義する要素。 シノニムの定義には、拡張セットと置換セットという 2 つの形式があります。  
  
 **類義語辞典ファイルの制限**  
  
 類義語辞典ファイルの編集には、次の制限が適用されます。  
  
-   類義語辞典ファイルを更新、変更、または削除できるのはシステム管理者だけです。  
  
-   テキスト エディター ツールを使用して類義語辞典ファイルを編集する場合、ファイルが Unicode 形式で保存され、バイト順マークが指定されている必要があります。  
  
-   類義語辞典のエントリを空にしたり、空の文字列の単語に区切ったりすることはできません。  
  
-   類義語辞典ファイルの語句は 512 文字以下にする必要があります。  
  
-   類義語辞典には間で重複したエントリが含まれていない必要があります、 \<sub > 拡張セットのエントリと\<pat > 置換セットの要素。  
  
 **類義語辞典ファイルに関する推奨事項**  
  
 類義語辞典ファイル内のエントリには特殊文字を含めないことをお勧めします。 これは、特殊文字に対するワード ブレーカーの動作がわかりづらいためです。 類義語辞典のエントリに特殊文字が含まれる場合、そのエントリと組み合わせて使用されるワード ブレーカーの動作がフルテキスト クエリに与える影響がわかりづらくなる可能性があります。  
  
 お勧め\<sub > エントリ ストップ ワードを含めないストップ ワードはフルテキスト インデックスから省略されるためです。 ようにクエリが拡張されます、 \<sub > エントリを類義語辞典ファイルから場合に、 \<sub > エントリにストップ ワードが含まれています、クエリのサイズが不必要に。  
  
#### <a name="to-edit-a-thesaurus-file"></a>類義語辞典ファイルを編集するには  
  
1.  類義語辞典ファイルをメモ帳で開きます。  
  
2.  初めて類義語辞典ファイルを編集する場合は、ファイルの先頭と末尾の次のコメント行をそれぞれ削除します。  
  
    ```  
    <!--Commented out  
    -->  
    ```  
  
3.  置換セットまたは拡張セットを追加、変更、または削除します。  
  
4.  ファイルを保存し、メモ帳を閉じます。  
  
5.  類義語辞典ファイルの内容を tempdb に読み込むために [sp_fulltext_load_thesaurus_file](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql) を使用し、類義語辞典ファイルの言語に対応するロケール識別子 (LCID) を指定します。 たとえば、英語の類義語辞典ファイル tsenu.xml の場合、対応する LCID は 1033 です。  
  
    ```  
    USE AdventureWorks2012 ;  
    EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
    GO  
    ```  
  
  
## <a name="see-also"></a>参照  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [フルテキスト検索](full-text-search.md)  
  
  
