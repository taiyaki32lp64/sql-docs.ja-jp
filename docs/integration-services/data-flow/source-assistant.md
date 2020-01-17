---
title: ソース アシスタント | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0312349652ad1854efdeacdbfc25726e1766862f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298036"
---
# <a name="source-assistant"></a>ソース アシスタント

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  変換元アシスタント コンポーネントを使用すると、変換元コンポーネントおよび接続マネージャーを作成できます。 このコンポーネントは、SSIS ツールボックスの **[お気に入り]** セクションにあります。  
  
> [!NOTE]  
>  変換元アシスタントは、Integration Services 接続プロジェクトと対応するウィザードに置き換わるものです。  
  
## <a name="add-a-source-with-source-assistant"></a>ソース アシスタントを使用してソースを追加する
このセクションでは、変換元アシスタントを使用して新しい変換元を追加する手順について説明します。また、 **[新しい変換元の追加]** ダイアログで使用できるオプションもリストします。このダイアログは、変換元アシスタントを SSIS デザイナーにドラッグ アンド ドロップしたときに表示されます。  

1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、変換元コンポーネントを追加する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **変換元アシスタント** コンポーネントを SSIS ツールボックスから **[データ フロー]** タブにドラッグします。 **[新しい変換元の追加]** ダイアログ ボックスが表示されます。 次のセクションでは、ダイアログ ボックスで使用できるオプションについて詳しく説明します。  
  
3.  **[種類]** 一覧で、変換先の種類を選択します。  
  
4.  **[接続マネージャー]** 一覧で既存の接続マネージャーを選択するか、 **[\<新規作成>]** を選択して新しい接続マネージャーを作成します。  
  
5.  既存の接続マネージャーを選択した場合は、 **[OK]** をクリックして **[新しい変換先の追加]** ダイアログ ボックスを閉じます。 変換先と接続マネージャーがデータ フローに追加されます。  
  
6.  **[\<新規作成>]** をクリックして新しい接続マネージャーを作成する場合は、 **[接続マネージャー]** ダイアログ ボックスが表示され、接続のパラメーターを指定できます。 新しい接続マネージャーの作成が完了すると、変換先と接続マネージャーが SSIS デザイナーに表示されます。  

## <a name="add-new-source-dialog-box"></a>[新しいソースの追加] ダイアログ ボックス
次の表に、 **[新しいソースの追加]** ダイアログ ボックスで使用できるオプションをリストします。  
  
|オプション|[説明]|  
|------------|-----------------|  
|型|接続先のソースの種類を選択します。|  
|接続マネージャー|既存の接続マネージャーを選択するか、 **[\<新規作成>]** をクリックして新しい接続マネージャーを作成します。|  
|インストールされているもののみを表示する|インストールされているソースのみを表示するかどうかを指定します。|  
|[OK]|変更を保存し、後続のダイアログ ボックスを開いてその他のオプションを構成する場合にクリックします。| 
  
