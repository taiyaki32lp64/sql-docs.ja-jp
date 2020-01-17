---
title: 列マッピング (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a16e270acae2a2685bcaf53045883eaa078ab03d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285931"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>[列マッピング]\(SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  指定したクエリをコピーまたは確認する既存のテーブルやビューを選択した後、 **[マッピングの編集]** をクリックすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインポートおよびエクスポート ウィザードに **[列マッピング]** ダイアログ ボックスが表示されます。 このページでは、コピー元の列からコピーしたデータを受け取るためのコピー先列を指定し、構成します。 多くの場合、このページでは何も変更する必要はありません。
  
選択したテーブル内のすべての列をコピーしない場合、このページでできることは、不要な列を除外することだけです。 コピーしない列については、 **[マッピング]** リストの **[変換先]** 列で **[無視]** を選択します。
 
## <a name="screen-shot-of-the-column-mappings-page"></a>[列マッピング] ページのスクリーン ショット 
 次のスクリーン ショットは、ウィザードの **[列マッピング]** ダイアログ ボックスの例を示しています。 
 
 この例では、 **[変換先テーブルを作成する]** が選択されているので、ウィザードで新しい変換先テーブルを作成しようとしているのがわかります。 既定では、ウィザードが新しい変換先テーブル内の各列の名前、データ型、およびプロパティを、対応するソース列と同じにします。 
  
 ![インポートおよびエクスポート ウィザードの [列マッピング] ページ](../../integration-services/import-export-data/media/column-mappings.png "インポートおよびエクスポート ウィザードの [列マッピング] ページ")  
  
## <a name="review-the-source-and-destination"></a>変換元と変換先のテーブルの確認 
![[列マッピング] ページ、変換元と変換先のセクション](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **ソース**  
 選択した変換元のテーブル、ビュー、またはクエリ。  
  
 **変換先**  
 選択した変換先のテーブルまたはビュー。  

## <a name="optionally-create-a-new-destination-table"></a>必要に応じて、新しい変換先テーブルを作成する
![[列マッピング] ページ、新しいテーブル セクション](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **変換先テーブル/ファイルの作成**  
 変換先テーブルが存在しない場合、変換先テーブルを作成します。    
  
 **SQL の編集**  
**[SQL の編集]** をクリックすると、 **[テーブル作成 SQL ステートメント]** ダイアログ ボックスが開きます。 自動生成された CREATE TABLE ステートメントを使用することもできますし、目的に応じてステートメントを変更することもできます。 このステートメントを手動で変更する場合は、変更内容が列マッピングの一覧に反映されていることを確認する必要があります。 詳細については、「 [[テーブル作成 SQL ステートメント] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)」を参照してください。  

### <a name="sometimes-these-options-are-disabled"></a>これらのオプションが無効になっている場合がある
**[変換先テーブル/ファイルの作成]** オプションと **[SQL の編集]** ボタンは、自動的に有効または自動的に無効になります。

-   **有効。** **[コピー元のテーブルおよびビューを選択]** ページで**新しい**変換先テーブルを指定した場合は、 **[変換先テーブルの作成]** オプションが自動的に選択され、 **[SQL の編集]** ボタンが有効になります。

-   **無効。** **[コピー元のテーブルおよびビューを選択]** ページで**既存の**変換先テーブルを選択した場合は、 **[変換先テーブルの作成]** オプションと **[SQL の編集]** ボタンが無効になります。 新しい変換先テーブルを作成する場合は、 **[コピー元のテーブルおよびビューを選択]** ページに戻り、 **[変換先]** 列に**新しい**テーブルの名前を入力します。  

## <a name="what-about-existing-data-in-the-destination"></a>変換先の既存のデータについて
![[列マッピング] ページ、オプション セクション](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **変換先テーブル/ファイル内の行を削除する**  
 新しいデータを読み込む前に、既存のテーブルからデータを削除するかどうかを指定します。  
  
 **変換先テーブル/ファイルに行を追加する**  
 既存のテーブルに存在するデータに、新しいデータを追加するかどうかを指定します。  
  
 **変換先テーブルを削除した後、再作成する**  
 変換先テーブルを上書きします。 このオプションは、ウィザードを使用して変換先テーブルを作成した場合にのみ使用できます。 ウィザードによって作成されたパッケージを保存し、その後パッケージを再び実行すると、変換先テーブルは削除されて、再作成されます。 これは、設定を複数回テストする場合に便利なオプションです。
  
 **ID 挿入を許可する**  
 変換元データの既存の ID 値を変換先テーブルの ID 列に挿入します。 既定では、変換先の ID 列に対して挿入は通常許可されません。  
  
> [!TIP]
> 既存のプライマリ キーが id 列、autonumber 列、または同等の列である場合、既存のプライマリ キー値を保持するには、通常、このオプションを選択する必要があります。  その他の場合、変換先の ID 列には通常、新しい値が割り当てられます。  

## <a name="keep-your-autonumber-or-identity-values"></a>autonumber または ID 値を保持する
autonumber 列または ID 列があるデータをエクスポートする場合 (たとえば、Microsoft Access からエクスポートする場合)、すぐ上で説明したように、 **[ID 挿入を許可する]** を忘れずに選択します。

## <a name="review-column-mappings"></a>列マッピングの確認
![[列マッピング] ページ、マッピング セクション](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **マッピング**  
 データ ソースの各列が変換先の列にどのようにマップされるかを表示します。
 
**[マッピング]** の一覧には、次の列があります。  
  
-    **ソース**  
     各ソース列を表示します。  
  
-   **変換先**  
    マップされる変換先列を確認するか、別の列を選択します。
    
    ソース テーブルからすべての列をコピーする必要はありません。 コピーしない列については、 **[変換先]** を選択すると、列のサブセットのみをコピーできます。 列をマップする前に、マップされないすべての列を無視する必要があります。  
  
-   **Type**  
    変換先列のデータ型を確認するか、別のデータ型を選択します。
  
-   **NULL 値の使用**  
    変換先列に null 値を使用できるかどうかを指定します。  
  
-   **[サイズ]**  
    変換先列の文字数を指定します (該当する場合)。  
  
-    **[精度]**  
    桁数を参照して、変換先列での数値データの有効桁数を指定します (該当する場合)。  
  
 -   **[スケール]**  
    小数点以下の桁数を参照して、変換先列での数値データの小数点以下の精度を指定します (該当する場合)。  
  
## <a name="whats-next"></a>次の操作  
 ソース列からコピーしたデータを受け取る変換先列を確認して構成した後、 **[OK]** をクリックすると、 **[列マッピング]** ダイアログ ボックスの表示が **[コピー元のテーブルおよびビューを選択]** ページまたは **[フラット ファイルの変換先の構成]** ページに戻ります。 詳細については、「 [[コピー元のテーブルおよびビューを選択]](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 」または「 [[フラット ファイルの変換先の構成]](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)」を参照してください。  
  
 指定したマッピングが **[マッピング]** 一覧で成功しない可能性がある場合は、 **[列マッピング]** ダイアログ ボックスに **[データ型マッピングの確認]** ページが表示されます。 このページでは、警告を確認し、変換オプションを指定して、エラーの処理方法も指定します。 詳しくは、「 [[データ型マッピングの確認]](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)」をご覧ください。  
 
 ## <a name="see-also"></a>参照
[SQL Server インポートおよびエクスポート ウィザードのデータ型マッピング](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

