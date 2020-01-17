---
title: RAW ファイル ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfilesource.f1
- sql13.dts.designer.rawfilesourceconnectionmanager.f1
- sql13.dts.designer.rawfilesourcecolumns.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e35fffa75f72b4edaddba344d166cb1c89fb3338
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298137"
---
# <a name="raw-file-source"></a>RAW ファイル ソース (Raw File source)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  RAW ファイル ソースは、ファイルから生データを読み取ります。 データはソース ファイル固有の方法で表示されるため、変換の必要がなく、ほとんどの場合は解析の必要もありません。 したがって、RAW ファイル ソースは、フラット ファイルや OLE DB などの他のソースよりも、高速にデータを読み取ることができます。  
  
 RAW ファイル ソースは、以前 RAW ファイルの変換先に記述された生データを取得するために使用されます。 また、RAW ファイル ソースの参照先を、列のみを含む空の RAW ファイル (メタデータのみのファイル) にすることもできます。 パッケージを実行せずにメタデータのみのファイルを生成するには、RAW ファイル変換先を使用します。 詳細については、「 [RAW ファイル変換先](../../integration-services/data-flow/raw-file-destination.md)」を参照してください。  
  
 RAW ファイルの形式には、並べ替えの情報が含まれています。 RAW ファイル変換先には、文字列の列の比較フラグを含む並べ替えの情報がすべて保存されます。 RAW ファイル ソースは、並べ替えの情報を読み取って受け入れます。 詳細エディターを使用して、ファイル内の並べ替えのフラグを無視するように RAW ファイル ソースを構成するためのオプションが用意されています。 比較フラグの詳細については、「 [文字列データの比較](../../integration-services/data-flow/comparing-string-data.md)」を参照してください。  
  
 RAW ファイルを構成するには、RAW ファイル ソースが読み取るファイル名を指定します。  
  
> [!NOTE]  
>  このソースでは、接続マネージャーは使用されません。  
  
 このソースは、1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-raw-file-source"></a>RAW ファイル ソースの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [RAW ファイルのカスタム プロパティ](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 コンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   sqlservercentral.com のブログ「 [RAW ファイルは最高](https://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx)」  
  
## <a name="raw-file-source-editor-connection-manager-page"></a>[生ファイル ソース エディター] ([接続マネージャー] ページ)
  RAW ファイル ソースは、ファイルから生データを読み取ります。 データはソース ファイル固有の方法で表示されるため、変換の必要がなく、ほとんどの場合は解析の必要もありません。   
## <a name="raw-file-source-editor-columns-page"></a>[生ファイル ソース エディター] ([列] ページ)
  RAW ファイル ソースは、ファイルから生データを読み取ります。 データはソース ファイル固有の方法で表示されるため、変換の必要がなく、ほとんどの場合は解析の必要もありません。   
## <a name="see-also"></a>参照  
 [RAW ファイル変換先](../../integration-services/data-flow/raw-file-destination.md)   
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
