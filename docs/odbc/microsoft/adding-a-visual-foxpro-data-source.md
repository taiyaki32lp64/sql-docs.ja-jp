---
title: Visual FoxPro データ ソースの追加 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5203a7216faa008aade21c4e3e1dc54fc794461b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901440"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Visual FoxPro データ ソースの追加
アプリケーションから Visual FoxPro データにアクセスするには、データ ソースが必要です。 次のように、データ ソースを作成できます。  
  
-   Microsoft® Word、Excel、または Microsoft Access などのアプリケーションでは、ODBC ドライバーを使用します。  
  
-   、アプリケーションの外部には、Microsoft Windows® 95、Microsoft Windows 98、または Microsoft Windows と Windows 2000 のコントロール パネルを使用します。  
  
 データ ソースがシステムに存在する後、Visual FoxPro データにアクセスするたびに、同じデータ ソース再を利用できます。 いくつかの異なるデータベースまたはテーブルにアクセスする場合は、データベースまたはディレクトリごとに個別のデータ ソースを作成できます。  
  
 次の手順では、コントロール パネルを使用してデータ ソースを作成します。 アプリケーションからデータ ソースを作成する方法の詳細については、次を参照してください。 [Visual FoxPro データから Microsoft Office へのアクセス](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)します。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Visual FoxPro データ ソースを追加するには  
  
1.  Windows 2000 を実行しているコンピューターで、Windows コントロール パネルを開きし、管理ツールをダブルクリックします。  
  
2.  ODBC データ ソース アドミニストレーター ダイアログ ボックスを開きますデータ ソース (ODBC) をダブルクリックします。 このアイコンは、Visual FoxPro ODBC ドライバーまたは ODBC ドライバー ソフトウェアをインストールした後に使用できます。  
  
    > [!NOTE]  
    >  以前のバージョンの Windows を実行している場合は、Windows コントロール パネルを開き 32 ビット ODBC と ODBC、ODBC データ ソース アドミニストレーター ダイアログ ボックスを開くをダブルクリックします。  
  
3.  [追加] をクリックします。  
  
4.  データ ソースの新規作成 ダイアログ ボックスでは、Microsoft Visual FoxPro ドライバーを選択し、完了 をクリックします。  
  
5.  [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)データ ソースの名前と説明を入力、データベースの種類を選択、データベースまたはディレクトリを選択し、[ok] をクリックします。  
  
     新しいデータ ソース名は、ODBC データ ソース アドミニストレーター ダイアログ ボックスの ユーザー DSN タブでユーザー データ ソースの一覧に表示されます。  
  
6.  新しいデータ ソースを保存し、ODBC データ ソース アドミニストレーター ダイアログ ボックスを閉じるには、ok をクリックします。
