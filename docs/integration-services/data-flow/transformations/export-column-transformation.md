---
title: 列エクスポート変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exportcolumntrans.f1
- sql13.dts.designer.fileextractortransformation.columns.f1
- sql13.dts.designer.fileextractortransformation.errorhandling.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 52acb1db548f6425dcfaf6339d38a4b55e57b76e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297943"
---
# <a name="export-column-transformation"></a>列エクスポート変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  列エクスポート変換は、データ フローのデータを読み取り、そのデータをファイルに挿入します。 たとえば、データ フローに、各製品の写真などの製品情報が含まれる場合、列エクスポート変換を使用して、その画像をファイルに保存できます。  
  
## <a name="append-and-truncate-options"></a>追加オプションと切り捨てオプション  
 次の表では、追加オプションと切り捨てオプションが結果に与える影響について説明します。  
  
|追加|切り捨て|ファイルが存在するか|[結果]|  
|------------|--------------|-----------------|-------------|  
|False|False|いいえ|新しいファイルが作成され、そのファイルにデータが書き込まれます。|  
|True|False|いいえ|新しいファイルが作成され、そのファイルにデータが書き込まれます。|  
|False|True|いいえ|新しいファイルが作成され、そのファイルにデータが書き込まれます。|  
|True|True|いいえ|デザイン時の検証に失敗します。 両方のプロパティに **true**を設定するのは無効です。|  
|False|False|はい|実行時エラーが発生します。 ファイルは存在しますが、そのファイルに書き込めません。|  
|False|True|はい|ファイルが削除されて再作成され、データが書き込まれます。|  
|True|False|はい|ファイルが開かれ、そのファイルの終わりにデータが書き込まれます。|  
|True|True|はい|デザイン時の検証に失敗します。 両方のプロパティに **true**を設定するのは無効です。|  
  
## <a name="configuration-of-the-export-column-transformation"></a>列エクスポート変換の構成  
 列エクスポート変換は、次の方法で構成できます。  
  
-   データ列と、データの書き込み先のファイルのパスが含まれる列を指定します。  
  
-   データ挿入の操作の際に既存のファイルを追加するか、または切り捨てるかを指定します。  
  
-   バイト順マーク (BOM) をファイルに書き込むかどうかを指定します。  
  
    > [!NOTE]  
    >  BOM は、データが既存のファイルに追加されず、DT_NTEXT データ型の場合にのみ書き込まれます。  
  
 この変換では入力列の組を使用します: 1 つの列にはファイル名が含まれ、もう 1 つの列にはデータが含まれます。 データセットの各行では、異なるファイルを指定できます。 この変換により行が処理されると、データは指定したファイルに挿入されます。 実行時に既存のファイルがない場合、変換によりファイルが作成され、そのファイルにデータが書き込まれます。 書き込まれるデータは、DT_TEXT、DT_NTEXT、または DT_IMAGE データ型である必要があります。 詳細については、「 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つの出力、および 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="export-column-transformation-editor-columns-page"></a>[列エクスポート変換エディター] ([列] ページ)
  **[列エクスポート変換エディター]** ダイアログ ボックスの **[列]** ページを使用すると、ファイルに抽出するデータ フロー内の列を指定できます。 列エクスポート変換でファイルにデータを追加するか、既存のファイルを上書きするかどうかを指定できます。  
  
### <a name="options"></a>オプション  
 **[列の抽出]**  
 テキストまたは画像データを持つ入力列の一覧から選択します。 すべての行には、 **[列の抽出]** と **[ファイル パス列]** の定義が含まれます。  
  
 **[ファイル パス列]**  
 ファイル パスとファイル名を持つ入力列の一覧から選択します。 すべての行には、 **[列の抽出]** と **[ファイル パス列]** の定義が含まれます。  
  
 **[追加の許可]**  
 変換により、既存のファイルにデータを追加するかどうかを指定します。 既定値は **false**です。  
  
 **[強制的に切り捨て]**  
 変換により、データを書き込む前に既存のファイルの内容を削除するかどうかを指定します。 既定値は **false**です。  
  
 **[バイト順マークの書き込み]**  
 バイト順マーク (BOM) をファイルに書き込むかどうかを指定します。 BOM は、データが **DT_NTEXT** または DT_WSTR のデータ型を持つ場合にのみ書き込まれ、既存のデータ ファイルには追加されません。  
  
## <a name="export-column-transformation-editor-error-output-page"></a>[列エクスポート変換エディター] ([エラー出力] ページ)
  **[列エクスポート変換エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラーをどのように処理するかを指定できます。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 出力の名前を表示します。 名前をクリックすると、ビューを展開して列を含めることができます。  
  
 **列**  
 **[列エクスポート変換エディター]** ダイアログ ボックスの **[列]** ページで選択された出力列を表示します。  
  
 **Error**  
 エラーが発生したときの処理方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を指定します。  
  
 **切り捨て**  
 切り捨てが発生したときの処理方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を指定します。  
  
 **[説明]**  
 操作の説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
  
