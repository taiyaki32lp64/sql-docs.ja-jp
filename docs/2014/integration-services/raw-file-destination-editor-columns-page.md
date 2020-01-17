---
title: Raw ファイル変換先エディター ([列] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledestinationcolumns.f1
ms.assetid: 37f61d0b-1269-42ee-94ab-011cbaac63e9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0f7921844b5d2281bd6ba9e51855ef37b816cc17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056576"
---
# <a name="raw-file-destination-editor-columns-page"></a>[Raw ファイル変換先エディター] ([列] ページ)
  ファイルに RAW データを書き込むための RAW ファイル変換先を構成するには、RAW ファイル変換先エディターを使用します。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [RAW ファイル変換先エディターを開く](#open)  
  
-   [[接続マネージャー] タブのオプションの設定](#connection)  
  
-   [[列] タブのオプションの設定](#mapping)  
  
##  <a name="open"></a> RAW ファイル変換先エディターを開く  
  
1.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]パッケージに RAW ファイル変換先を追加します。  
  
2.  コンポーネントを右クリックし、 **[編集]** をクリックします。  
  
##  <a name="connection"></a> [接続マネージャー] タブのオプションの設定  
 **[アクセス モード]**  
 ファイル名の指定方法を選択します。 ファイル名とパスを直接入力するには **[ファイル名]** を選択します。ファイル名を含んでいる変数を指定するには、 **[変数からのファイル名]** を選択します。  
  
 **[ファイル名]** または **[変数名]**  
 RAW ファイルの名前とパスを入力するか、またはファイル名を含んでいる変数を選択します。  
  
 **[書き込みオプション]**  
 ファイルの作成およびファイルへの書き込みに使用するメソッドを選択します。  
  
 **[初期 RAW ファイルの生成]**  
 パッケージを実行せずに、列のみを含む空の RAW ファイル (メタデータのみのファイル) を生成するには、このボタンをクリックします。 RAW ファイル ソースの参照先を、メタデータのみのファイルにすることができます。  
  
 このボタンをクリックすると、列の一覧が表示されます。 [キャンセル] をクリックして列を変更するか、[OK] をクリックしてファイルの作成を続行することができます。  
  
##  <a name="mapping"></a> [列] タブのオプションの設定  
 **使用できる入力列**  
 RAW ファイルに書き込む 1 つ以上の入力列を選択します。  
  
 **入力列**  
 **[使用できる入力列]** から選択した場合、このテーブルに入力列が自動的に追加されます。入力列をこのテーブルで直接選択することもできます。  
  
 **[出力の別名]**  
 出力列に使用する代替名を指定します。  
  
## <a name="see-also"></a>参照  
 [RAW ファイル変換先](data-flow/raw-file-destination.md)  
  
  
