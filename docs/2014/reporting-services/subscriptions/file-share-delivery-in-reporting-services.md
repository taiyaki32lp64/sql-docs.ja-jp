---
title: Reporting Services でのファイル共有の配信 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d3d042530f69d34fde377ffc7c6e0a9200b9cc48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100908"
---
# <a name="file-share-delivery-in-reporting-services"></a>Reporting Services でのファイル共有の配信
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、フォルダーへのレポートの配信を可能にするファイル共有配信拡張機能が用意されています。 ファイル共有配信拡張機能は既定で使用できるため、追加で構成する必要はありません。 ファイルの配信を正常に実行するためには、共有フォルダーに書き込みアクセス権を設定する必要があります。 また、レポートへのアクセスを要求するユーザーは、共有フォルダーの読み取り権限を持っている必要があります。  
  
 ファイル共有にレポートを配信するには、標準のサブスクリプションまたはデータ ドリブン サブスクリプションを定義します。 配信へのサブスクライブおよび配信の要求は、一度に 1 つのレポートに対してのみ実行できます。 データ ドリブン サブスクリプションでファイル共有配信を使用する方法については、「[データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)」を参照してください。 また、リモート ファイル共有サブスクリプションを実行するアカウントには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンピューターに対するローカル ログオン権限が必要です。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード|  
  
 このトピックの内容  
  
-   [共有フォルダーに配信されるレポートの特性](#bkmk_Characteristics)  
  
-   [ターゲット フォルダー](#bkmk_target_folders)  
  
-   [ファイル形式](#bkmk_file_formats)  
  
-   [ファイル オプション](#bkmk_file_options)  
  
##  <a name="bkmk_Characteristics"></a> 共有フォルダーに配信されるレポートの特性  
 レポート サーバーによってホストおよび管理されるレポートとは異なり、共有フォルダーに配信されるレポートは静的なファイルです。 レポート用に定義されている対話機能は、ファイル システムにファイルとして保存されているレポートには使用できません。 対話機能は、静的要素として表現されます。 たとえば、マトリックス形式のレポートを配信する場合は、レポートのトップレベルのビューが表示されます。行および列を拡張して、サポートしているデータを表示することはできません。 レポートにグラフが含まれている場合は、既定の表示方法が使用されます。 レポートが別のレポートへリンクしている場合は、リンクは静的なテキストとして表示されます。 配信したレポートで対話機能を保持するには、代わりに電子メール配信を使用します。 詳細については、「 [Reporting Services の電子メール配信](e-mail-delivery-in-reporting-services.md)」を参照してください。  
  
##  <a name="bkmk_target_folders"></a> ターゲット フォルダー  
 ファイル共有の配信を使用するサブスクリプションを定義する場合には、対象フォルダーとして既存のフォルダーを指定する必要があります。 レポート サーバーでは、ファイル システムにフォルダーを作成しません。 指定するフォルダーは、ネットワーク接続を使用してアクセス可能である必要があります。  
  
 共有フォルダーでレポートを表示するユーザーに読み取り権限があることを確認します。  
  
 サブスクリプションで対象フォルダーを指定する場合、コンピューターのネットワーク名を含む汎用名前付け規則 (UNC) 形式を使用してください。 フォルダー パスの末尾には円記号 (バックスラッシュ) を含めないでください。 以下に、UNC パスの例を示します。  
  
```  
\\<servername>\reportarchive\operations\2003  
```  
  
 フォルダーを作成するときに、必要な接続の上限を検討します。 レポート サーバーに必要な接続数は 2 つですが、共有フォルダーでレポートを開く追加のユーザーに対応できるように、十分な接続数を指定する必要があります。  
  
##  <a name="bkmk_file_formats"></a> ファイル形式  
 レポートは、HTML や Excel などさまざまなファイル形式で表示されます。 レポートを特定の形式で保存するには、サブスクリプションの作成時に表示形式を選択します。 たとえば **Excel** を選択すると、レポートは [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ファイルとして保存されます。 サポートされている任意の表示形式を選択できますが、一部の形式はファイルの生成で他の形式より優れています。  
  
 ファイル共有配信を使用する場合は、すべての画像および関連するコンテンツが含まれているレポートを、単一のファイルで配信する形式を選択します。 適切な形式は、Web アーカイブ、PDF、TIFF、Excel などです。 HTML4.0 は避けてください。 レポートに画像が含まれている場合、HTML 4.0 形式のファイルにその画像が含まれるようには処理されません。  
  
##  <a name="bkmk_file_options"></a> ファイル オプション  
 サブスクリプションを作成する場合は、ファイル名の作成方法と、更新ごとに新しいバージョンに置き換えるかどうかを指定するオプションを選択できます。 完全修飾ファイル名は、名前、拡張子、およびファイルに付加されるテキストや数値という 3 つの要素で構成されて一意のファイル名が形成されます。 テキストまたは数値をファイル名に追加するかどうかは、上書きオプションによって決まります。  
  
 ファイル名はレポート名に基づいて生成されますが、サブスクリプションでは独自の名前を指定することもできます。 拡張子は省略可能です。拡張子を使用する場合は、表示形式に対応する拡張子がレポート サーバーによって生成されます。  
  
 上書きオプションを指定すると、毎回のレポート配信または新規ファイルの作成時に同じファイル名を再利用できます。 ファイルを上書きするには、同じファイル名と拡張子を使用する必要があります。  
  
 配信ごとに一意のファイルを作成するための別の方法として、ファイル名にタイムスタンプを含める方法があります。 これを行うには、追加、`@timestamp`変数にファイル名 (たとえば、 *CompanySales@timestamp* )。 この方法を使用すると、一意のファイル名が生成されるので、上書きされることはありません。  
  
## <a name="see-also"></a>参照  
 [作成、変更、および標準のサブスクリプションを削除&#40;Reporting Services のネイティブ モード&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
