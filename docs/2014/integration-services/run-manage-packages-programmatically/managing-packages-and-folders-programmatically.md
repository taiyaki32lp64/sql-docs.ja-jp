---
title: プログラムによるパッケージとフォルダーの管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6ede05e340cbd2822cd72ceee514f6ce31a2755
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766854"
---
# <a name="managing-packages-and-folders-programmatically"></a>プログラムによるパッケージとフォルダーの管理
  プログラムで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを操作する際に、個々のパッケージやフォルダーが存在するかどうかを判断したり、パッケージが格納されたフォルダーを管理したりする必要がある場合があります。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 名前空間の <xref:Microsoft.SqlServer.Dts.Runtime> クラスは、これらの要件を満たすさまざまなメソッドを提供します。  
  
##  <a name="exists"></a> パッケージまたはフォルダーが存在するかどうかの判断  
 保存済みのパッケージの読み込みと実行を行う前に、プログラムによってそのパッケージが存在するかどうかを判断するには、次のいずれかのメソッドを呼び出します。  
  
|ストレージの場所|呼び出すメソッド|  
|----------------------|--------------------|  
|[SSIS パッケージ ストア]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|  
  
 フォルダーに保存されているパッケージを一覧表示する前に、プログラムによってそのフォルダーが存在するかどうかを判断するには、次のいずれかのメソッドを呼び出します。  
  
|ストレージの場所|呼び出すメソッド|  
|----------------------|--------------------|  
|[SSIS パッケージ ストア]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|  
  

  
##  <a name="managing"></a> パッケージとフォルダーの管理  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 名前空間の <xref:Microsoft.SqlServer.Dts.Runtime> クラスには、パッケージおよびそれを格納するフォルダーの管理用に、追加のメソッドが提供されています。  
  
###  <a name="managing_rempkg"></a> パッケージの削除  
 プログラムにより保存済みパッケージを削除するには、次のいずれかのメソッドを呼び出します。  
  
|ストレージの場所|呼び出すメソッド|  
|----------------------|--------------------|  
|[SSIS パッケージ ストア]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="managing_create"></a> フォルダーの作成  
 プログラムによりストレージ フォルダーを作成するには、次のいずれかのメソッドを呼び出します。  
  
|ストレージの場所|呼び出すメソッド|  
|----------------------|--------------------|  
|[SSIS パッケージ ストア]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="managing_remfldr"></a> フォルダーの削除  
 プログラムによりストレージ フォルダーを削除するには、次のいずれかのメソッドを呼び出します。  
  
|ストレージの場所|呼び出すメソッド|  
|----------------------|--------------------|  
|[SSIS パッケージ ストア]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="managing_rename"></a> フォルダーの名前変更  
 プログラムによりストレージ フォルダーの名前を変更するには、次のいずれかのメソッドを呼び出します。  
  
|ストレージの場所|呼び出すメソッド|  
|----------------------|--------------------|  
|[SSIS パッケージ ストア]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [パッケージの管理 &#40;SSIS サービス&#41;](../service/package-management-ssis-service.md)   
 [プログラムによる使用可能なパッケージの列挙](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
