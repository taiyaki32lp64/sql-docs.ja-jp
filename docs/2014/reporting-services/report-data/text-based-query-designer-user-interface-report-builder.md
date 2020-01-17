---
title: テキストベースのクエリ デザイナーのユーザー インターフェイス (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
helpviewer_keywords:
- query designers, text-based
ms.assetid: 89fddca5-bd96-4128-9072-5348d1b6e02c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a71c1781432ee4ca35c72beb8b091380f2e72513
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891874"
---
# <a name="text-based-query-designer-user-interface-report-builder"></a>テキストベースのクエリ デザイナーのユーザー インターフェイス (レポート ビルダー)
  デザイン時に、データ ソースでサポートされているクエリ言語でクエリを指定し、クエリを実行し、結果を表示するには、テキスト ベースのクエリ デザイナーを使用します。 複数の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメント、カスタム データ処理拡張機能のクエリまたはコマンド構文、および式としてのクエリを指定できます。 テキスト ベースのクエリ デザイナーはクエリを前処理せず、あらゆる種類のクエリ構文に対応できるため、これは多くの種類のデータ ソースで既定のクエリ デザイナー ツールになっています。  
  
> [!IMPORTANT]  
>  ユーザーは、クエリを作成して実行する際にデータ ソースにアクセスします。 したがって、データ ソースに対する最小限の権限 (読み取り専用権限など) を付与する必要があります。  
  
 テキスト ベースのクエリ デザイナーでは、ツール バーと次の 2 つのペインが表示されます。  
  
-   **[クエリ]** クエリの種類に応じて、クエリ テキスト、テーブル名、またはストアド プロシージャ名が表示されます。 すべての種類のデータ ソースですべての種類のクエリが使用できるとは限りません。 たとえば、テーブル名はデータ ソースの種類が OLE DB の場合にのみサポートされます。  
  
-   **[結果]** デザイン時にクエリの実行結果が表示されます。  
  
## <a name="text-based-query-designer-toolbar"></a>テキスト ベースのクエリ デザイナーのツール バー  
 テキスト ベースのクエリ デザイナーで使用できるツール バーは、コマンドの種類に関係なく 1 つだけです。 次の表は、ツール バーの各ボタンとその機能を示しています。  
  
|ボタン|説明|  
|------------|-----------------|  
|**[テキストとして編集]**|テキスト ベースのクエリ デザイナーと、グラフィカル クエリ デザイナー間で切り替えます。 すべての種類のデータ ソースでグラフィカル クエリ デザイナーがサポートされているとは限りません。|  
|**[インポート]**|ファイルまたはレポートから既存のクエリをインポートします。 サポートされているファイルの種類は sql と rdl だけです。|  
|![クエリを実行する](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "クエリを実行する")|クエリを実行し、その結果セットを結果ペインに表示します。|  
|**[コマンドの種類]**|**[Text]** 、 **[StoredProcedure]** 、または **[TableDirect]** を選択します。 パラメーターを受け取るストアド プロシージャの場合、ツール バーの **[実行]** をクリックすると、 **[クエリ パラメーターの定義]** ダイアログ ボックスが表示され、必要な値を入力できます。<br /><br /> 注:ストアド プロシージャから複数の結果セットが返された場合、最初の結果セットのみを使ってデータセットが設定されます。|  
  
### <a name="command-type-text"></a>コマンドの種類 (Text)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データセットを作成するとき、既定ではリレーショナル クエリ デザイナーが表示されます。 テキスト ベースのクエリ デザイナーに切り替えるには、ツール バーの **[テキストとして編集]** 切り替えボタンをクリックします。 テキスト ベースのクエリ デザイナーは、クエリ ペインと結果ペインの 2 つのペインで構成されています。 次の図に各ペインの名称を示します。  
  
 ![リレーショナル データのクエリに使用する汎用クエリ デザイナー](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsaw-sql-generic.gif "リレーショナル データのクエリに使用する汎用クエリ デザイナー")  
  
 次の表に各ペインの機能を示します。  
  
|ペイン|機能|  
|----------|--------------|  
|Query|[!INCLUDE[tsql](../../../includes/tsql-md.md)] クエリ テキストを表示します。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] クエリを記述または編集する際に、このペインを使用します。|  
|結果|クエリの結果を表示します。 クエリを実行するには、任意のペインで右クリックして、 **[実行]** をクリックするか、ツール バーの **[実行]** ボタンをクリックします。|  
  
#### <a name="example"></a>例  
 次の[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]クエリは、 `Person`スキーマの**2008**データベース`ContactType`テーブルから姓の一覧を返します。  
  
```  
SELECT Name FROM Person.ContactType  
```  
  
 ツール バーの **[実行]** をクリックすると、 **クエリ** ペインのコマンドが実行され、その結果が **結果** ペインに表示されます。 結果セットには、所有者や販売担当者など 20 種類の連絡先の一覧が表示されます。  
  
### <a name="command-type-storedprocedure"></a>コマンドの種類 (StoredProcedure)  
 **[コマンドの種類] で [StoredProcedure]** を選択した場合、テキスト ベースのクエリ デザイナーには、クエリ ペインと結果ペインの 2 つのペインが表示されます。 ストアド プロシージャ名をクエリ ペインに入力し、ツール バーの **[実行]** をクリックします。 ストアド プロシージャでパラメーターを使用する場合、 **[クエリ パラメーターの定義]** ダイアログ ボックスが表示されます。 ストアド プロシージャのパラメーター値を入力します。 すべてのストアド プロシージャの入力パラメーターについて、レポート パラメーターが作成されます。  
  
 次の図に、ストアド プロシージャを実行したときのクエリ ペインと結果ペインを示します。 この場合、入力パラメーターは定数です。  
  
 ![テキスト ベースのクエリ デザイナーのストアド プロシージャ](https://docs.microsoft.com/analysis-services/analysis-services/media/rs-relational-text-sp.gif "テキスト ベースのクエリ デザイナーのストアド プロシージャ")  
  
 次の表に各ペインの機能を示します。  
  
|ペイン|機能|  
|----------|--------------|  
|[クエリ]|ストアド プロシージャの名前と入力パラメーターを表示します。|  
|[結果]|クエリの結果を表示します。 クエリを実行するには、任意のペインで右クリックして、 **[実行]** をクリックするか、ツール バーの **[実行]** ボタンをクリックします。|  
  
#### <a name="example"></a>例  
 次のクエリは、 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] **2008**ストアドプロシージャ`uspGetWhereUsedProductID`を呼び出します。 クエリを実行する場合は、製品 ID 番号パラメーターの値を入力する必要があります。  
  
```  
uspGetWhereUsedProductID  
```  
  
 **[実行]** ( **!** ) ボタンをクリックします。 クエリ パラメーターの入力画面が表示されたら、次の表にある値を入力します。  
  
|||  
|-|-|  
|*@StartProductID*|820|  
|*@CheckDate*|20010115|  
  
 指定した日付について、結果セットには、指定したコンポーネント番号を使用している 13 の製品 ID の一覧が表示されます。  
  
### <a name="command-type-tabledirect"></a>コマンドの種類 (TableDirect)  
 **[コマンドの種類] で [TableDirect]** を選択した場合、テキスト ベースのクエリ デザイナーには、クエリ ペインと結果ペインの 2 つのペインが表示されます。 テーブルを入力し、 **[実行]** ボタンをクリックすると、そのテーブルのすべての列が返されます。  
  
#### <a name="example"></a>例  
 データソースの種類が OLE DB の場合、次のデータセットクエリでは、 **2008**データベースのすべて[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]の種類の連絡先について結果セットが返されます。  
  
 `Person.ContactType`  
  
 テーブル名 Person.ContactType を入力した場合、これは [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントの `SELECT * FROM Person.ContactType`を作成することに相当します。  
  
## <a name="see-also"></a>関連項目  
 [リレーショナル クエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](relational-query-designer-user-interface-report-builder.md)   
 [クエリ デザイナー &#40;レポート ビルダー&#41;](../query-designers-report-builder.md)  
  
  
