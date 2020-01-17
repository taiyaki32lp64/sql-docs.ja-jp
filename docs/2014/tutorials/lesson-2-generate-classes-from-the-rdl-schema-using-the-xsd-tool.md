---
title: レッスン 2:Xsd ツールを使用して RDL スキーマからクラスを生成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f5f74c6621d329885e9149fce9a37c7418d9c37b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653750"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>レッスン 2:xsd ツールを使用して RDL スキーマからクラスを作成
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトを作成したら、次はレポート定義スキーマのローカル コピーを取得して、XML スキーマ定義ツール (Xsd.exe) を実行します。  
  
### <a name="to-generate-the-rdl-classes"></a>RDL クラスを生成するには  
  
1.  インスタンスを開いて[!INCLUDE[msCoName](../includes/msconame-md.md)]Internet Explorer (または同等の Web ブラウザー)、次の URL に移動します。  
  
    ```  
    https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  RDL スキーマは、ブラウザーで開かれている、したらを参照、**ファイル**メニューを選択し、**付けて**します。  
  
3.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトを作成した場所に移動して、スキーマをファイル名 ReportDefinition.xsd として保存します。  
  
4.  インスタンスを開き、ファイルを保存した後、[!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]コマンド プロンプト。 コマンド プロンプトのインスタンスを開くには、スタート ボタンをポイントして**すべてのプログラム**、 をポイント**Microsoft Visual Studio 2010**、 をポイント**Visual Studio Tools**  をクリック**Visual Studio コマンド プロンプト (2010)** します。  
  
5.  現在のパスを、ReportDefinition.xsd ファイルを保存した場所に変更します。  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  次のコマンドを使用して、RDL スキーマのクラスを含む ReportDefinition.cs ファイルを生成します。  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     ReportDefinition.vb ファイルを生成するには、次のコマンドを使用します。  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  プロジェクトに ReportDefinition.xsd を追加します。 **プロジェクト** メニューのをクリックして**既存項目の追加**します。 ReportDefinition.xsd ファイルの場所を参照、ReportDefinition.xsd を選択およびクリックして**追加**します。  
  
    > [!NOTE]  
    >  ReportDefinition.xsd ファイルをプロジェクトに追加した後でわかります**ソリューション エクスプ ローラー** ReportDefinition.cs (.vb) ファイルがないことがあります。 ファイルを表示するには、ReportDefinition.xsd ファイルの横にある展開/折りたたみのボタンをクリックします。  
  
## <a name="next-lesson"></a>次のレッスン  
 次のレッスンでは、RDL スキーマから生成したクラスを使って、レポート サーバーからレポート定義を読み込むコードを作成します。 「[レッスン 3:レポート サーバーからレポート定義を読み込む](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)します。  
  
## <a name="see-also"></a>関連項目  
 [RDL スキーマから生成されたクラスを使用してレポートを更新&#40;SSRS チュートリアル&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [レポート定義言語 &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
