---
title: フルテキスト検索に使用する類義語辞典ファイルの構成と管理
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], configuring
- thesaurus [full-text search]
ms.assetid: 3ef96a63-8a52-45be-9a1f-265bff400e54
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.openlocfilehash: c54c1774622416adb213b31852941c934be7af24
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056201"
---
# <a name="configure-and-manage-thesaurus-files-for-full-text-search"></a>フルテキスト検索に使用する類義語辞典ファイルの構成と管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト検索クエリでは、フルテキスト検索の*類義語辞典*を使用して、ユーザーが指定した用語のシノニムを検索できます。 各々の類義語辞典では、特定の言語の一連のシノニムを定義します。 フルテキスト データに合わせた類義語辞典を作成すると、そのデータのフルテキスト クエリのスコープを効果的に拡張できます。

類義語辞典の照合は、すべての [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) クエリと [FREETEXTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) クエリの場合と `FORMSOF THESAURUS` 句を指定する [CONTAINS](../../t-sql/queries/contains-transact-sql.md) クエリと [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) クエリの場合に行われます。
  
フルテキスト検索の類義語辞典は、XML テキスト ファイルです。
  
##  <a name="tasks"></a>類義語辞典の機能  
 フルテキスト検索クエリで特定の言語のシノニムを検索するには、その言語の類義語辞典のマッピング (シノニム) を定義しておく必要があります。 各類義語辞典は、次の内容を定義するために手動で構成する必要があります。  
  
-   拡張セット  
  
     拡張セットには、フルテキスト クエリで相互に置き換えられる "writer"、"author"、"journalist" などのシノニムのグループが格納されます。 拡張セット内のシノニムと一致するクエリは、拡張セット内の他のシノニムもすべて含むように拡張されます。  
  
     詳細については、このトピックの後半の「[拡張セットの XML 構造](#expansion)」をご覧ください。  
  
-   置換セット  
  
     置換セットには、代替セットによって置き換えられるテキストのパターンが格納されます。 このトピックの後半で説明する「[置換セットの XML 構造](#replacement)」の例をご覧ください。 

-   分音文字の設定  
  
     類義語辞典では、チルダ ( **~** )、アキュート アクセント記号 ( **&acute;** )、ウムラウト ( **&uml;** ) などの分音記号をすべての検索パターンで区別するかしないか (つまり、"*アクセントを区別する*" か "*アクセントを区別しない*" か) が設定されます。 たとえば、フルテキスト クエリで "caf&eacute;" というパターンが他のパターンに置き換えられるように指定するとします。 類義語辞典でアクセントが区別されない場合、フルテキスト検索では、パターン "caf&eacute;" と "cafe" が置き換えられます。 類義語辞典でアクセントが区別される場合、フルテキスト検索では "caf&eacute;" というパターンのみが置き換えられます。 既定では、類義語辞典でアクセントは区別されません。  
  
##  <a name="initial_thesaurus_files"></a> 既定の類義語辞典ファイル
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には XML 類義語辞典ファイルのセットが用意されており、サポートされている各言語に対して 1 つのファイルが存在します。 これらのファイルは基本的に空です。 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類義語辞典およびコメント アウトされたサンプル類義語辞典に共通する最上位の XML 構造のみが格納されています。  
  
##  <a name="location"></a> 類義語辞典ファイルの場所  
 類義語辞典ファイルの既定の場所は次のとおりです。  
  
     <SQL_Server_data_files_path>\MSSQL13.MSSQLSERVER\MSSQL\FTDATA\  
  
 この既定の場所には、次のファイルが格納されています。  
  
-   **言語固有の**類義語辞典ファイル  

    セットアップでは、空の類義語辞典ファイルが前述の場所にインストールされます。 サポートされている言語ごとに個別のファイルが用意されています。 システム管理者は、これらのファイルをカスタマイズできます。  
  
     類義語辞典ファイルの既定のファイル名には、次の形式が使用されます。  
  
         'ts' + <three-letter language-abbreviation> + '.xml'  
  
     指定した言語の類義語辞典ファイルの名前は、レジストリで次のように指定されます。
     
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<instance-name>\MSSearch\<language-abbrev>  
  
-   **グローバル**類義語辞典ファイル  
  
     tsGlobal.xml は空のグローバル類義語辞典ファイルです。  

### <a name="change-the-location-of-a-thesaurus-file"></a>類義語辞典ファイルの場所を変更する 
類義語辞典ファイルの場所および名前を変更するには、そのレジストリ キーを変更します。 各言語の類義語辞典ファイルの場所は、レジストリで次のように指定されています。  
  
    HKLM\SOFTWARE\Microsoft\Microsoft SQL Server\<instance name>\MSSearch\Language\<language-abbreviation>\TsaurusFile  
  
 グローバル類義語辞典ファイルは、LCID 0 のニュートラル言語に対応します。 この値は、管理者のみが変更できます。  

##  <a name="how_queries_use_tf"></a>フルテキスト クエリで類義語辞典を使用する方法  
類義語辞典クエリでは、言語固有の類義語辞典とグローバル類義語辞典の両方が使用されます。
1.  まず、言語固有のファイルが参照されて処理のために読み込まれ (まだ読み込まれていない場合)、 類義語辞典ファイル内の拡張セットおよび置換セットのルールで指定された言語固有のシノニムを含むようにクエリが拡張されます。 
2.  この手順がグローバル類義語辞典に対して繰り返されます。 ただし、言語固有の類義語辞典ファイルで既に一致するものが見つかった用語は、グローバル類義語辞典では照合されません。  

##  <a name="structure"></a> 類義語辞典ファイルの構造  
 各類義語辞典ファイルでは、ID が `Microsoft Search Thesaurus` の XML コンテナー、およびサンプル類義語辞典を含むコメント `<!--`...`-->` が定義されます。 類義語辞典は `<thesaurus>` 要素で定義されます。この要素には、分音記号の設定、拡張セット、置換セットを定義する子要素のサンプルが含まれます。

一般的な空の類義語辞典ファイルには、次の XML テキストが含まれています。  
  
```xml  
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

### <a name="expansion"></a> 拡張セットの XML 構造  
  
 各拡張セットは `<expansion>` 要素で囲みます。 この要素内に、`<sub>` 要素で囲んだ 1 つまたは複数の代替文字列を指定します。 拡張セットでは、互いにシノニムとなる代替文字列のグループを指定できます。  
  
 たとえば、拡張のセクションを編集して、代替文字列 "writer"、"author"、および "journalist" をシノニムとして扱うことができます。 1 つの代替文字列と一致するフルテキスト検索クエリは、拡張セット内の他の代替文字列もすべて含むように拡張されます。 したがって、上記の例では、"author" という語に対して FORMS OF THESAURUS クエリまたは FREETEXT クエリを実行すると、フルテキスト検索では "writer" と "journalist" という語も含む検索結果が返されます。  
  
上記の例の拡張セットのセクションを次に示します。  
  
```xml  
<expansion>  
        <sub>writer</sub>  
        <sub>author</sub>  
        <sub>journalist</sub>  
</expansion>  
```  
  
### <a name="replacement"></a> 置換セットの XML 構造  
  
各置換セットは `<replacement>` 要素で囲みます。 この要素内に、`<pat>` 要素で囲んだ 1 つ以上のパターンと `<sub>` 要素で囲んだ 0 個以上の代替文字列 (シノニムごとに 1 つ) を指定できます。 ここで指定するパターンが代替セットで置き換えられます。 パターンと代替文字列には、語または語の並びを含めることができます。 パターンに対して代替文字列が指定されていない場合は、ユーザー クエリからパターンが削除されます。  
  
たとえば、"Win8" というパターンを検索するクエリを、"Windows Server 2012" または "Windows 8.0" という代替文字列に置き換えるとします。 この場合、"Win8" に対してフルテキスト クエリを実行すると、フルテキスト検索からは "Windows Server 201" または "Windows 8.0" だけを含む検索結果が返されます。 "Win8" を含む結果は返されません。 これは、"Win8" が "Windows Server 2012" と "Windows 8.0" というパターンに置換されるためです。  
  
上記の例の置換セットのセクションを次に示します。  
  
```xml  
<replacement>  
        <pat>Win8</pat>  
        <sub>Windows Server 2012</sub>  
        <sub>Windows 8.0</sub>  
</replacement>  
```  
  
類似するパターンを含む 2 つの置換セットが一致する場合、2 つのうちで長い置換セットが優先されます。 たとえば、"Internet Explorer online community" に対して FORMS OF THESAURUS クエリを実行し、次の置換セットを使用すると、"Internet Explorer" 置換セットの方が "Internet" 置換セットよりも優先されます。 したがって、このクエリは "IE online community" または "IE 9 online community" として処理されます。  
  
```xml  
<replacement>  
         <pat>Internet</pat>  
         <sub>intranet</sub>  
</replacement>  
```  
  
クエリと  
  
```xml  
<replacement>  
         <pat>Internet Explorer</pat>  
         <sub>IE</sub>  
         <sub>IE 9</sub>  
</replacement>  
```

### <a name="xml-structure-of-the-diacritics-setting"></a>分音記号の設定の XML 構造  
  
類義語辞典の分音文字の設定は、単一の `<diacritics_sensitive>` 要素で指定されます。 この要素には、次のようにアクセントの区別を制御する整数値が含まれます。  
  
|分音文字の設定|[値]|XML|  
|------------------------|-----------|---------|  
|アクセントを区別しない|0|`<diacritics_sensitive>0</diacritics_sensitive>`|  
|アクセントを区別する|1|`<diacritics_sensitive>1</diacritics_sensitive>`|  
  
> [!NOTE]  
>  この設定はファイルで 1 回のみ適用でき、ファイル内のすべての検索パターンに適用されます。 この設定は個別のパターンには指定できません。  

##  <a name="editing"></a> 類義語辞典ファイルの編集  
特定の言語の類義語辞典は、類義語辞典ファイル (XML ファイル) を編集することによって構成できます。 セットアップ中に、`<xml>` コンテナーとコメント アウトされたサンプルの `<thesaurus`> 要素のみが格納されている空の類義語辞典ファイルがインストールされます。 シノニムを検索するフルテキスト検索クエリを正しく機能させるには、一連のシノニムを定義する実際の `<thesaurus`> 要素を作成する必要があります。 シノニムの定義には、拡張セットと置換セットという 2 つの形式があります。  

### <a name="edit-a-thesaurus-file"></a>類義語辞典ファイルを編集する  
  
1.  メモ帳またはその他のテキスト エディターで類義語辞典ファイルを開きます。  
  
2.  初めて類義語辞典ファイルを編集する場合は、ファイルの先頭と末尾の次のコメント行をそれぞれ削除します。  
  
    ```xml  
    <!--Commented out  
    -->  
    ```  
  
3.  置換セットまたは拡張セットを追加、変更、または削除します。  
  
4.  ファイルを保存し、メモ帳を閉じます。  
  
5.  類義語辞典ファイルの内容を tempdb に読み込むために [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md) を使用し、類義語辞典ファイルの言語に対応するロケール識別子 (LCID) を指定します。 たとえば、英語の類義語辞典ファイル tsenu.xml の場合、対応する LCID は 1033 です。  
  
    ```sql  
    USE AdventureWorks;  
    EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
    GO
    ```

### <a name="recommendations-for-editing-thesaurus-files"></a>類義語辞典ファイルの編集に関する推奨事項  
  
 類義語辞典ファイル内のエントリには特殊文字を含めないことをお勧めします。 これは、特殊文字に対するワード ブレーカーの動作がわかりづらいためです。 類義語辞典のエントリに特殊文字が含まれる場合、そのエントリと組み合わせて使用されるワード ブレーカーの動作がフルテキスト クエリに与える影響がわかりづらくなる可能性があります。  
  
 ストップワードはフルテキスト インデックスから省略されるため、`<sub>` エントリにはストップワードを含めないことをお勧めします。 クエリは類義語辞典ファイルの `<sub>` エントリを含むように拡張されるため、`<sub>` エントリにストップワードが含まれる場合は、クエリのサイズが不必要に大きくなります。  

### <a name="restrictions-for-editing-thesaurus-files"></a>類義語辞典ファイルの編集に関する制限事項  
  
 類義語辞典ファイルの編集には、次の制限が適用されます。  
  
-   類義語辞典ファイルを更新、変更、または削除できるのはシステム管理者だけです。  
  
-   テキスト エディター ツールを使用して類義語辞典ファイルを編集する場合、ファイルが Unicode 形式で保存され、バイト順マークが指定されている必要があります。  
  
-   類義語辞典のエントリを空にしたり、空の文字列の単語に区切ったりすることはできません。  
  
-   類義語辞典ファイルの語句は 512 文字以下にする必要があります。  
  
-   類義語辞典には、拡張セットの `<sub>` エントリと置換セットの `<pat>` 要素間で重複したエントリを含めることはできません。  

## <a name="see-also"></a>参照  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)     
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)
 
