---
title: SMO | をインストールするMicrosoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cabd2d1ebbe726971e7837ff3e268ad3c2cee89f
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041260"
---
# <a name="installing-smo"></a>SMO のインストール

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

このページでは、アプリケーションで使用する SMO をインストールする方法と、SMO を使用するためのシステム要件について説明します。

## <a name="smo-nuget-package"></a>SMO NuGet パッケージ

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017以降、smo は [SqlManagementObjects NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) パッケージとして配布され、ユーザーは smo を使用してアプリケーションを開発できるようになります。

これは、SQL Server の各リリースの SQL Feature Pack の一部としてリリースされた SharedManagementObjects の後継です。 SMO を使用するアプリケーションは、代わりに NuGet パッケージを使用するように更新する必要があり、開発中のアプリケーションと共にバイナリが確実にインストールされるようにします。

>>[!Important]
>>「[ファイルとバージョン番号](files-and-version-numbers.md)」ページで説明したように、SMO アセンブリを GAC にインストールすることはできません。 これを行うと、他のアプリケーションで問題が発生する可能性があります。これらのアプリケーションは、これらのバージョンの SMO ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio など) も使用します。

## <a name="installing-the-package"></a>パッケージのインストール

Nuget パッケージのインストールと使用の手順と例については、「 [nuget クイックスタート-パッケージを使用](https://docs.microsoft.com/nuget/quickstart/use-a-package)する」を参照してください。 
  
## <a name="system-requirements"></a>システム要件
  
 SMO では、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0 または .NET Core 2.0 を実行する必要があるため、これを使用するアプリケーションでは、クライアントコンピューターのバージョンがインストールされていることを確認する必要があります。 NetFx SMO ライブラリと共にインストールされる一部のネイティブバイナリでは、VC 2013 ランタイムもインストールする必要があります。このランタイムはパッケージに含まれていません。 ターゲットアーキテクチャに適した再頒布可能パッケージを https://www.microsoft.com/download/details.aspx?id=40784 からダウンロードできます。
  
