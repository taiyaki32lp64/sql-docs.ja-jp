---
title: (SSRS チュートリアル) RDL スキーマから生成されたクラスを使用してレポートの更新 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RDL [Reporting Services], generating
- RDL [Reporting Services], tutorials
- RDL [Reporting Services], serializing
ms.assetid: 8f81d48f-7ab9-4ef8-bce0-7d16d9a47fbd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 313a5268b754089d4ca8964328d53cb23ec6edd1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62746116"
---
# <a name="updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial"></a>RDL スキーマから生成されたクラスを使ったレポートの更新 (SSRS チュートリアル)
  このチュートリアルで、およびレポート定義ファイル (.rdl、.rdlc) を逆シリアル化するための XML スキーマ定義ツール (Xsd.exe) クラスを生成するを使用する方法を示しています、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.Xml.Serialization.XmlSerializer>クラス。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルの中は、次のアクティビティを行います。  
  
-   使用して、アプリケーションを作成、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]コンソール アプリケーション プロジェクト テンプレート。  
  
-   使用して、レポート定義言語 (RDL) スキーマからクラスを生成、 **xsd**ツール。  
  
-   レポート サーバーに接続し、レポート定義を取得する。  
  
-   レポート定義ファイルを更新するコードを記述する。  
  
-   更新したレポート定義をレポート サーバーに保存する。  
  
-   RDL スキーマ アプリケーション (VB/C#) を実行する。  
  
> [!NOTE]  
>  このチュートリアルのコード サンプルでは、レポートに説明がないため失敗する場合があります。 失敗する理由は、説明が指定されていないレポートには説明のプロパティが存在しないためです。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルを完了するには次の準備が必要です。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]」を参照してください。  
  
-   レポート サーバーが配置されているコンピューター上のレポート サーバー Web サービスにアクセスし、レポートをパブリッシュできる十分な権限。  
  
-   [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] のインスタンスにインストールされた [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サンプル データベース。  
  
-   レポート サーバーにインストールされているレポート。 このチュートリアルでは、サンプル レポート Company Sales 2012 を使用します。 サンプル レポートの詳細については、次を参照してください。 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)します。  
  
> [!NOTE]  
>  サンプルはセットアップ中に自動的にインストールされませんが、いつでもインストールできます。 サンプルについては、次を参照してください。 [SQL Server Product Samples](https://go.microsoft.com/fwlink/?LinkId=182887)します。  
  
 **このチュートリアルの推定所要時間:** 30 分  
  
## <a name="tasks"></a>処理手順  
 [レッスン 1:RDL スキーマ Visual Studio プロジェクトを作成します。](../../2014/tutorials/lesson-1-create-the-rdl-schema-visual-studio-project.md)  
  
 [レッスン 2:Xsd ツールを使用して RDL スキーマからクラスを生成します。](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)  
  
 [レッスン 3:レポート サーバーからレポート定義を読み込む](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)  
  
 [レッスン 4:レポート定義をプログラムで更新します。](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)  
  
 [レッスン 5: レポート サーバーにレポート定義をパブリッシュします。](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)  
  
 [レッスン 6:RDL スキーマ アプリケーションの実行&#40;VB C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)  
  
## <a name="see-also"></a>参照  
 [レポート定義言語 &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
