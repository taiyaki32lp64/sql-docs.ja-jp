---
title: ブックが保存されている信頼できる場所で、外部データ接続が許可されていません。 次の接続の更新に失敗しました:PowerPivot データ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b10a4a80b74bf64741784edc4fc1974dc0464805
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070976"
---
# <a name="the-trusted-location-where-the-workbook-is-stored-does-not-allow-external-data-connections-the-following-connections-failed-to-refresh-powerpivot-data"></a>ブックが保存されている信頼できる場所で、外部データ接続が許可されていません。 次の接続の更新に失敗しました:[PowerPivot データ]
  PowerPivot データを含む Excel ブックで、Excel Services は、埋め込みデータ ソースに接続できない場合にこのエラーを返します。  
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|対象|PowerPivot for SharePoint|  
|製品バージョン|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|外部データ アクセスを拒否するように Excel Services が構成されています。|  
|メッセージ テキスト|ブックが保存されている信頼できる場所で、外部データ接続が許可されていません。 次の接続の更新に失敗しました:[PowerPivot データ]|  
  
## <a name="explanation"></a>説明  
 PowerPivot ブックには、埋め込みデータ接続が含まれています。 スライサーやフィルターを介したブックの操作をサポートするには、埋め込まれている接続情報を使用した外部データ アクセスを許可するように Excel Services を構成する必要があります。 外部データ アクセスは、ファームの PowerPivot サーバーに読み込まれる PowerPivot データを取得するのに必要です。  
  
## <a name="user-action"></a>ユーザーの操作  
 埋め込みデータ ソースを許可するように構成設定を変更します。  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  **[Excel Services アプリケーション]** をクリックします。  
  
3.  **[信頼できるファイル保存場所]** をクリックします。  
  
4.  **[http://]** または構成する場所をクリックします。  
  
5.  [外部データ] の [外部データの許可] で、 **[信頼できるデータ接続ライブラリと、埋め込まれている接続]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
 または、PowerPivot ブックが含まれるサイト用に新しく信頼できる場所を作成し、そのサイトの構成設定だけを変更することもできます。 詳細については、「 [サーバーの全体管理での PowerPivot サイト用の信頼できる場所の作成](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)」を参照してください。  
  
  
