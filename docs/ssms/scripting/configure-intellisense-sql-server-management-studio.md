---
title: IntelliSense の構成 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Options [SQL Server Management Studio], IntelliSense
- modifying IntelliSense options
- IntelliSense [SQL Server], modifying options
ms.assetid: 3ffc9f31-4efa-4c1a-a033-ed1dc48b065f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e148cd3dc64ce93b46a990580be24ace757a87af
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263506"
---
# <a name="configure-intellisense-sql-server-management-studio"></a>IntelliSense の構成 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  ほとんどの [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense オプションは、既定でオンになっています。 IntelliSense オプションをオフにして、メニュー コマンドやキーストロークの組み合わせによって起動することも可能です。  
  
> [!IMPORTANT]  
>  一部の変更は、現在のエディター セッションで反映されません。  変更を確認するには、新しい Transact-SQL エディター セッションを開く必要があります。
  
### <a name="to-turn-statement-completion-options-off-by-default"></a>入力候補オプションを既定でオフにするには  

> [!NOTE]
> SQL Data Warehouse は、IntelliSense をサポートしていません。
>
>
  
1.  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  **[テキスト エディター]** を展開し、 **[すべての言語]** 、 **[Transact-SQL]** 、 **[XML]** のいずれかを展開して、 **[全般]** をクリックします。  
  
3.  入力候補オプションのうち、使用しないオプションのチェック ボックスをオフにし、 **[OK]** をクリックします。  
  
### <a name="to-modify-transact-sql-intellisense-options"></a>Transact-SQL IntelliSense オプションを変更するには  
  
1.  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  **[テキスト エディター]** を展開し、 **[Transact-SQL]** を展開し、 **[IntelliSense]** をクリックします。  
  
3.  使用しない IntelliSense オプションのチェック ボックスをオフにします。  
  
4.  IntelliSense 機能を無効にするスクリプト サイズを変更するには、 **[スクリプトの最大サイズ]** ボックスの一覧からサイズを選択します。  
  
5.  入力候補一覧の関数名に適用される文字種を変更するには、 **[組み込み関数名の文字種]** ボックスの一覧から文字種仕様を選択します。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
