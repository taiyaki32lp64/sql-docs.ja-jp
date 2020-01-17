---
title: エラーとイベントのリファレンス (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- events [Integration Services]
- errors [Integration Services]
- Integration Services, errors
ms.assetid: cf4f0f14-8087-42d7-9b67-e4929228abd6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 64e805e5dd9b334afe252e2c1d43685e9c92b95f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290617"
---
# <a name="errors-and-events-reference-integration-services"></a>エラーとイベントのリファレンス (Integration Services)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ここでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]に関連するいくつかのエラーとイベントについて説明します。 エラー メッセージについては、原因と解決方法も示します。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] エラーとその説明の一覧など、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のエラー メッセージの詳細については、「 [Integration Services のエラーおよびメッセージのリファレンス](../integration-services/integration-services-error-and-message-reference.md)」を参照してください。 ただし、現在一覧にはトラブルシューティング情報は含まれていません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で作業しているときに発生する可能性のあるエラー メッセージの多くは、他のコンポーネントが原因になっています。 これには、OLE DB プロバイダー、 [!INCLUDE[ssDE](../includes/ssde-md.md)] や [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] などの他のデータベース コンポーネント、またはファイル システム、SMTP サーバー、Microsoft Message Queueing などの他のサービスやコンポーネントが含まれます。 このような外部エラー メッセージの情報については、コンポーネント固有のドキュメントを参照してください。  
  
## <a name="error-messages"></a>エラー メッセージ  
  
|エラーのシンボル名|[説明]|  
|----------------------------|-----------------|  
|DTS_E_CACHELOADEDFROMFILE|キャッシュ変換によるインメモリ キャッシュへのデータの書き込みが試行されているため、パッケージを実行できないが、 キャッシュ接続マネージャーは、既にキャッシュ ファイルをインメモリ キャッシュに読み込んでいることを示しています。|  
|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|指定された接続に失敗したため、パッケージを実行できないことを示しています。|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|データ フロー コンポーネントが Unicode 文字列データを別のコンポーネントに渡そうとしているが、そのコンポーネントの対象となる列では Unicode 以外の文字列データが必要とされていることを示しています。または、その逆に Unicode 以外の文字列を、Unicode 文字列データが必要となる列へ渡そうとしていることを示しています。|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|データ フロー コンポーネントが Unicode 文字列データを別のコンポーネントに渡そうとしているが、そのコンポーネントの対象となる列では Unicode 以外の文字列データが必要とされていることを示しています。または、その逆に Unicode 以外の文字列を、Unicode 文字列データが必要となる列へ渡そうとしていることを示しています。|  
|DTS_E_CANTINSERTCOLUMNTYPE|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 列のデータ型とデータベース列のデータ型との間の変換がサポートされていないので、データベース テーブルに列を追加できないことを示しています。|  
|DTS_E_CONNECTIONNOTFOUND|指定された接続マネージャーが見つからないので、パッケージを実行できないことを示しています。|  
|DTS_E_CONNECTIONREQUIREDFORMETADATA|[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでは、変換元または変換先の新しいメタデータや更新されたメタデータを取得する際にデータ ソースに接続する必要があること、およびこのデザイナーがデータ ソースに接続できないことを示しています。|  
|DTS_E_MULTIPLECACHEWRITES|キャッシュ変換によるインメモリ キャッシュへのデータの書き込みが試行されているため、パッケージを実行できないが、 別のキャッシュ変換が、既にインメモリ キャッシュに書き込んでいることを示しています。|  
|DTS_E_PRODUCTLEVELTOLOW|適切なバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] がインストールされていないため、パッケージを実行できないことを示しています。|  
|DTS_E_READNOTFILLEDCACHE|キャッシュ変換によるキャッシュへのデータの書き込みと同時に、参照変換によるインメモリ キャッシュ内からのデータの読み取りが試行されていることを示しています。|  
|DTS_E_UNPROTECTXMLFAILED|保護された XML ノードの暗号化が解除されなかったことを示しています。|  
|DTS_E_WRITEWHILECACHEINUSE|参照変換によるインメモリ キャッシュからのデータの読み取りと同時に、キャッシュ変換によるインメモリ キャッシュへのデータの書き込みが試行されていることを示しています。|  
|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|データ ソース内の列のメタデータが、そのデータ ソースに接続されている変換元コンポーネントまたは変換先コンポーネントの列のメタデータと一致しないことを示しています。|  
  
## <a name="events-sqlispackage"></a>イベント (SQLISPackage)  
 詳細については、「 [Integration Services パッケージによってログに記録されるイベント](../integration-services/performance/events-logged-by-an-integration-services-package.md)」を参照してください。  
  
|イベント|[説明]|  
|-----------|-----------------|  
|SQLISPackage_12288|パッケージが開始されたことを示しています。|  
|SQLISPackage_12289|パッケージの実行が正常に完了したことを示しています。|  
|SQLISPACKAGE_12291|パッケージが実行を完了できず、停止したことを示しています。|  
|SQLISPackage_12546|パッケージ内のタスクまたは他の実行可能ファイルで作業が完了したことを示しています。|  
|SQLISPackage_12549|パッケージで警告メッセージが発生したことを示しています。|  
|SQLISPackage_12550|パッケージでエラー メッセージが発生したことを示しています。|  
|SQLISPackage_12551|パッケージが作業を完了せずに停止したことを示しています。|  
|SQLISPackage_12557|パッケージの実行が完了したことを示しています。|  
  
## <a name="events-sqlisservice"></a>イベント (SQLISService)  
 詳細については、「 [Integration Services サービスによってログに記録されるイベント](../integration-services/service/events-logged-by-the-integration-services-service.md)」を参照してください。  
  
|イベント|[説明]|  
|-----------|-----------------|  
|SQLISService_256|サービスを開始しようとしていることを示しています。|  
|SQLISService_257|サービスが開始したことを示しています。|  
|SQLISService_258|サービスを停止しようとしていることを示しています。|  
|SQLISService_259|サービスが停止したことを示しています。|  
|SQLISService_260|サービスを開始しようとしたが開始できなかったことを示しています。|  
|SQLISService_272|指定した場所に構成ファイルが存在しないことを示しています。|  
|SQLISService_273|構成ファイルを読み取ることができなかったか、無効であることを示しています。|  
|SQLISService_274|構成ファイルの場所を含むレジストリ エントリが存在しないか、空であることを示しています。|  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../integration-services/integration-services-error-and-message-reference.md)  
  
  
