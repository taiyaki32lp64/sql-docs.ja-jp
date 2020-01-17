---
title: フラット ファイルの変換先の構成 (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8c596f37cb0a83682c5c8dff370a92a5d3d73eb5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285794"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>[フラット ファイルの変換先の構成] (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  フラット ファイルの変換先を選択した場合、テーブルをコピーするように指定した後で、またはクエリを指定した後で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードには、 **[フラット ファイルの変換先の構成]** が表示されます。 このページで、宛先のフラット ファイルの書式設定オプションを指定します 必要に応じて、個々の列のマッピングを確認し、サンプル データをプレビューします。  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>[フラット ファイル変換先の構成] ページのスクリーン ショット  
 次のスクリーン ショットは、ウィザードの **[フラット ファイルの変換先の構成]** ページのサンプルです。
 
 この例では、ユーザーは次のオプションを指定し、一般的な CSV (コンマ区切り値) ファイルを作成しています。
-   **行区切り記号**」を参照してください。 出力のデータの各行は、改行復帰と改行の組み合わせで終わっています。
-   **列区切り記号**」を参照してください。 各行内のデータの列はコンマで区切られています。

 ![インポートおよびエクスポート ウィザードのフラット ファイル ページの構成](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>ソース テーブルを選択する
 **ソース テーブルまたはビュー**  
-   前のページでテーブルのコピーを指定した場合、ドロップダウン リストからソース テーブルまたはビューを選択します。
-   クエリを指定した場合、`"Query"` が選択されています。これは唯一のオプションです。  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>出力の行と列の区切り記号を指定する
 **[行区切り記号]**  
 出力で行を区切るための区切り記号を一覧から選択します。 *カスタム*の行区切り記号を指定するオプションはありません。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**{CR}{LF}**|復帰と改行の組み合わせで行を区切ります。|  
|**{CR}**|復帰で行を区切ります。|  
|**{LF}**|改行で行を区切ります。|  
|**セミコロン {;}**|セミコロンで行を区切ります。|  
|**コロン {:}**|コロンで行を区切ります。|  
|**[コンマ {,}]**|コンマで行を区切ります。|  
|**[タブ {t}]**|タブで行を区切ります。|  
|**縦棒 {&#124;}**|垂直バーで行を区切ります。|  
  
 **列区切り記号**  
 出力で列を区切るための区切り記号を一覧から選択します。 *カスタム*の列区切り記号を指定するオプションはありません。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**{CR}{LF}**|復帰と改行の組み合わせで列を区切ります。|  
|**{CR}**|復帰で列を区切ります。|  
|**{LF}**|改行で列を区切ります。|  
|**セミコロン {;}**|セミコロンで列を区切ります。|  
|**コロン {:}**|コロンで列を区切ります。|  
|**[コンマ {,}]**|コンマで列を区切ります。|  
|**タブ {t}**|タブで列を区切ります。|  
|**[縦棒 {&#124;}]**|垂直バーで列を区切ります。|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>必要に応じて、列マッピングとプレビュー データをレビューします。

**マッピングの編集**   
必要に応じて、 **[マッピングの編集]** をクリックして、選択したテーブルに対する **[列マッピング]** ダイアログ ボックスを表示します。 **[列マッピング]** ダイアログ ボックスを使用して、次のことを行います。
-   変換元と変換先の間の個々の列のマッピングを確認します。
-   列のサブセットのみをコピーするには、コピーしない列について **[無視]** を選択します。

詳細については、「 [列マッピング](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)」を参照してください。  

**プレビュー**  
必要に応じて、 **[プレビュー]** をクリックして、 **[データのプレビュー]** ダイアログ ボックスで、最大 200 行のサンプル データをプレビューします。 プレビューで、コピーしたいデータがウィザードによってコピーされることを確認します。 詳細については、 [データのプレビュー](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)に関するページを参照してください。  
  
データをプレビューした後で、ウィザードの前のページで選択したオプションを変更してもかまいません。 これらの変更を行うには、 **[フラット ファイルの変換先の構成]** ページに戻り、 **[戻る]** をクリックし、選択の変更が可能な前のページに戻ります。  

## <a name="whats-next"></a>次の操作  
 変換先のフラット ファイルの書式設定オプションを指定すると、次のページは **[パッケージの保存および実行]** となります。 このページでは、操作をすぐに実行するかどうかを指定します。 構成によっては、設定を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージとして保存して、それをカスタマイズし、後から再利用することができます。 詳細については、 [パッケージの保存および実行](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)に関するページを参照してください。  

