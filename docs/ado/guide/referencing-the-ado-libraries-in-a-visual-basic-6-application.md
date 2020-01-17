---
title: Visual Basic 6 アプリケーションで ADO ライブラリを参照する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25ea858995c884af202d3d80f4de675c9f4cda27
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923057"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Visual Basic 6 アプリケーションで ADO ライブラリを参照する
Microsoft Visual Basic 6 アプリケーションには、ADO ライブラリをインポートするには、Visual Basic プロジェクトで参照を設定する必要があります。  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Visual Basic プロジェクトで ADO ライブラリへの参照を設定するには  
  
1.  新しいを作成するか、既存の Visual Basic プロジェクトを開きます。  
  
2.  をクリックして、**プロジェクト**クリックしてメニュー項目**参照.** ドロップダウン メニューのパネルから。  
  
3.  **使用可能な参照**、チェック ボックスをオン**Microsoft ActiveX Data Objects *n.n*ライブラリ**ここで、 ***n.n***最新を表しますバージョン番号です。 **場所**下にあるフィールドとして選択したを識別する必要があります *$installDir\msado15.dll*ここで、 *$installDir*先のディレクトリのパスを表す、ADO ライブラリインストールされています。  
  
4.  ADO MD を使用する場合は、手順 3 を繰り返し選択 **Microsoft ActiveX Data Objects (多次元) *n.n* ライブラリ** します。 **場所**フィールドとしてこの選択肢を識別する必要があります *$installDir\msadomd.dll*します。  
  
5.  ADOX を使用する場合は、手順 3 を繰り返し選択 **Microsoft ADO 内線 *n.n* DDL とセキュリティの** します。 **場所**フィールドとしてこの選択肢を識別する必要があります *$installDir\msadox.dll*します。  
  
6.  クリックして**OK**参照の設定を完了します。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ADO をインストールすると、次のタイプ ライブラリの以前のバージョンもコピーします。  
  
-   *msado27.tlb*、ADO 2.7 タイプ ライブラリ  
  
-   *msado26.tlb*、ADO 2.6 のタイプ ライブラリ  
  
-   *msado25.tlb*、ADO 2.5 のタイプ ライブラリ  
  
-   *msado21.tlb*、ADO 2.1 のタイプ ライブラリ  
  
-   *msado20.tlb*、ADO 2.0 のタイプ ライブラリ  
  
 アプリケーションは、旧バージョンと互換性の理由からこれらの ADO ライブラリのいずれかを使用する必要がありますは、タイプ ライブラリの適切なバージョンをインポートする必要があります。 これを行うには、前のセクションの手順に従います置き換え*msado15.dll*によって*msadoXX.tlb*ここで、 *XX*をインポートする必要があります。 バージョン番号を表します。
