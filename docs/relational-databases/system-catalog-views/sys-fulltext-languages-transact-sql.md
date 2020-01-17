---
title: fulltext_languages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e5af224150508f048d91345cba595517209f824d
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981777"
---
# <a name="sysfulltext_languages-transact-sql"></a>fulltext_languages (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  このカタログビューには、ワードブレーカーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に登録されている言語ごとに1行が含まれています。 各行には、言語の LCID と名前が表示されます。 言語のワードブレーカーが登録されている場合、その他の言語リソース (ステミング機能、ノイズワード (ストップワード)、および類義語辞典ファイル) は、フルテキストインデックス作成またはクエリ操作で使用できるようになります。 **名前**または**lcid**の値は、フルテキストクエリとフルテキストインデックスの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで指定できます。  
   
|列|データ型|[説明]|  
|------------|---------------|-----------------|  
|**lcid**|**int**|言語の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ロケール識別子 (LCID) です。|  
|**name**|**sysname**|**Lcid**の値に対応する[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)のエイリアスの値か、または数値の lcid の文字列表現です。|  
  
## <a name="values-returned-for-default-languages"></a>既定の言語の戻り値  
 次の表に、ワード ブレーカーが既定で登録されている言語の値を示します。  
  
|言語|LCID (LCID)|  
|--------------|----------|  
|アラビア語|1025|  
|ベンガル語 (インド)|1093|  
|英語 (U.K.)|2057|  
|ブルガリア語|1026|  
|カタロニア語|1027|  
|中国語 (中華人民共和国香港特別行政区)|3076|  
|中国語 (中華人民共和国マカオ特別行政区)|5124|  
|中国語 (シンガポール)|4100|  
|クロアチア語|1050|  
|チェコ語|1029|  
|デンマーク語|1030|  
|オランダ語|1043|  
|英語|1033|  
|フランス語|1036|  
|ドイツ語|1031|  
|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> ギリシャ語|1032|  
|グジャラート語|1095|  
|ヘブライ語|1037|  
|ヒンディー語|1081|  
|アイスランド語|1039|  
|インドネシア語|1057|  
|イタリア語|1040|  
|日本語|1041|  
|カンナダ語|1099|  
|韓国語|1042|  
|ラトビア語|1062|  
|リトアニア語|1063|  
|マレー語 - マレーシア|1086|  
|マラヤーラム語|1100|  
|マラーティー語|1102|  
|ニュートラル|0|  
|ノルウェー語 (ブークモール)|1044|  
|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> ポーランド語|1045|  
|ポルトガル語 (ブラジル)|1046|  
|ポルトガル語 (ポルトガル)|2070|  
|パンジャーブ語|1094|  
|ルーマニア語|1048|  
|ロシア語|1049|  
|セルビア語 (キリル)|3098|  
|セルビア語 (ラテン)|2074|  
|Simplified Chinese|2052|  
|スロバキア語|1051|  
|スロベニア語|1060|  
|スペイン語|3082|  
|スウェーデン語|1053|  
|タミール語|1097|  
|テルグ語|1098|  
|タイ語|1054|  
|繁体字中国語|1028|  
|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> トルコ語|1055|  
|ウクライナ語|1058|  
|ウルドゥ語|1056|  
|ベトナム語|1066|  
  
## <a name="remarks"></a>Remarks  
 フルテキスト検索に登録されている言語の一覧を更新するには、 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**' を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>参照  
 [transact-sql &#40;  の&#41; sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [検索用のワード ブレーカーとステミング機能の構成と管理](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [フルテキスト検索のための類義語辞典ファイルの構成と管理](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
