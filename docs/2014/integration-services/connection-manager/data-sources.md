---
title: データ ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Integration Services], about data sources
ms.assetid: 7ac81612-9822-470f-8d0f-a1dc96142fe3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5fa4a428c1d1f290ceadee19d21f3b8f0b8bd942
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833847"
---
# <a name="data-sources"></a>ソリューション エクスプローラー
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] には、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージで使用できるデザイン時のオブジェクト (データ ソース) が含まれています。  
  
 データ ソース オブジェクトは接続への参照であり、少なくとも接続文字列とデータ ソース識別子が含まれています。 また、説明、名前、ユーザー名、パスワードなどの追加メタデータを含むこともできます。  
  
> [!NOTE]  
>  データ ソースは、パッケージ配置モデルを使用するように構成されているプロジェクトにのみ追加できます。 プロジェクト配置モデルを使用するようにプロジェクトが構成されている場合は、データ ソースを使用する代わりに、プロジェクト レベルで作成された接続マネージャーを使用して接続を共有します。  
>   
>  配置モデルの詳細については、「 [Deployment of Projects and Packages](../packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。 プロジェクト配置モデルへのプロジェクトの変換の詳細については、「[Integration Services サーバーへのプロジェクトの配置](../deploy-projects-to-integration-services-server.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージでデータ ソースを使用する場合、次の利点があります。  
  
-   データ ソースにはプロジェクト スコープがあるため、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクト内で作成されたデータ ソースは、そのプロジェクト内のすべてのパッケージで利用できます。 データ ソースを一度定義すると、複数パッケージの接続マネージャーで参照できます。  
  
-   データ ソースは、データ ソース オブジェクトと、そのパッケージ参照との間を同期します。 データ ソースとそのデータ ソースを参照するパッケージが同じプロジェクトに存在する場合、データ ソース参照の接続文字列のプロパティは、データ ソースが変更されるときに自動的に更新されます。  
  
## <a name="reference-data-sources"></a>データ ソースを参照する  
 データ ソース オブジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトに追加するには、 **ソリューション エクスプローラー** で **[データ ソース]** フォルダーを右クリックし、 **[新しいデータ ソース]** をクリックします。 アイテムが **[データ ソース]** フォルダーに追加されます。 別のプロジェクトで作成されたデータ ソース オブジェクトを使用する場合は、まず、そのデータ ソース オブジェクトをプロジェクトに追加する必要があります。  
  
 パッケージ内でデータ ソース オブジェクトを使用するには、そのデータ ソース オブジェクトを参照する接続マネージャーをパッケージに追加します。 パッケージ制御フローおよびデータ フローを構築する前に接続マネージャーをパッケージに追加するか、制御フローまたはデータ フローを構築する手順の中で接続マネージャーを追加することができます。  
  
 データ ソース オブジェクトはデータ ソースへの単純な接続を表し、参照するデータ ストア内のオブジェクトへのアクセスを提供します。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の AdventureWorks サンプル データベースに接続するデータ ソース オブジェクトには、データベースにある 60 のテーブルすべてが含まれます。  
  
 データ ソースと、そのデータ ソースを参照する接続マネージャーとの間に、依存関係はありません。 データ ソースがプロジェクトの一部ではなくなった場合でも、パッケージは引き続き有効です。接続の種類や接続文字列などのデータ ソースに関する情報は、パッケージ定義に含まれているためです。  
  
  
