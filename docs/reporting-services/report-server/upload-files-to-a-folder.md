---
title: "フォルダーにファイルをアップロード |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b4a7d4a5babf6789baa551f808b840c469dfa31a
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="upload-files-to-a-folder"></a>フォルダーへのファイルのアップロード
  ファイル システムからファイルをアップロードし、それらを管理対象アイテムとしてレポート サーバー データベースに格納できます。 ファイルのアップロード時に行われる処理は、ファイルの種類によって異なります。  
  
-   .rdl ファイルのアップロードは、レポートのパブリッシュと同等です。  
  
-   その他のファイルをアップロードすると、アップロードしたファイルが単一のバイナリ オブジェクトとしてレポート サーバー データベースに追加されます。 これらのファイルは、リソースとしてレポート サーバーにパブリッシュされます。 リソースのファイルの種類には指定がありません。 ファイルの拡張子が既知の MIME の種類に一致する場合、リソースの種類を識別するために、その MIME の種類のアイコンが使用されます。 ファイルの拡張子が未登録の場合、リソースは汎用ファイル アイコンで示されます。  
  
> [!NOTE]  
>  レポート データ ソース (.rds) ファイルをアップロードして共有データ ソースを作成することはできません。 .rds ファイルは、レポート デザイナーでのみ使用されます。 レポート マネージャーで定義および管理する共有データ ソース アイテムのコンテンツを、このファイルから提供することはできません。 アップロードする代わりに、.rds ファイルを基に共有データ ソースを作成するスクリプトを記述することができます。  
  
 アップロードするアイテムの最大ファイル サイズは [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]によって決まります。 既定の最大サイズは 4 MB です。  
  
 視覚的には、レポート サーバー データベースにアップロードしたファイルは、以下のアイコンでフォルダー階層に表示されます。  
  
 ![レポート アイコン](../../reporting-services/report-server/media/hlp-16doc.gif "レポート アイコン")  
レポート アイコン  
  
 ![モデル アイコン](../../reporting-services/report-server/media/model-icon.gif "モデル アイコン")  
レポート モデル アイコン  
  
 ![汎用リソース アイコン](../../reporting-services/report-server/media/hlp-16file.gif "汎用リソース アイコン")  
汎用リソース アイコン  
  
 ファイルをアップロードすると、ファイルは常に、現在選択しているフォルダーに格納されます。 最初に、アイテムを含めるフォルダーに移動できます。また、ファイルをアップロードしてから最終的な場所にファイルを移動することもできます。  
  
 ファイルをアップロードするには、レポート マネージャーを使用します。 レポート サーバーにファイルをアップロードできるかどうかは、ロールの割り当てを構成するタスクによって異なります。 既定のセキュリティを使用している場合は、ローカル管理者によってレポート サーバーにアイテムを追加できます。 個人用レポートが有効である場合は、個人用レポート フォルダーを持っているすべてのユーザーに、そのフォルダーへアイテムをアップロードする権限が与えられます。 カスタム ロールの割り当てを使用している場合は、フォルダー管理をサポートするタスクがロールの割り当てに含まれている必要があります。  
  
|目的|含まれるタスク|  
|----------------|-------------------------|  
|.rdl ファイルをフォルダーにアップロード|レポートの管理|  
|任意のファイルをバイナリ オブジェクトとしてアップロード|リソースの管理|  
|フォルダーのコンテンツの表示|リソースの表示、レポートの表示|  
  
## <a name="see-also"></a>参照  
 [レポート マネージャーと &#40; です。SSRS ネイティブ モードと &#41; です。](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [ネイティブ モード レポート サーバーに対する権限の許可](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [タスクと権限](../../reporting-services/security/tasks-and-permissions.md)   
 [ファイルまたはレポート &#40; をアップロードします。レポート マネージャー &#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)  
  
  