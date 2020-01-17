---
title: 手順 2:フラット ファイル接続マネージャーの追加と構成 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a412235a3eaeb18f32e820460b82ab238c7c0e8
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296116"
---
# <a name="lesson-1-2-add-and-configure-a-flat-file-connection-manager"></a>レッスン 1-2:フラット ファイル接続マネージャーの追加と構成

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



この実習では、先ほど作成したパッケージにフラット ファイル接続マネージャーを追加します。 パッケージにフラット ファイル接続マネージャーを追加すると、フラット ファイルからデータを抽出できるようになります。 フラット ファイル接続マネージャーでは、フラット ファイルからデータを抽出するときに適用するファイルの名前と場所、ロケールとコード ページ、およびファイル形式を指定できます。また、列区切り記号も指定できます。 さらに、各列のデータ型を手動で指定できます。 **[列の型の予測]** ダイアログ ボックスを使用して、抽出したデータの列を [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] データ型に自動的にマップすることもできます。  
  
通常は、操作する各フラット ファイルについて、新しいファイル インポート マネージャーを作成する必要があります。 ただし、このチュートリアルでは、データ形式がまったく同じである複数のフラット ファイルからデータを抽出するので、フラット ファイル接続マネージャーを 1 つだけサンプル パッケージに追加して、構成します。  
  
このレッスンでは、フラット ファイル接続マネージャーで次のプロパティを構成します。  
  
-   **列名:** フラット ファイルには列名がないため、フラット ファイル接続マネージャーによって既定の列名が作成されます。 これらの既定の列名は、各列の内容を明確に表していません。 フラット ファイル データの読み込み先であるファクト テーブルと一致する名前に既定の名前を変更します。  
  
-   **データのマッピング:** フラット ファイル接続マネージャーのデータ型マッピングを指定します。このマッピングは、その接続マネージャーを参照するすべてのフラット ファイル データ ソース コンポーネントで使用されます。 フラット ファイル接続マネージャーでは、データ型を手動でマップできます。また、 **[列の型の予測]** ダイアログ ボックスを使用してマップすることもできます。 この実習では、 **[列の型の予測]** ダイアログ ボックスで予測されたマッピングを表示し、 **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで必要なマッピングを手動で行います。  
  
> [!NOTE]
> フラット ファイル接続マネージャーでは、データ ファイルに関するロケール情報が提供されます。 コンピューターが、地域オプション **[英語 (米国)]** を使用するように構成されていない場合、 **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで追加のプロパティを設定する必要があります。  
  
## <a name="add-a-flat-file-connection-manager-to-the-ssis-package"></a>SSIS パッケージにフラット ファイル接続マネージャーを追加する  
  
1.  **[ソリューション エクスプローラー]** ウィンドウで **[接続マネージャー]** を右クリックし、 **[新しい接続マネージャー]** を選択します。
1. **[SSIS 接続マネージャーの追加]** ダイアログで **[FLATFILE]** 、 **[追加]** の順に選択します。
  
2.  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[接続マネージャー名]** に「**Sample Flat File Source Data**」と入力します。  
  
3.  **[参照]** を選択します。  
  
4.  **[ファイルを開く]** ダイアログ ボックスで、コンピューター上の **SampleCurrencyData.txt** ファイルを指定します。  
  
5.  [先頭データ行を列名として使用する] チェック ボックスをオフにします。  
  
### <a name="set-locale-sensitive-properties"></a>ロケール依存型プロパティを設定する  
  
1.  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[全般]** を選択します。  
  
2.  **[ロケール]** を **[英語 (米国)]** に、 **[コード ページ]** を **[1252]** に設定します。  
  
### <a name="rename-columns-in-the-flat-file-connection-manager"></a>フラット ファイル接続マネージャーで列名を変更する  
  
1.  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[詳細]** を選択します。  
  
2.  プロパティ ペインで、次のように変更します。  
  
    -   **[列 0]** の Name プロパティを「 **AverageRate**」に変更します。  
  
    -   **[列 1]** の Name プロパティを「 **CurrencyID**」に変更します。  
  
    -   **[列 2]** の Name プロパティを「 **CurrencyDate**」に変更します。  
  
    -   **[列 3]** の Name プロパティを「 **EndOfDayRate**」に変更します。  
  
### <a name="remap-column-data-types"></a>列のデータ型を再マップする  
  
既定では、4 つのすべての列が文字列データ型 [DT_STR] に設定され、 **OutputColumnWidth** は 50 に設定されます。  

1.  **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[型の推測]** を選択します。  
  
    [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] は、最初の 200 行分のデータに基づいて適切なデータ型を自動的に予測します。 この推測オプションを変更して、サンプルの行数を変更したり、整数またはブール データの既定のデータ型を指定したり、文字列の列の余白としてスペースを挿入することもできます。  
  
    ここでは **[列の型の予測]** ダイアログ ボックスのオプションを変更せずに、 **[OK]** を選択して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] に列のデータ型を予測させます。 このアクションにより、 **[フラット ファイル接続マネージャー エディター]** ダイアログ ボックスの **[詳細設定]** ペインに戻ります。このペインでは、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によって予測された列のデータ型を確認できます あるいは、 **[キャンセル]** を選択すると、列のメタデータの予測は行われず、既定の文字列データ型 (DT_STR) が使用されます。  
  
    このチュートリアルでは、SampleCurrencyData.txt ファイルのデータに対応するデータ型を [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] が推測します。推測されたデータ型は、下表の 2 列目に示されています。 4 番目の列には、後続の手順で定義される、変換先の列に必要なデータ型が含まれます。  
  
    |フラット ファイルの列|推測されたデータ型|変換先列|変換先の型|  
    |--------------------|------------------|----------------------|--------------------|  
    |AverageRate|float [DT_R4]|FactCurrencyRate.AverageRate|FLOAT|  
    |CurrencyID|string [DT_STR]|DimCurrency,CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|date|  
    |EndOfDayRate|float [DT_R4]|FactCurrencyRate.EndOfDayRate|FLOAT|  
  
    **CurrencyID** 列で推測されたデータ型は、変換先テーブルのフィールドのデータ型と互換性がありません。 `DimCurrency.CurrencyAlternateKey` のデータ型は nchar(3) なので、**CurrencyID** のデータ型を文字列 [DT_STR] から Unicode 文字列 [DT_WSTR] に変更する必要があります。 また、フィールド `DimDate.FullDateAlternateKey` は date データ型として定義されるため、**CurrencyDate** の型は、date [DT_Date] から database date [DT_DBDATE] に変更する必要があります。  
  
2.  一覧の **CurrencyID** 列を選択し、[プロパティ] ペインで **CurrencyID** 列のデータ型を string [DT_STR] から Unicode string [DT_WSTR] に変更します。  
  
3.  [プロパティ] ペインで、 **CurrencyDate** 列のデータ型を date [DT_DATE] から database date [DT_DBDATE] に変更します。  
  
4.  **[OK]** を選択します。  
  
## <a name="go-to-next-task"></a>次の実習に進む
[手順 3:OLE DB 接続マネージャーを追加し、構成する](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>参照  
[フラット ファイル接続マネージャー](../integration-services/connection-manager/flat-file-connection-manager.md)  
[Integration Services のデータ型](../integration-services/data-flow/integration-services-data-types.md)  
  
  
  
