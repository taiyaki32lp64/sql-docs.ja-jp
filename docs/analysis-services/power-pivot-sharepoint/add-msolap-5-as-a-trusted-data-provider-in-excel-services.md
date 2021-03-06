---
title: Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加する |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d7576aadda3739709acdffcb1b2419c20d39ed4e
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979454"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  MSOLAP.5 は、SQL Server 2012 用の Analysis Services OLE DB プロバイダーです。 Excel Services は、サーバー上の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データを利用可能とする接続要求を行う前に、このプロバイダーを信頼する必要があります。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツールを使用して [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint を構成した場合、このツールは要件を満たすアクションを含むため、MSOLAP.5 は、既に信頼されたプロバイダーとなっている可能性があります。 ただし、PowerShell や全体管理を使用している場合、または信頼されたプロバイダー アクションを構成ツールで除外している場合は、このプロバイダーが不足している可能性があります。その場合は、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ アクセスのファームを構成するときに、それを追加する必要があります。  
  
 この手順は、各 Excel Services サービス アプリケーションにつき 1 回実行するだけです。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint サーバーまたは Excel Services サーバーなど、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ要求を処理する物理サーバーでは、コンピューターに OLE DB プロバイダーをインストールする必要があります。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint のインストールには常に OLE DB プロバイダーが含まれていますが、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint がないコンピューターで Excel Services が実行されている場合は、プロバイダーを手動でインストールする必要があります。 詳細については、「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859)」を参照してください。  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Excel Services に信頼できるプロバイダーを追加する  
  
1.  サーバーの全体管理で、 **[アプリケーション構成の管理]** をクリックし、Excel Services サービス アプリケーションをクリックします。  
  
2.  **[信頼できるデータ プロバイダー]** をクリックします。  
  
3.  MSOLAP.5 が一覧に表示されていることを確認します。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint の構成方法によっては、MSOLAP.5 が既に信頼されている場合があります。  
  
4.  表示されない場合は、 **[信頼できるデータ プロバイダーの追加]** をクリックします。  
  
5.  [プロバイダー ID] に、「 **MSOLAP.5**」と入力します。  
  
6.  [プロバイダーの種類] では、OLE DB が選択されていることを確認します。  
  
7.  [プロバイダーの説明] に、「 **Microsoft OLE DB プロバイダー (OLAP Services 11.0 用)**」と入力します。  
  
  
