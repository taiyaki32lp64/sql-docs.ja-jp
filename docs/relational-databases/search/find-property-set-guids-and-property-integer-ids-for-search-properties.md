---
title: 検索プロパティのプロパティ セット GUID およびプロパティ整数 ID の検索
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 3b950557c3c5c22968cffa4be0b4565ddedb293c
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056517"
---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>検索プロパティのプロパティ セット GUID およびプロパティ整数 ID の取得
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、プロパティを検索プロパティ リストに追加してフルテキスト検索で検索できるようにするために事前に必要な値を取得する方法について説明します。 これらの値には、ドキュメント プロパティのプロパティ セット GUID およびプロパティ整数識別子が含まれます。  
  
 バイナリ データ (**varbinary**、**varbinary(max)** (**FILESTREAM** を含む)、または **image** データ型の列に格納されたデータ) から IFilter で抽出されたドキュメント プロパティは、フルテキスト検索で使用できます。 抽出されたプロパティを検索できるようにするには、検索プロパティ リストにプロパティを手動で追加する必要があります。 さらに、検索プロパティ リストを 1 つ以上のフルテキスト インデックスに関連付ける必要があります。 詳細については、「 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。  
  
 使用可能なプロパティをプロパティ リストに追加する前に、プロパティに関する以下の 2 つの情報を入手する必要があります。  
  
-   プロパティのプロパティ セット GUID  
  
-   プロパティの整数 ID  
  
 プロパティ リストにプロパティを追加するとき、名前と説明も指定する必要があります。 ただし、プロパティの正規の名前と説明を使用する必要はありません。  
  
 このトピックでは、使用可能なプロパティ (特にマイクロソフトによって定義されているプロパティ) に関する情報を取得するための一般的な方法について説明します。 サード パーティによって定義されているプロパティについては、サード パーティのドキュメントを参照するか、ベンダーに問い合わせてください。  
  
##  <a name="wellknown"></a> 広く使用され、知られている Microsoft プロパティについての情報の入手  
 マイクロソフトでは、さまざまなコンテキストで使用できる何百ものドキュメント プロパティを定義していますが、それぞれのファイル形式で使用できるプロパティはごくわずかです。 頻繁に使用される Windows プロパティの中に、少数の汎用プロパティがあります。 よく知られている汎用プロパティの一部の例を次の表に示します。 この表では、よく知られている名前、Windows の正規名 (マイクロソフトが公開するプロパティの説明で使用)、プロパティ セット GUID、プロパティ整数識別子、および簡単な説明を示します。  
  
|よく知られている名前|Windows の正規名|プロパティ セット GUID|整数 ID|[説明]|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Authors|**System.Author**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|特定のアイテムの作成者。|  
|Tags|**System.Keywords**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|アイテムに割り当てられる一連のキーワード (タグとも呼ばれます)。|  
|型|**System.PerceivedType**|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|正規の種類に基づいて認識されるファイルの種類。|  
|[タイトル]|**System.Title**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|アイテムのタイトル。 たとえば、ドキュメントのタイトル、メッセージの件名、写真のキャプション、または音楽トラックの名前。|  
  
 ファイル形式間で一貫性を保持するため、マイクロソフトでは、頻繁に使用される、優先度の高いドキュメントのプロパティのサブセットを、いくつかのドキュメントのカテゴリとして特定しています。 これらには、通信、連絡先、ドキュメント、音楽ファイル、画像、およびビデオがあります。 各カテゴリの上位のプロパティの詳細については、Windows サーチに関するドキュメントの「 [カスタム ファイル形式のシステム定義プロパティ](https://go.microsoft.com/fwlink/?LinkId=144336) 」を参照してください。  
  
 特定のファイル形式では、以下の 3 種類のプロパティが実装される場合があります。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]によって定義された汎用プロパティ  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]によって定義された、カテゴリに固有のプロパティ  
  
-   ソフトウェア ベンダーによって定義された、アプリケーション固有のカスタム プロパティ  
  
##  <a name="filtdump"></a> FILTDUMP.EXE による使用可能なプロパティについての情報の取得  
 インストールされた IFilter で検出および抽出されるプロパティを調べるには、 **Windows SDK に含まれている** filtdump.exe [!INCLUDE[msCoName](../../includes/msconame-md.md)] ユーティリティをインストールして実行してください。  
  
 **filtdump.exe** はコマンド プロンプトから実行し、1 つの引数を指定します。 この引数は、インストールした IFilter が対象とする種類のファイルの個別の名前です。 このユーティリティは、IFilter で検出された、ドキュメント内のすべてのプロパティと、そのプロパティ セット GUID、整数 ID、および追加情報の一覧を表示します。  
  
 このソフトウェアをインストールする方法の詳細については、「 [Windows 7 および .NET Framework 4 用 Microsoft Windows SDK](https://www.microsoft.com/download/details.aspx?id=8279)」を参照してください。 SDK をダウンロードしてインストールした後、以下のフォルダーで filtdump.exe ユーティリティを見つけてください。  
  
-   64 ビット バージョンの場合は、 `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`にあります。  
  
-   32 ビット バージョンの場合は、 `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`にあります。  
  
##  <a name="propdesc"></a> Windows プロパティの説明からの検索プロパティの値の入手  
 よく知られた Windows 検索プロパティについては、プロパティの説明 ( **propertyDescription** ) の **formatID** 属性および**propID**属性から必要な情報を入手できます。  
  
 次の例では、一般的なマイクロソフト プロパティの関連する部分 (この例では、 `System.Author` ) を示します。 `formatID` 属性はプロパティ セット GUID の `F29F85E0-4FF9-1068-AB91-08002B27B3D9`を指定し、 `propID` 属性は、プロパティの整数 ID `4.` を指定します。 `name` 属性は、Windows の正規のプロパティ名である `System.Author`を示すことに注意してください (この例では、関係のない列プロパティ説明部分を省略しています)。  
  
```  
.  
propertyDescription  
name = System.Author  
...  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
...  
```  
  
 このプロパティの完全な説明については、Windows サーチに関するドキュメントの「 [System.Author](https://go.microsoft.com/fwlink/?LinkId=144337) 」を参照してください。  
  
 Windows プロパティの完全な一覧については、Windows サーチに関するドキュメントの「 [Windows プロパティ](https://go.microsoft.com/fwlink/?LinkId=215013)」を参照してください。  
  
##  <a name="examples"></a> 検索プロパティ リストへのプロパティの追加  
 次の例では、プロパティを検索プロパティ リストに追加する方法を示します。 この例では、 [ALTER SEARCH PROPERTY LIST](../../t-sql/statements/alter-search-property-list-transact-sql.md) ステートメントを使用して、 `System.Author` プロパティを `PropertyList1`という名前の検索プロパティ リストに追加し、 `Author`という表示名を指定します。  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 検索プロパティ リストを作成し、フルテキスト インデックスに関連付ける方法については、「 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [検索用フィルターの構成と管理](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
