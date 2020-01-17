---
title: SharePoint リストのデータフィードのエクスポートをサポートするために ADO.NET Data Services をインストールする |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b9b3ec2d8b7459f9d66313c6a40b1cbc26450e0d
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952166"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>SharePoint リストのデータ フィードのエクスポートをサポートする ADO.NET Data Services のインストール
  ADO.NET Data Services は、SharePoint リストのデータ フィードのエクスポートに必要です。 SharePoint 2010 では、このコンポーネントは SharePoint の必須コンポーネントのインストーラー プログラムに含まれていないため、手動でインストールする必要があります。  
  
 この前提条件がなければ、データフィードとしてエクスポートされた SharePoint リストを使用しようとすると、次のエラーが表示されます。"セキュリティ上の理由から、DTD はこの XML ドキュメントでは禁止されています。 XmlReaderSettings の ProhibitDtd プロパティを false に設定し、その設定を XmlReader.Create メソッドに渡してください。"  
  
 次の手順に従って、リストをデータ フィードとしてエクスポートできるようにする各 SharePoint サーバーに ADO.NET Data Services をインストールします。  
  
### <a name="download-and-install-adonet-data-services"></a>ADO.NET Data Services のダウンロードとインストール  
  
1.  SharePoint 2010 のハードウェアとソフトウェアの要件に関するドキュメント「[ハードウェアとソフトウェアの要件 (sharepoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734) 」を参照してください。  
  
2.  **[適用可能なソフトウェアへのアクセス]** で、使用しているオペレーティングシステム (windows SERVER 2008 SP2 または windows Server 2008 R2) に対応する ADO.NET Data Services 3.5 のリンクを見つけます。  
  
3.  リンクをクリックし、サービスをインストールするセットアップ プログラムを実行します。  
  
## <a name="see-also"></a>関連項目  
 [PowerPivot for SharePoint 2010 のインストール](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
