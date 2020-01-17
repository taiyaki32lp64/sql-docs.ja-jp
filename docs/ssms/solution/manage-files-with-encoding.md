---
title: エンコーディングによるファイルの管理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio]
- encoding [SQL Server Management Studio]
- files [SQL Server Management Studio], encoding
ms.assetid: 919544c9-59f0-4cc6-bb2a-f1ad671eb74b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c75981961540081d8761bfb4cdf24028b41d1071
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262827"
---
# <a name="manage-files-with-encoding"></a>エンコーディングによるファイルの管理
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
特定の言語や特定のプラットフォームでコードを正しく表示するために、特定の文字エンコードをファイルに関連付けることができます。  
  
## <a name="opening-files"></a>ファイルを開く  
ファイルの編集に使用するエディターを選択できます。  
  
#### <a name="to-open-a-file-with-a-specific-editor"></a>特定のエディターでファイルを開くには  
  
1.  **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  **[ファイルを開く]** ダイアログ ボックスでファイル名を選択します。  
  
3.  **[開く]** ボタンの横にある矢印をクリックし、表示されるメニューから **[ファイルを開くアプリケーションの選択]** をクリックします。  
  
4.  **[このファイルを開くのに使用するプログラムを選択してください]** 一覧でエディターを選択し、 **[開く]** をクリックします。 特定のエンコードでファイルを開くには、SQL クエリ エディター (エンコード付き)、XML エディター (エンコード付き) など、エンコード サポート付きのエディターを選択します。  
  
## <a name="saving-files"></a>ファイルの保存  
西ヨーロッパ言語や東ヨーロッパ言語など、さまざまな言語をサポートするために、Unicode エンコードまたは他のコード ページを指定してコードを保存することができます。 特定の言語でコードを正しく表示するためにその文字エンコードをファイルに関連付けることや、特定のオペレーティング システムをサポートするために行終端文字の種類を選択することも可能です。 また、ファイル名に使用する一部の文字は、Unicode エンコード付きでないと保存できません。  
  
#### <a name="to-save-a-file-with-a-different-encoding-or-line-ending-type"></a>他のエンコードまたは行終端文字の種類を指定してファイルを保存するには  
  
1.  **[ファイル]** メニューの **[名前を付けて <filename> を保存]** をクリックします。  
  
2.  **[ファイル名を付けて保存]** ダイアログ ボックスで、 **[保存]** ボタンを展開し、 **[エンコード付きで保存]** をクリックします。  
  
3.  **[保存オプションの詳細設定]** ダイアログ ボックスの **[エンコード]** 一覧から目的のエンコードを選択します。  
  
4.  **[行の終わり]** 一覧から目的の行終端文字の種類を選択します。  
  
    > [!NOTE]  
    > Unicode エンコードを指定してファイルを保存した場合は、そのファイルをバイナリ ファイルとして [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual SourceSafe にチェックインする必要があります。Visual SourceSafe は、Unicode で保存したファイルのマージ、比較、差分の表示をサポートしていないからです。  
  
Visual SourceSafe を使用して ANSI、UTF8、または Unicode のファイルを格納している場合は、次の制限事項に注意してください。  
  
-   ANSI ファイルでは、現在のコード ページでサポートされている文字だけを使用できます。完全には対応できない言語があります。  
  
-   Unicode ファイルはバイナリ ファイルとして処理されるので、共有チェックアウト、差分チェック、マージの各機能を使用できません。 この形式は、さまざまな言語のファイルで使用できます。  
  
-   UTF8 ファイルは、Visual SourceSafe で安全に動作しません。チェックイン、チェックアウト、差分チェック、マージの実行時に、UTF8 ファイル エディターで問題を起こす原因になる変更が加えられるためです。  
  
## <a name="see-also"></a>参照  
[ソリューションとプロジェクトを管理するためのファイル](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[ファイル拡張子をコード エディターに関連付ける](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
  
