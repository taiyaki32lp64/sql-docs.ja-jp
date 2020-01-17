---
title: レポートとスナップショットのサイズ制限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- large reports
- maximum report size
- size [SQL Server], reports
- report size [Reporting Services]
- reports [Reporting Services], size
- denial of service attacks [Reporting Services]
ms.assetid: 1e3be259-d453-4802-b2f5-6b81ef607edf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cef2943b2d7805a9738662bcd85c9602430a7e6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103538"
---
# <a name="report-and-snapshot-size-limits"></a>レポートとスナップショットのサイズ制限
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の配置を管理する管理者は、このトピックの情報を参照することにより、レポート サーバーへのパブリッシュ時、レンダリング時 (実行時)、ファイル システムへの保存時のレポート サイズ制限を理解できます。 このトピックでは、レポート サーバー データベースのサイズを測定する方法の具体的な指針とサーバーのパフォーマンスのスナップショット サイズの効果についても説明します。  
  
## <a name="maximum-size-for-published-reports-and-models"></a>パブリッシュされたレポートとモデルの最大サイズ  
 レポート サーバー上のレポートとモデルのサイズは、レポート サーバーにパブリッシュされたレポート定義ファイル (.rdl) とレポート モデル ファイル (.smdl) のサイズに基づいています。 レポート サーバーでは、パブリッシュするレポートまたはモデルのサイズは制限されません。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] により、サーバーに送信できるアイテムの最大サイズが制限されています。 既定では、この制限は 4 MB です。 この制限を超えるサイズのファイルをレポート サーバーにアップロードまたはパブリッシュすると、HTTP 例外が返されます。 この場合、Machine.config ファイルの `maxRequestLength` 要素の値を大きくすることで、既定値を変更することができます。  
  
 レポート モデルは非常に大きくなる場合がありますが、レポート定義が 4 MB を超えることはほとんどありません。 一般的なレポート サイズは、キロバイト (KB) 単位です。 ただし、埋め込み画像が含まれている場合は、これらの画像のエンコードによってレポート定義のサイズが大きくなり、既定の 4 MB を超える可能性があります。  
  
 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] では、サーバーに対するサービス拒否攻撃 (DoS) の脅威を低減するために、送信ファイルに最大サイズを設けています。 最大サイズの制限の値を大きくした場合、この制限による保護がある程度弱められます。 値を大きくすることで得られるメリットが、それに伴うセキュリティ リスクの増大よりも重要であると確信できる場合のみ、値を大きくしてください。  
  
 `maxRequestLength` 要素に設定する値は、適用する実際のサイズ制限より大きい必要があることに注意してください。 すべてのパラメーターが SOAP エンベロープにカプセル化され、Base64 エンコードが <xref:ReportService2010.ReportingService2010.CreateReportEditSession%2A> メソッドや <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> メソッドの定義パラメーターなどの特定のパラメーターに適用されると、必然的に HTTP 要求サイズまで増大するため、値を大きくする必要があります。 Base64 エンコードによって、元のデータのサイズより約 33% 大きくなります。 このため、`maxRequestLength` 要素に指定する値は、実際の使用可能なアイテムのサイズより約 33% 大きくする必要があります。 たとえば、`maxRequestLength` を 64 MB に指定した場合、実際にレポート サーバーに送信されるレポート ファイルの最大サイズは約 48 MB になると予測されます。  
  
## <a name="report-size-in-memory"></a>メモリ内のレポート サイズ  
 レポート実行時のレポート サイズは、レポートに返されるデータ量に出力ストリームのサイズを加えた値になります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レンダリングされたレポートのサイズに対する最大値が設定されません。 サイズの上限は、システム メモリによって決まります。既定では、構成された使用可能なメモリがすべてレポートのレンダリング時に使用されますが、メモリのしきい値およびメモリ管理ポリシーを設定するための構成設定を指定できます。 詳細については、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。  
  
 いずれのレポートでも、返されるデータ量とレポートの表示形式に応じて、サイズが大幅に変化する可能性があります。 パラメーター化されたレポートは、パラメーター値がクエリの結果にどのように影響するかによって、サイズが増減する可能性があります。 選択したレポートの出力形式は、レポート サイズに次のように影響します。  
  
-   HTML では、レポートが 1 ページずつ処理されます。 レポートの処理単位が小さいので、個々のチャンクを処理するために必要なメモリの使用量は少なくなります。  
  
-   PDF、Excel、TIFF、XML、および CSV では、ユーザーに対してレポートを表示する前に、メモリ内でレポート全体が処理されます。  
  
 表示されているレポートのサイズを測定する場合は、レポート実行ログを参照できます。 詳細については、次を参照してください。[レポート サーバー実行ログと ExecutionLog3 ビュー](report-server-executionlog-and-the-executionlog3-view.md)します。  
  
 ディスク上のレンダリング済みレポートのサイズを計算する場合は、レポートをファイル システムにエクスポートして保存できます (保存されるファイルには、データとレポート形式情報が含まれます)。  
  
 レポート サイズのハード制限は、Excel 形式で表示する場合にのみ存在します。 ワークシートの大きさが、65536 行および 256 列を超えることはできません。 他の表示形式にはこれらの制限がないので、サーバーのリソース量によってのみサイズが制限されます。 Excel ファイルの制限の詳細については、次を参照してください。[別のファイルの種類としてレポートをエクスポート&#40;レポート ビルダーおよび SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)します。  
  
> [!NOTE]  
>  レポートの処理とレンダリングは、メモリ内で行われます。 レポートが大きい場合またはユーザーが多い場合は、なんらかのキャパシティ プランニングを行い、ユーザーにとって満足のいくレベルのパフォーマンスを実現できるようにレポート サーバーを配置してください。 ツールとガイドラインの詳細については、MSDN の次の記事を参照してください。[Reporting Services でのスケーラビリティおよびパフォーマンス計画](http://spmarchitecture.com/ssrs-architecture/planning-for-scalability-and-performance-reporting-services-70744/)と[Visual Studio 2005 を使用して、SQL Server 2005 Reporting Services レポート サーバーのロード テストを実行する](https://go.microsoft.com/fwlink/?LinkID=77519)します。  
  
## <a name="measuring-snapshot-storage"></a>スナップショット ストレージの測定  
 スナップショットのサイズは、レポートのデータ量に比例します。 通常、スナップショットは、レポート サーバーに格納されている他の項目よりはるかに大きくなります。 スナップショットの一般的なサイズの範囲は、数メガバイトから数十メガバイトです。 非常に大きいレポートを使用している場合、さらにスナップショットが大きくなる可能性があります。 スナップショットを使用する頻度およびレポート履歴の構成方法に応じて、レポート サーバー データベースに必要なディスク領域が短期間で急速に増える可能性があります。  
  
 既定では、 **reportserver** と **reportservertempdb** データベースは、自動拡張に設定されます。 データベース サイズが自動的に大きくなりますが、自動的に小さくなることはありません。 スナップショットを削除したため、 **reportserver** データベースに余分な容量がある場合、手動でサイズを小さくして、ディスク領域を回復する必要があります。 同様に、非常に大きな対話型のレポートを格納するために **reportservertempdb** のサイズが大きくなっていても、ディスク領域の割り当ては、サイズを小さくするまでその設定のままです。  
  
 レポート サーバー データベースのサイズを測定するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行します。 定期的にデータベースの合計サイズを計算すると、時間の経過と共にレポート サーバー データベースの領域の割り当て方法に関する適切な推定値を算出できます。 次のステートメントは、現在使用されている領域を測定します (このステートメントでは、既定のデータベース名が使用されていると仮定します)。  
  
```  
USE ReportServer  
EXEC sp_spaceused  
```  
  
## <a name="snapshot-size-and-report-server-performance"></a>スナップショットのサイズとレポート サーバーのパフォーマンス  
 スナップショットのサイズは、レポートが処理されて表示される際、サーバーのパフォーマンスに影響します。 サーバーのパフォーマンスは、表示操作で最も影響を受けます。このため、大きいスナップショットを使用している場合、ユーザーがレポートを要求する際に遅延が発生する可能性があります。 ユーザー数によっては、スナップショットのサイズが 100 メガバイトを超えると、遅延が発生することがあります。  
  
 大きいスナップショットによるパフォーマンスの遅延を最小限に抑えるには、次の方法を使用できます。  
  
-   レポート サーバーと [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] を別々のコンピューターに配置します。  
  
-   システム メモリを追加します。  
  
-   企業向けレポート サーバーの構成方法に関する推奨事項について、MSDN Web サイトの「Planning for Scalability and Performance with Reporting Services (Reporting Services でのスケーラビリティおよびパフォーマンスの計画)」を確認します。  
  
 レポート サーバー データベースに格納されているスナップショットの数量自体は、パフォーマンスに影響する要因にはなりません。 サーバーのパフォーマンスに影響を与えないで、多くのスナップショットを格納できます。 スナップショットは、無期限に保存できます。 ただし、レポート履歴は構成が可能なので注意が必要です。 レポート サーバー管理者がレポート履歴の制限値を低くした場合、保存したレポート履歴が失われることがあります。 レポートを削除すると、すべてのレポート履歴が一緒に削除されます。  
  
## <a name="see-also"></a>参照  
 [レポート処理プロパティの設定](set-report-processing-properties.md)   
 [レポート サーバー データベース &#40;SSRS ネイティブ モード&#41;](report-server-database-ssrs-native-mode.md)   
 [サイズの大きなレポートの処理](process-large-reports.md)  
  
  
