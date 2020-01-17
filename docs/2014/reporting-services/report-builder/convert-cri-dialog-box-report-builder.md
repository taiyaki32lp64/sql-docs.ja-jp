---
title: '[CRI の変換] ダイアログ ボックス (レポート ビルダー) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10008"
helpviewer_keywords:
- CRI
- custom report items
ms.assetid: 2a3f2ac6-667e-4498-8b73-9c40beb993f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 97a6c14b9486b2cc82d514bd7a7fa8210bc22204
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107942"
---
# <a name="convert-cri-dialog-box-report-builder"></a>[CRI の変換] ダイアログ ボックス (レポート ビルダー)
  このレポートにはサポートされていない機能を持つカスタム レポート アイテム (CRI) が含まれています。 CRI は、レポートにデータを表示するカスタム オブジェクトをサポートするレポート定義言語 (RDL) の拡張機能です。 CRI には、サードパーティのソフトウェア ベンダーによって提供されるデザイン時コンポーネントおよび実行時コンポーネントが含まれます。  
  
> [!NOTE]  
>  システム管理者は、レポート サーバーでカスタム レポートをサポートするかどうかを選択します。 レポートで CRI を表示するには、CRI コンポーネントをレポートのプレビューのためにレポート作成クライアントに、およびパブリッシュまたはアップロードされたレポートを表示するためにレポート サーバーにインストールする必要があります。 詳細については、「 [Custom Report Items](../custom-report-items/custom-report-items.md)」、およびサードパーティのソフトウェア ベンダーのマニュアルを参照してください。  
  
 新しいレポート定義形式のレポート アイテムに変換できる CRI もあります。 レポートを開くときに、アップグレードするかどうかを確認するメッセージが表示されます。 次の情報に従って、このレポートの CRI を変換するかどうかを決定します。  
  
-   **[する]** 可能であればレポート内のすべての CRI を変換する場合に、 **[する]** を選択します。 CRI でサポートされていない機能はアップグレードできません。レポート定義ファイルから削除されます。 サポートされていない機能の一覧については、「 [レポートのアップグレード](../install-windows/upgrade-reports.md)」を参照してください。 レポートを表示すると、CRI がレポートに表示される方法に違いが見られます。  
  
-   **[しない]** レポートの CRI を変換しない場合に **[しない]** を選択します。 現在のバージョンでは、レポート プロセッサはこれらの CRI を表示できません。 システム管理者が、サードパーティのソフトウェア ベンダーから新しいレポート定義形式と互換性のある CRI の新しいバージョンのインストールを計画している場合、 **しない**を選択する必要があります。 新しいバージョンが使用可能になるまで、CRI はレポート内で赤い X のある空白テキスト ボックスとして表示されます。  
  
 どちらの場合でも、レポートは新しいレポート定義形式にアップグレードされ、元のレポートのバックアップ コピーは *\<Report Name>* `-` Backup.rdl として保存されます。 レポート作成ツールにレポートを保存する場合、新しいレポート定義形式でアップグレードされたレポートを保存することになります。 レポートをパブリッシュする場合、レポートはまずコンピューターに保存され、それからレポート サーバーにパブリッシュされます。 レポートのアップグレード バージョンをレポート サーバーにパブリッシュします。  
  
 レポートを保存しない場合、元のレポートは変更されません。 ただし、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンの [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] か、このレポート定義形式を使用するレポート作成環境では、このレポートは編集できません。 レポート マネージャーを使用して [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーにアップロードすることで、レポートの元のバージョンを継続して実行できます。 詳細については、「[ファイルまたはレポートのアップロード &#40;レポート マネージャー&#41;](../reports/upload-a-file-or-report-report-manager.md)」を参照してください。  
  
 レポートをレポート サーバーにパブリッシュする代わりに、アップロードする場合、レポート プロセッサはそのレポートを最初の使用時にアップグレードできるかどうかを決定します。 アップグレードできないレポートは下位互換性モードで処理され、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の以前のバージョンと同じように表示されます。 詳細については、「 [Upgrade Reports](../install-windows/upgrade-reports.md)」を参照してください。  
  
 レポート、レポート サーバー、またはレポート作成環境の現在のレポート定義形式を特定するには、「[Find the Report Definition Schema Version &#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md)」(レポート定義スキーマのバージョンを確認する &#40;SSRS&#41;) を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
