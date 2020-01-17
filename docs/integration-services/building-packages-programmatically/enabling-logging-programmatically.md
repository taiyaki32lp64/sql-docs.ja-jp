---
title: プログラムによるログ記録の有効化 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 45e97657bf70bdf023388f97497f9c2a8c5dd0f4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294944"
---
# <a name="enabling-logging-programmatically"></a>プログラムによるログ記録の有効化

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ランタイム エンジンでは、パッケージの検証中および実行中にイベント固有の情報のキャプチャを有効にするための <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> オブジェクトのコレクションが提供されます。 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> オブジェクトは、<xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer> オブジェクト群、つまり <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>、<xref:Microsoft.SqlServer.Dts.Runtime.Package>、<xref:Microsoft.SqlServer.Dts.Runtime.ForLoop>、<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> などの各オブジェクトで使用できます。 ログ記録は、個別のコンテナーでも、パッケージ全体でも有効にすることができます。  
  
 コンテナーで使用できるログ プロバイダーには、いくつかの種類があります。 そのため、さまざまな形式でログ情報を作成し、保存することができます。 コンテナー オブジェクトをログ記録に登録するには、まずログ記録を有効にし、次にログ プロバイダーを選択するという、2 段階の処理が必要です。 コンテナーの <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> プロパティおよび <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> プロパティを使用して、ログ記録するイベントを指定し、ログ プロバイダーを選択します。  
  
## <a name="enabling-logging"></a>ログ記録の有効化  
 ログ記録を実行できる各コンテナーにある <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> プロパティは、コンテナーのイベント情報をイベント ログに記録するかどうかを指定します。 このプロパティには <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> 構造の値が割り当てられ、既定でコンテナーの親オブジェクトから継承されます。 コンテナーがパッケージであるため、親オブジェクトがない場合、プロパティは <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting> を使用します。既定値は **Disabled** です。  
  
### <a name="selecting-a-log-provider"></a>ログ プロバイダーの選択  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> プロパティを **Enabled** に設定したら、コンテナーの <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> コレクションにログ プロバイダーを追加し、処理を完了します。 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> オブジェクトでは <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> コレクションが使用可能で、これにはコンテナーで選択されたログ プロバイダーが含まれています。 プロバイダーを作成し、コレクションに追加するには、<xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> メソッドを呼び出します。 このメソッドは、コレクションに追加されたログ プロバイダーを返します。 それぞれのプロバイダーには、そのプロバイダーに特有の構成設定があります。これらのプロパティは、<xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> プロパティを使用して設定します。  
  
 次の表に、使用可能なログ プロバイダー、説明、および <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 情報を示します。  
  
|プロバイダー|[説明]|ConfigString プロパティ|  
|--------------|-----------------|---------------------------|  
|SQL Server プロファイラー|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler でキャプチャおよび表示される SQL トレースを生成します。 このプロバイダーで使用されるファイル名の既定の拡張子は、.trc です。|構成は必要ありません。|  
|SQL Server|イベント ログ エントリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの **sysssislog** テーブルに書き込みます。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロバイダーの場合は、データベースへの接続と対象データベースの名前を指定する必要があります。|  
|テキスト ファイル|イベント ログ エントリをコンマ区切り (CSV) 形式で ASCII テキスト ファイルに書き込みます。 このプロバイダーで使用されるファイル名の既定の拡張子は、.log です。|ファイル接続マネージャーの名前。|  
|Windows イベント ログ|ローカル コンピューター上のアプリケーション ログの標準 Windows イベント ログにログを記録します。|構成は必要ありません。|  
|XML ファイル|イベント ログ エントリを XML 形式ファイルに書き込みます。 このプロバイダーの既定のファイル名拡張子は .xml です。|ファイル接続マネージャーの名前。|  
  
 イベント ログのイベントを含めたり除外するには、コンテナーの **EventFilterKind** および **EventFilter** プロパティを設定します。 **EventFilterKind** 構造体には、**ExclusionFilter** および **InclusionFilter** という 2 つの値が含まれており、**EventFilter** に追加されるイベントがイベント ログに含まれるかどうかを示します。 次に、フィルター選択の対象となるイベントの名前を含む文字配列を **EventFilter** プロパティに割り当てます。  
  
 次のコードは、パッケージのログ記録を有効にし、<xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> コレクションにテキスト ファイルのログ プロバイダーを追加し、ログ出力に含めるイベントの一覧を指定します。  
  
## <a name="sample"></a>サンプル  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      ConnectionManager loggingConnection = p.Connections.Add("FILE");  
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";  
  
      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");  
      provider.ConfigString = loggingConnection.Name;  
      p.LoggingOptions.SelectedLogProviders.Add(provider);  
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;  
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute",   
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };  
      p.LoggingMode = DTSLoggingMode.Enabled;  
  
      // Add tasks and other objects to the package.  
  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
  
    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")  
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"  
  
    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")  
    provider.ConfigString = loggingConnection.Name  
    p.LoggingOptions.SelectedLogProviders.Add(provider)  
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion  
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _  
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}  
    p.LoggingMode = DTSLoggingMode.Enabled  
  
    ' Add tasks and other objects to the package.  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
