---
title: ナレッジ ベースへのナレッジの追加 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c9122db448e95a6734ea3cf3c1010665b60f4650
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481185"
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>ナレッジ ベースへのナレッジの追加
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) のナレッジ ベースにナレッジを追加する方法について説明します。 データ品質操作を実行するには、データに関するナレッジを事前に用意しておく必要があります。 このナレッジを取得するには、データ品質ナレッジ ベースを構築および管理し、特定の種類のデータ ソースに関連するナレッジをそのナレッジベースに追加します。 ナレッジ ベースはデータに関するナレッジのリポジトリです。ナレッジ ベースを使用して、データを理解し、その整合性を維持できます。  
  
 ナレッジ ベースには、データ ソースに関連するデータ ドメインが含まれています。 DQKB には、データ ドメインごとに、データ ソースに対するデータ品質操作の実行に使用できる識別された用語、スペル ミス、検証ルールとビジネス ルール、および参照データがすべて格納されます。 DQS は、正しくないデータまたは無効なデータの識別や照合の実行にこのナレッジを使用します。  
  
 ナレッジは、次に示すコンピューター支援型または対話型の手法でナレッジ ベースに追加できます。  
  
-   [ナレッジ検出の実行](#Discovery)  
  
-   [ドメイン内のデータ値の管理](#ManageDomain)  
  
-   [.dqs ファイルからのナレッジのインポート](#DQSFile)  
  
-   [Excel ファイルからのナレッジのインポート](#Excel)  
  
-   [プロジェクトからナレッジ ベースへのナレッジの再インポート](#Project)  
  
-   [既定の DQS ナレッジ ベースの使用](#Default)  
  
##  <a name="Discovery"></a> ナレッジ検出の実行  
 ナレッジ検出では、データ品質基準を取得するためにデータのサンプルを分析し、取得したナレッジをナレッジ ベースに追加します。 これは、データの不整合と構文エラーを識別し、データへの変更を提案するコンピューター支援型のプロセスです。 ナレッジ検出アクティビティは、ドメイン値を対話的に管理できるページを含むウィザードです。  
  
-   ドキュメント化された詳細情報については、「 [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md)」を参照してください。  
  
-   ナレッジ検出の実行方法を示すビデオについては、 [ここ](https://msdn.microsoft.com/sqlserver/hh323825.aspx)をクリックしてください。  
  
##  <a name="ManageDomain"></a> ドメイン内のデータ値の管理  
 DQS では、コンピューター支援型のナレッジ検出アクティビティで生成されたメタデータを対話的に変更および拡張することができます。 これはドメイン管理アクティビティで行います。ドメイン管理アクティビティでは、特定のデータ値に変更を適用することができます。  
  
-   ドキュメント化された詳細情報については、「 [Change Domain Values](../../2014/data-quality-services/change-domain-values.md)」を参照してください。  
  
-   ドメイン管理の実行方法を示すビデオについては、 [ここ](https://msdn.microsoft.com/sqlserver/hh323825.aspx)をクリックしてください。 このビデオでは、ナレッジ検出ウィザードの [ドメイン値の管理] ページでドメイン値を変更します。 この手順は、ドメイン管理アクティビティの [ドメイン値] ページでも行うことができます。  
  
##  <a name="DQSFile"></a> .dqs ファイルからのナレッジのインポート  
 .dqs データ ファイルから既存のナレッジ ベースにドメインをインポートしたり、.dqs から新しいナレッジ ベースにナレッジ ベース全体をインポートしたりできます。 これを行うには、まず既存のドメインまたはナレッジ ベースを .dqs ファイルにエクスポートする必要があります。 ドメインを含む .dqs ファイルには、ドメインのすべてのデータが格納されています。ナレッジ ベースを含む .dqs ファイルには、ドメインや照合ポリシーを含むナレッジ ベースのすべての情報が格納されています。  
  
-   ドキュメントについて詳しくは、「[.dqs ファイルからのドメインのインポート](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md)」または「[.dqs ファイルからのナレッジ ベースのインポート](../../2014/data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)」をご覧ください。  
  
##  <a name="Excel"></a> Excel ファイルからのナレッジのインポート  
 Excel スプレッドシート ファイルから既存のドメインまたはナレッジ ベースにドメイン値をインポートできます。 これを行うには、まずインポートするドメイン値を含む Excel スプレッドシートを作成し、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] を使用して値をインポートできるように Excel が [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]コンピューターにインストールされていることを確認する必要があります。 ドメインまたはナレッジ ベースから Excel ファイルにドメイン値をエクスポートすることはできません。  
  
-   ドキュメントについて詳しく、「[値を Excel ファイルからドメインへインポートする](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md)」または「[ナレッジ検出でドメインを Excel ファイルからインポートする](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)」をご覧ください。  
  
##  <a name="Project"></a> プロジェクトからナレッジ ベースへのナレッジの再インポート  
 ナレッジ ベースを使用してクレンジングまたは照合データ品質プロジェクトを実行した後、クレンジングまたは照合中に作成されたナレッジをそのナレッジ ベースに再インポートできます。 これにより、プロジェクト中に生成されたナレッジを保持し、ナレッジ ベースにナレッジを継続的に構築することができます。  
  
-   ドキュメントについて詳しくは、「[ドメインへのクレンジング プロジェクトの値のインポート](../../2014/data-quality-services/import-cleansing-project-values-into-a-domain.md)」をご覧ください。  
  
##  <a name="Default"></a> 既定の DQS ナレッジ ベースの使用  
 DQS には、DQS データと呼ばれる構築済みのナレッジ ベースが同梱されています。このナレッジ ベースには、米国の会社および住所データのドメインが含まれています。 このナレッジ ベースを使用すると、新しいナレッジ ベースを作成することなく、プロジェクトをすばやく開始できます。 DQS データ ナレッジ ベースは読み取り専用ですが、データ スチュワードはこれに基づいて新しいナレッジ ベースを作成できます。  
  
-   ドキュメント化された詳細情報については、「 [Using the DQS Default Knowledge Base](../../2014/data-quality-services/using-the-dqs-default-knowledge-base.md)」を参照してください。  
  
  
