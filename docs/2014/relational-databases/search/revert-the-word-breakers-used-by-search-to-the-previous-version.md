---
title: 検索で使用するワード ブレーカーを以前のバージョンに戻す | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 29b4488e-4c6a-4bf0-a64d-19e2fdafa7ae
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9e0eadbbc2d126a001057cf5f9d0e17211c0a93e
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874725"
---
# <a name="revert-the-word-breakers-used-by-search-to-the-previous-version"></a>検索で使用するワード ブレーカーを以前のバージョンに戻す
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、フルテキスト検索でサポートされているすべての言語 (韓国語を除く) 用のワード ブレーカーおよびステマーのバージョンがインストールされ、有効になります。 このトピックでは、これらのコンポーネントのこのバージョンを前のバージョンに切り替えたり、前のバージョンから新しいバージョンに切り替えたりする方法について説明します。  
  
 このトピックでは、次の言語については説明しません。  
  
-   **英語**。 英語のコンポーネントに戻す、または英語のコンポーネントを復元するには、「 [Change the Word Breaker Used for US English and UK English](change-the-word-breaker-used-for-us-english-and-uk-english.md)」を参照してください。  
  
-   **デンマーク語、ポーランド語、およびトルコ語**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のリリースに含まれていたデンマーク語、ポーランド語、およびトルコ語向けのサードパーティ製のワード ブレーカーは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] コンポーネントに置き換えられました。  
  
-   **チェコ語とギリシャ語**。 チェコ語とギリシャ語向けの新しいワード ブレーカーがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フルテキスト検索の以前のリリースでは、これらの 2 つの言語のサポートは含まれていません。  
  
-   **韓国語**。 韓国語向けのワード ブレーカーとステマーは、このリリースではアップグレードされていません。  
  
 ワード ブレーカーとステマーの全般的な情報については、「 [検索用のワード ブレーカーとステミング機能の構成と管理](configure-and-manage-word-breakers-and-stemmers-for-search.md)」を参照してください。  
  
##  <a name="overview"></a> ワード ブレーカーとステマーの切り替えと復元の概要  
 ワード ブレーカーとステマーの切り替えと復元の手順は、言語によって異なります。 次の表は、以前のバージョンのコンポーネントに戻す場合に必要な 3 組の操作をまとめたものです。  
  
|現在のファイル|以前のファイル|影響を受ける言語の数|ファイルに対する操作|レジストリ エントリに対する操作|  
|------------------|-------------------|----------------------------------|----------------------|---------------------------------|  
|NaturalLanguage6.dll|NaturalLanguage6.dll|34|以前のバージョンの NaturalLanguage6.dll を入手してインストールし、現在のバージョンのファイルを上書きします。|操作は不要です。<br /><br /> レジストリのキーと値は、このリリースでは変更されていません。|  
|(その他のファイル名)|NaturalLanguage6.dll|5|以前のバージョンの NaturalLanguage6.dll を入手してインストールし、現在のバージョンのファイルを上書きします。|以前のバージョンのコンポーネントを指定するようにレジストリ エントリのセットを変更します。|  
|(その他のファイル名)|(その他のファイル名)|6|操作は不要です。<br /><br /> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のセットアップでは、現在と以前の両方のバージョンのコンポーネントを Binn フォルダーにコピーします。|以前のバージョンのコンポーネントを指定するようにレジストリ エントリのセットを変更します。|  
  
> [!WARNING]  
>  現在のバージョンのファイル (NaturalLanguage6.dll) を別のバージョンに置き換えると、そのファイルを使用するすべての言語の動作が影響を受けます。  
  
 このトピックで説明するファイルは、 `MSSQL\Binn` インスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フォルダーにインストールされる DLL ファイルです。 通常、完全なパスは次のようになります。  
  
 `C:\Program Files\Microsoft SQL Server\<instance>\MSSQL\Binn`  
  
##  <a name="nl6nl6"></a> 現在と以前のワード ブレーカーのファイル名が NaturalLanguage6.dll である言語  
 次の表に示す言語では、現在と以前のワード ブレーカーのファイル名が NaturalLanguage6.dll です。 これらのコンポーネントの切り替えまたは復元を行うには、NaturalLanguage6.dll を同じファイルの別のバージョンで上書きする必要があります。 このリリースではレジストリ エントリは変更されていないため、レジストリ エントリを変更する必要はありません。  
  
> [!WARNING]  
>  現在のバージョンのファイル (NaturalLanguage6.dll) を別のバージョンに置き換えると、そのファイルを使用するすべての言語の動作が影響を受けます。  
  
 **影響を受ける言語の一覧**  
  
|言語|省略形<br />(レジストリで<br />使用)|LCID (LCID)|  
|--------------|---------------------------------------|----------|  
|ベンガル語|ben|1093|  
|ブルガリア語|bgr|1026|  
|カタロニア語|cat|1027|  
|スペイン語|esn|3082|  
|フランス語|fra|1036|  
|グジャラート語|guj|1095|  
|ヘブライ語|heb|1037|  
|ヒンディー語|hin|1081|  
|クロアチア語|hrv|1050|  
|インドネシア語|ind|1057|  
|アイスランド語|isl|1039|  
|イタリア語|ita|1040|  
|カンナダ語|kan|1099|  
|リトアニア語|lth|1063|  
|ラトビア語|lvi|1062|  
|マラヤーラム語|mal|1100|  
|マラーティー語|mar|1102|  
|マレー語|msl|1086|  
|ニュートラル|ニュートラル|0000|  
|ノルウェー語 (ボークモール)|nor|1044|  
|パンジャーブ語|pan|1094|  
|ポルトガル語|ptg|2070|  
|ポルトガル語 (ブラジル) |ptb|1046|  
|ルーマニア語|rom|1048|  
|スロバキア語|sky|1051|  
|スロベニア語|slv|1060|  
|セルビア語 (キリル)|srb|3098|  
|セルビア語 (ラテン)|srl|2074|  
|スウェーデン語|sve|1053|  
|タミール語|tam|1097|  
|テルグ語|tel|1098|  
|ウクライナ語|ukr|1058|  
|ウルドゥ語|urd|1056|  
|ベトナム語|vit|1066|  
  
 この表は、省略形の列を基準としてアルファベット順に並べられています。  
  
###  <a name="nl6nl6revert"></a> 以前のコンポーネントに戻すには  
  
1.  上で説明した Binn フォルダーに移動します。  
  
2.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの NaturalLanguage6.dll を別の場所にバックアップします。  
  
3.  以前のバージョンの NaturalLanguage6.dll を、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のインスタンスの Binn フォルダーから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンスの Binn フォルダーにコピーします。  
  
    > [!WARNING]  
    >  この変更は、現在と以前のバージョンの両方で NaturalLanguage6.dll を使用するすべての言語に影響します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動します。  
  
###  <a name="nl6nl6restore"></a> 現在のコンポーネントを復元するには  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの NaturalLanguage6.dll をバックアップした場所に移動します。  
  
2.  現在のバージョンの NaturalLanguage6.dll を、バックアップ場所から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンスの Binn フォルダーにコピーします。  
  
    > [!WARNING]  
    >  この変更は、現在と以前のバージョンの両方で NaturalLanguage6.dll を使用するすべての言語に影響します。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動します。  
  
##  <a name="newnl6"></a> 以前のワード ブレーカーのファイル名のみが NaturalLanguage6.dll である言語  
 次の表に示す言語では、以前のワード ブレーカーのファイル名が新しいバージョンのファイル名とは異なります。 以前のファイル名は NaturalLanguage6.dll です。 以前のバージョンに戻すには、現在のバージョンの NaturalLanguage6.dll を同じファイルの以前のバージョンで上書きする必要があります。 また、以前または現在のバージョンのコンポーネントを指定するようにレジストリ エントリのセットを変更する必要があります。  
  
> [!WARNING]  
>  現在のバージョンのファイル (NaturalLanguage6.dll) を別のバージョンに置き換えると、そのファイルを使用するすべての言語の動作が影響を受けます。  
  
 **影響を受ける言語の一覧**  
  
|言語|省略形<br />(レジストリで<br />使用)|LCID (LCID)|  
|--------------|---------------------------------------|----------|  
|アラビア語|ara|1025|  
|ドイツ語|deu|1031|  
|日本語|jpn|1041|  
|オランダ語|nld|1043|  
|ロシア語|rus|1049|  
  
 この表は、省略形の列を基準としてアルファベット順に並べられています。  
  
 次の手順は、「 [ワード ブレーカーとステマーの切り替えと復元のためのファイル名とレジストリ値](#newnl6values)」に示す値の一覧と共に使用してください。  
  
###  <a name="newnl6revert"></a> 以前のコンポーネントに戻すには  
  
1.  上で説明した Binn フォルダーに移動します。  
  
2.  現在のバージョンのコンポーネントのファイルを Binn フォルダーから削除しないでください。  
  
3.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの NaturalLanguage6.dll を別の場所にバックアップします。  
  
4.  以前のバージョンの NaturalLanguage6.dll を、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のインスタンスの Binn フォルダーから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンスの Binn フォルダーにコピーします。  
  
    > [!WARNING]  
    >  この変更は、現在と以前のバージョンの両方で NaturalLanguage6.dll を使用するすべての言語に影響します。  
  
5.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** ノードに移動します。  
  
6.  次の手順に従って、選択した言語の以前のワード ブレーカー インターフェイスおよびステマー インターフェイスに対応する COM ClassID の新しいキーを追加します。  
  
    1.  以前のワード ブレーカー用に、表に示す値を持つ新しいキーを追加します。  
  
    2.  そのキー値の (既定) データを、表に示す以前のワード ブレーカーのファイル名に更新します。  
  
    3.  選択した言語でステマーを使用する場合は、以前のステマー用に、表に示す値を持つ新しいキーを追加します。  
  
    4.  選択した言語でステマーを使用する場合は、そのキー値の (既定) データを、表に示す以前のステマーのファイル名に更新します。  
  
7.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\\<language_key>** ノードに移動します。 *<language_key>* は、レジストリで使用される言語の省略形を表します。たとえば、フランス語の場合は "fra"、スペイン語の場合は "esn" です。  
  
8.  **WBreakerClass** キー値を、表に示す現在のワード ブレーカーの値に更新します。  
  
9. 選択した言語でステマーを使用する場合は、 **StemmerClass** キー値を、表に示す現在のステマーの値に更新します。  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動します。  
  
###  <a name="newnl6restore"></a> 現在のコンポーネントを復元するには  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンの NaturalLanguage6.dll をバックアップした場所に移動します。  
  
2.  現在のバージョンの NaturalLanguage6.dll を、バックアップ場所から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンスの Binn フォルダーにコピーします。  
  
    > [!WARNING]  
    >  この変更は、現在と以前のバージョンの両方で NaturalLanguage6.dll を使用するすべての言語に影響します。  
  
3.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** ノードに移動します。  
  
4.  次のキーが存在しない場合は、次の手順に従って、選択した言語の現在のワード ブレーカー インターフェイスおよびステマー インターフェイスに対応する COM ClassID の新しいキーを追加します。  
  
    1.  現在のワード ブレーカー用に、表に示す値を持つ新しいキーを追加します。  
  
    2.  そのキー値の (既定) データを、表に示す現在のワード ブレーカーのファイル名に更新します。  
  
    3.  選択した言語でステマーを使用する場合は、現在のステマー用に、表に示す値を持つ新しいキーを追加します。  
  
    4.  選択した言語でステマーを使用する場合は、そのキー値の (既定) データを、表に示す現在のステマーのファイル名に更新します。  
  
5.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\\<language_key>** ノードに移動します。 *<language_key>* は、レジストリで使用される言語の省略形を表します。たとえば、フランス語の場合は "fra"、スペイン語の場合は "esn" です。  
  
6.  **WBreakerClass** キー値を、表に示す以前のワード ブレーカーの値に更新します。  
  
7.  選択した言語でステマーを使用する場合は、 **StemmerClass** キー値を、表に示す以前のステマーの値に更新します。  
  
8.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動します。  
  
###  <a name="newnl6values"></a> ワード ブレーカーとステマーの切り替えと復元のためのファイル名とレジストリ値  
 次に示すファイル名とレジストリ エントリの一覧は、前のセクションの手順と共に使用してください。 以前のバージョンに戻す場合は以前の値を使用し、現在のバージョンのコンポーネントを復元する場合は現在の値を使用します。  
  
 次の一覧は、各言語に使用される省略形を基準としてアルファベット順に並べられています。  
  
 **アラビア語 (ara)、LCID 1025**  
  
|コンポーネント|ワード ブレーカー|ステマー|  
|---------------|------------------|-------------|  
|以前の CLSID|7EFD3C7E-9E4B-4a93-9503-DECD74C0AC6D|483B0283-25DB-4c92-9C15-A65925CB95CE|  
|以前のファイル名|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|現在の CLSID|04b37e30-c9a9-4a7d-8f20-792fc87ddf71|[InclusionThresholdSetting]|  
|現在のファイル名|MSWB7.dll|[InclusionThresholdSetting]|  
  
 **ドイツ語 (deu)、LCID 1031**  
  
|コンポーネント|ワード ブレーカー|ステマー|  
|---------------|------------------|-------------|  
|以前の CLSID|45EACA36-DBE9-4e4a-A26D-5C201902346D|65170AE4-0AD2-4fa5-B3BA-7CD73E2DA825|  
|以前のファイル名|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|現在の CLSID|dfa00c33-bf19-482e-a791-3c785b0149b4|8a474d89-6e2f-419c-8dd5-9b50edc8c787|  
|現在のファイル名|MSWB7.dll|MSWB7.dll|  
  
 **日本語 (jpn)、LCID 1041**  
  
|コンポーネント|ワード ブレーカー|ステマー|  
|---------------|------------------|-------------|  
|以前の CLSID|E1E8F15E-8BEC-45df-83BF-50FF84D0CAB5|3D5DF14F-649F-4cbc-853D-F18FEDE9CF5D|  
|以前のファイル名|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|現在の CLSID|04096682-6ece-4e9e-90c1-52d81f0422ed|[InclusionThresholdSetting]|  
|現在のファイル名|MsWb70011.dll|[InclusionThresholdSetting]|  
  
 **オランダ語 (nld)、LCID 1043**  
  
|コンポーネント|ワード ブレーカー|ステマー|  
|---------------|------------------|-------------|  
|以前の CLSID|2C9F6BEB-C5B0-42b6-A5EE-84C24DC0D8EF|F7A465EE-13FB-409a-B878-195B420433AF|  
|以前のファイル名|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|現在の CLSID|69483c30-a9af-4552-8f84-a0796ad5285b|CF923CB5-1187-43ab-B053-3E44BED65FFA|  
|現在のファイル名|MSWB7.dll|MSWB7.dll|  
  
 **ロシア語 (rus)、LCID 1049**  
  
|コンポーネント|ワード ブレーカー|ステマー|  
|---------------|------------------|-------------|  
|以前の CLSID|2CB6CDA4-1C14-4392-A8EC-81EEF1F2E079|E06A0DDD-E81A-4e93-8A8D-F386C3A1B670|  
|以前のファイル名|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|現在の CLSID|aaa3d3bd-6de7-4317-91a0-d25e7d3babc3|d42c8b70-adeb-4b81-a52f-c09f24f77dfa|  
|現在のファイル名|MSWB7.dll|MSWB7.dll|  
  
##  <a name="newnew"></a> 以前と現在のファイル名がどちらも NaturalLanguage6.dll でない言語  
 次の表に示す言語では、以前のワード ブレーカーとステマーのファイル名が新しいバージョンのファイル名とは異なります。 以前と現在のファイル名はどちらも NaturalLanguage6.dll ではありません。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のセットアップでは、現在と以前の両方のバージョンのコンポーネントを Binn フォルダーにコピーするため、ファイルを置き換える必要はありません。 ただし、以前または現在のバージョンのコンポーネントを指定するようにレジストリ エントリのセットを変更する必要があります。  
  
 **影響を受ける言語の一覧**  
  
|言語|省略形<br />(レジストリで<br />使用)|LCID (LCID)|  
|--------------|---------------------------------------|----------|  
|Simplified Chinese|chs|2052|  
|繁体字中国語|cht|1028|  
|タイ語|tha|1054|  
|繁体字中国語|zh-hk|3076|  
|繁体字中国語|zh-mo|5124|  
|簡体中国語|zh-sg|4100|  
  
 この表は、省略形の列を基準としてアルファベット順に並べられています。  
  
 次の手順は、「 [ワード ブレーカーとステマーの切り替えと復元のためのファイル名とレジストリ値](#newnewvalues)」に示す値の一覧と共に使用してください。  
  
###  <a name="newnewrevert"></a> 以前のコンポーネントに戻すには  
  
1.  現在のバージョンのコンポーネントのファイルを Binn フォルダーから削除しないでください。  
  
2.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** ノードに移動します。  
  
3.  次の手順に従って、選択した言語の以前のワード ブレーカー インターフェイスおよびステマー インターフェイスに対応する COM ClassID の新しいキーを追加します。  
  
    1.  以前のワード ブレーカー用に、表に示す値を持つ新しいキーを追加します。  
  
    2.  そのキー値の (既定) データを、表に示す以前のワード ブレーカーのファイル名に更新します。  
  
    3.  選択した言語でステマーを使用する場合は、以前のステマー用に、表に示す値を持つ新しいキーを追加します。  
  
    4.  選択した言語でステマーを使用する場合は、そのキー値の (既定) データを、表に示す以前のステマーのファイル名に更新します。  
  
4.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\\<language_key>** ノードに移動します。 *<language_key>* は、レジストリで使用される言語の省略形を表します。たとえば、フランス語の場合は "fra"、スペイン語の場合は "esn" です。  
  
5.  **WBreakerClass** キー値を、表に示す現在のワード ブレーカーの値に更新します。  
  
6.  選択した言語でステマーを使用する場合は、 **StemmerClass** キー値を、表に示す現在のステマーの値に更新します。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動します。  
  
###  <a name="newnewrestore"></a> 以前のコンポーネントを復元するには  
  
1.  以前のバージョンのコンポーネントのファイルを Binn フォルダーから削除しないでください。  
  
2.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** ノードに移動します。  
  
3.  次のキーが存在しない場合は、次の手順に従って、選択した言語の現在のワード ブレーカー インターフェイスおよびステマー インターフェイスに対応する COM ClassID の新しいキーを追加します。  
  
    1.  現在のワード ブレーカー用に、表に示す値を持つ新しいキーを追加します。  
  
    2.  そのキー値の (既定) データを、表に示す現在のワード ブレーカーのファイル名に更新します。  
  
    3.  選択した言語でステマーを使用する場合は、現在のステマー用に、表に示す値を持つ新しいキーを追加します。  
  
    4.  選択した言語でステマーを使用する場合は、そのキー値の (既定) データを、表に示す現在のステマーのファイル名に更新します。  
  
4.  レジストリで、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\\<language_key>** ノードに移動します。 *<language_key>* は、レジストリで使用される言語の省略形を表します。たとえば、フランス語の場合は "fra"、スペイン語の場合は "esn" です。  
  
5.  **WBreakerClass** キー値を、表に示す以前のワード ブレーカーの値に更新します。  
  
6.  選択した言語でステマーを使用する場合は、 **StemmerClass** キー値を、表に示す以前のステマーの値に更新します。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動します。  
  
###  <a name="newnewvalues"></a> ワード ブレーカーとステマーの切り替えと復元のためのファイル名とレジストリ値  
 次に示すファイル名とレジストリ エントリの一覧は、前のセクションの手順と共に使用してください。 以前のバージョンに戻す場合は以前の値を使用し、現在のバージョンのコンポーネントを復元する場合は現在の値を使用します。  
  
 次の一覧は、各言語に使用される省略形を基準としてアルファベット順に並べられています。  
  
 **簡体中国語 (chs)、LCID 2052**  
  
|コンポーネント|ワード ブレーカー|  
|---------------|------------------|  
|以前の CLSID|12CE94A0-DEFB-11D2-B31D-00600893A857|  
|以前のファイル名|chsbrkr.dll|  
|現在の CLSID|E0831C90-BAB0-4ca5-B9BD-EA254B538DAC|  
|現在のファイル名|MsWb70804.dll|  
  
 **繁体字中国語 (cht)、LCID 1028**  
  
|コンポーネント|ワード ブレーカー|  
|---------------|------------------|  
|以前の CLSID|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|以前のファイル名|chtbrkr.dll|  
|現在の CLSID|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|現在のファイル名|MsWb70404.dll|  
  
 **タイ語 (tha)、LCID 1054**  
  
|コンポーネント|ワード ブレーカー|ステマー|  
|---------------|------------------|-------------|  
|以前の CLSID|CCA22CF4-59FE-11D1-BBFF-00C04FB97FDA|CEDC01C7-59FE-11D1-BBFF-00C04FB97FDA|  
|以前のファイル名|Thawbrkr.dll|Thawbrkr.dll|  
|現在の CLSID|F70C0935-6E9F-4ef1-9F06-7876536DB900|[InclusionThresholdSetting]|  
|現在のファイル名|MsWb7001e.dll|[InclusionThresholdSetting]|  
  
 **繁体字中国語 (zh-hk)、LCID 3076**  
  
|コンポーネント|ワード ブレーカー|  
|---------------|------------------|  
|以前の CLSID|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|以前のファイル名|chtbrkr.dll|  
|現在の CLSID|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|現在のファイル名|MsWb70404.dll|  
  
 **繁体字中国語 (zh-mo)、LCID 5124**  
  
|コンポーネント|ワード ブレーカー|  
|---------------|------------------|  
|以前の CLSID|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|以前のファイル名|chtbrkr.dll|  
|現在の CLSID|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|現在のファイル名|MsWb70404.dll|  
  
 **簡体中国語 (zh-sg)、LCID 4100**  
  
|コンポーネント|ワード ブレーカー|  
|---------------|------------------|  
|以前の CLSID|12CE94A0-DEFB-11D2-B31D-00600893A857|  
|以前のファイル名|chsbrkr.dll|  
|現在の CLSID|E0831C90-BAB0-4ca5-B9BD-EA254B538DAC|  
|現在のファイル名|MsWb70804.dll|  
  
## <a name="see-also"></a>参照  
 [Change the Word Breaker Used for US English and UK English](change-the-word-breaker-used-for-us-english-and-uk-english.md)   
 [フルテキスト検索の動作の変更](../../database-engine/behavior-changes-to-full-text-search.md)  
  
  
