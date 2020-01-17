---
title: データベースの記憶域の場所 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2dd3659aed11e4e1cee791fcb5e541471320c82a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075899"
---
# <a name="database-storage-location"></a>データベースの格納場所
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータベース管理者 (DBA) が特定のデータベースをサーバー データ フォルダー以外の場所に配置することは少なくありません。 こうした状況は、パフォーマンスの向上やストレージの拡張などのビジネス上のニーズによって頻繁に発生します。 このような場合は、`DbStorageLocation` データベース プロパティを使用すると、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の DBA はローカル ディスクまたはネットワーク デバイス内にデータベースの格納場所を指定できます。  
  
## <a name="dbstoragelocation-database-property"></a>DbStorageLocation データベース プロパティ  
 `DbStorageLocation` データベース プロパティでは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって作成および管理されるすべてのデータベースのデータ ファイルとメタデータ ファイルのフォルダーを指定します。 メタデータ ファイルはすべて `DbStorageLocation` フォルダーに格納されますが、例外として、データベースのメタデータ ファイルはサーバー データ フォルダーに格納されます。 `DbStorageLocation` データベース プロパティの値を設定する場合は、重要な注意点が 2 つあります。  
  
-   `DbStorageLocation` データベース プロパティには、既存の UNC フォルダー パスまたは空の文字列を設定する必要があります。 空の文字列は、サーバー データ フォルダーを示す既定値です。 フォルダーが存在しない場合、`Create` コマンド、`Attach` コマンド、`Alter` コマンドを実行するとエラーが発生します。  
  
-   `DbStorageLocation` データベース プロパティは、サーバー データ フォルダーまたはそのサブフォルダーを指すように設定することはできません。 サーバー データ フォルダーまたはそのサブフォルダーを指した場合、`Create` コマンド、`Attach` コマンド、`Alter` コマンドを実行するとエラーが発生します。  
  
> [!IMPORTANT]  
>  固有の UNC パスを設定して、Storage Area Network (SAN)、iSCSI ベースのネットワーク、またはローカルにアタッチされたディスクを使用することをお勧めします。 ネットワーク共有への UNC パスや、待機時間の長いリモート ストレージ ソリューションは、サポートされないインストールにつながります。  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>DbStorageLocation と StorageLocation の比較  
 `DbStorageLocation` は、すべてのデータベースのデータ ファイルとメタデータ ファイルが存在するフォルダーを指定します。一方、`StorageLocation` は、キューブのパーティションが存在するフォルダーを指定します。 `StorageLocation` は、`DbStorageLocation` とは別に設定できます。 これは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の DBA が予想した結果に基づいて決定します。また、どちらか一方のプロパティが何度も重複して使用されます。  
  
## <a name="dbstoragelocation-usage"></a>DbStorageLocation の使用方法  
 `DbStorageLocation`データベース プロパティの一部として使用されます、`Create`データベース コマンドを`Detach` / `Attach`データベース コマンド シーケンス、 `Backup` / `Restore`データベース コマンド シーケンス、または、`Synchronize`データベース コマンド。 `DbStorageLocation` データベース プロパティの変更は、データベース オブジェクトの構造の変更と見なされます。 つまり、すべてのメタデータを再作成し、データを再処理する必要があります。  
  
> [!IMPORTANT]  
>  `Alter` コマンドを使用して、データベースの格納場所を変更しないでください。 シーケンスを使用すること勧め代わりに、 `Detach` / `Attach`データベース コマンド (を参照してください[Analysis Services データベースの移動](move-an-analysis-services-database.md)、 [にAnalysisServicesデータベースをデタッチとアタッチ](attach-and-detach-analysis-services-databases.md)).  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Analysis Services データベースのインポートとデタッチ](attach-and-detach-analysis-services-databases.md)   
 [Analysis Services データベースの移動](move-an-analysis-services-database.md)   
 [DbStorageLocation 要素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)   
 [Create 要素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)   
 [Attach 要素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Synchronize 要素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)  
  
  
