---
title: '手順 1: Visual Basic プロジェクトを設定する |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce9e337a1ea45db851bafd32e0af476ae33fd3c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798800"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>手順 1: Visual Basic プロジェクトを設定する
このシナリオである Microsoft Visual Basic 6.0、ADO 2.5 またはそれ以降、および Microsoft OLE DB Provider for Internet Publishing がシステムにインストールされていると見なされます。 まず、新しいプロジェクトを作成して、プロジェクトで既定のフォームをいくつかのコントロールを追加します。  
  
### <a name="to-create-an-ado-project"></a>ADO プロジェクトを作成します。  
  
1.  Microsoft Visual Basic では、新しい標準 EXE プロジェクトを作成します。  
  
2.  [プロジェクト] メニューからの参照を選択します。  
  
3.  「Microsoft ActiveX データ オブジェクト 2.5 ライブラリ」を選択し、[ok] をクリックします。  
  
### <a name="to-insert-controls-on-the-main-form"></a>メイン フォームのコントロールを挿入するには。  
  
1.  Form1 に ListBox コントロールを追加します。 その名前のプロパティを設定**lstMain**します。  
  
2.  Form1 にもう 1 つの ListBox コントロールを追加します。 その名前のプロパティを設定**lstDetails**します。  
  
3.  Form1 に TextBox コントロールを追加します。 その名前のプロパティを設定**txtDetails**します。  
  
## <a name="see-also"></a>参照  
 [インターネットのシナリオへの発行](../../../ado/guide/data/internet-publishing-scenario.md)   
 [手順 2: Main リスト ボックスを初期化する](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
