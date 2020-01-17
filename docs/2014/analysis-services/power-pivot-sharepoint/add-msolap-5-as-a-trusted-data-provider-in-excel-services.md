---
title: Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9095c1fa767e1854c300df1ad08bf5d1900af860
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071928"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加
  MSOLAP.5 は、SQL Server 2012 用の Analysis Services OLE DB プロバイダーです。 Excel Services は、サーバー上の PowerPivot データを利用可能とする接続要求を行う前に、このプロバイダーを信頼する必要があります。  
  
 PowerPivot 構成ツールを使用して PowerPivot for SharePoint を構成した場合、このツールは要件を満たすアクションを含むため、MSOLAP.5 は、既に信頼されたプロバイダーとなっている可能性があります。 ただし、PowerShell や全体管理を使用している場合、または信頼されたプロバイダー アクションを構成ツールで除外している場合は、このプロバイダーが不足している可能性があります。その場合は、PowerPivot データ アクセスのファームを構成するときに、それを追加する必要があります。  
  
 この手順は、各 Excel Services サービス アプリケーションにつき 1 回実行するだけです。  
  
 PowerPivot for SharePoint サーバーまたは Excel Services サーバーなど、PowerPivot データ要求を処理する物理サーバーでは、コンピューターに OLE DB プロバイダーをインストールする必要があります。 PowerPivot for SharePoint のインストールには常に OLE DB プロバイダーが含まれていますが、PowerPivot for SharePoint がないコンピューターで Excel Services が実行されている場合は、プロバイダーを手動でインストールする必要があります。 「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Excel Services に信頼できるプロバイダーを追加する  
  
1.  サーバーの全体管理で、 **[アプリケーション構成の管理]** をクリックし、Excel Services サービス アプリケーションをクリックします。  
  
2.  **[信頼できるデータ プロバイダー]** をクリックします。  
  
3.  MSOLAP.5 が一覧に表示されていることを確認します。 PowerPivot for SharePoint の構成方法によっては、MSOLAP.5 が既に信頼されている場合があります。  
  
4.  表示されない場合は、 **[信頼できるデータ プロバイダーの追加]** をクリックします。  
  
5.  [プロバイダー ID] に、「`MSOLAP.5`」と入力します。  
  
6.  [プロバイダーの種類] では、OLE DB が選択されていることを確認します。  
  
7.  [プロバイダーの説明] に、「 **Microsoft OLE DB プロバイダー (OLAP Services 11.0 用)** 」と入力します。  
  
  
