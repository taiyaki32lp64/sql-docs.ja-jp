---
title: プログラムによるパッケージの実行の管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 42c4383692677c0e124e72b997fdca54707f4d03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889592"
---
# <a name="managing-running-packages-programmatically"></a>プログラムによるパッケージの実行の管理
  プログラムによって [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを操作する際に、現在実行中のパッケージを特定することが必要な場合があります。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 名前空間の <xref:Microsoft.SqlServer.Dts.Runtime> クラスは、これらの要件を満たすメソッドとクラスを提供します。  
  
 パッケージの監視の詳細については、「[パッケージの管理 &#40;SSIS サービス&#41;](../service/package-management-ssis-service.md)」を参照してください。  
  
 このトピックで説明するすべてのメソッドには、`Microsoft.SqlServer.ManagedDTS` アセンブリへの参照が必要です。 新しいプロジェクトに参照を追加した後は、インポート、<xref:Microsoft.SqlServer.Dts.Runtime>を持つ名前空間、`using`または`Imports`ステートメント。  
  
> [!IMPORTANT]  
>  SSIS パッケージ ストアを操作するための <xref:Microsoft.SqlServer.Dts.Runtime.Application> クラスのメソッドでは、"."、localhost、またはローカル サーバーのサーバー名のみがサポートされます。 "(local)" は使用できません。  
  
## <a name="determining-which-packages-are-currently-running"></a>現在実行中のパッケージの特定  
 特定のサーバーでどのパッケージが現在実行されているかを調べるには、<xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A> メソッドを呼び出します。 このメソッドは、<xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> オブジェクトの <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> コレクションを返します。  
  
> [!NOTE]  
>  管理者に対しては、現在コンピューターで実行されているすべてのパッケージが表示されます。他のユーザーに対しては、自分が起動したパッケージのみが表示されます。  
  
## <a name="working-with-running-packages"></a>実行中のパッケージの操作  
 現在実行中のパッケージを特定した後、そのパッケージの情報を取得したり、パッケージの停止を要求することができます。  
  
### <a name="getting-information-about-a-running-package"></a>実行中のパッケージの情報の取得  
 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> コレクションを反復処理するときに、<xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> オブジェクトのプロパティを使用して、パッケージを探したり、実行中のパッケージに関する追加情報を取得することができます。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>実行中のパッケージの停止  
 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> オブジェクトの <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> メソッドを呼び出して、そのパッケージを停止するように要求できます。 停止要求が発行されてからパッケージが実際に停止するまでの間に遅延が発生する場合があります。  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [パッケージの管理 &#40;SSIS サービス&#41;](../service/package-management-ssis-service.md)   
 [プログラムによる使用可能なパッケージの列挙](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
