---
title: CDC へのテーブルの追加 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- addTabs
ms.assetid: ad260e19-c021-4035-9311-c02fc96ceaea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 546f001ac4809a4fb8c455e37bf10f975d84dce8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771508"
---
# <a name="add-tables-to-a-cdc-instance"></a>CDC へのテーブルの追加
  [テーブル選択] ダイアログ ボックスを使用すると、Oracle ソースから CDC インスタンスに追加のテーブルを追加できます。 選択したテーブルは、プロパティ エディターの **[テーブル]** タブの一覧に追加されます。  
  
 既定では、このダイアログ ボックスのテーブルの一覧にはテーブルが含まれていません。 **[(すべて選択)]** チェック ボックスをオンにするか、特定のテーブルを検索することができます。  
  
 **特定のテーブルを検索するには**  
 次のように検索条件を入力し、 **[検索]** をクリックします。  
  
-   **[スキーマ]** : データベース スキーマを一覧から選択します。 そのスキーマを持つテーブルだけが一覧に表示されます。  
  
-   **[テーブル名パターン]** : 任意の文字列を入力します。 入力した文字列を含むテーブルのみが表示されます。  
  
> [!NOTE]  
>  これらのフィールドの一方または両方に条件を入力できます。  
  
-   **[一致するテーブルのうち最初の 1000 個を表示する]** : 既定では、このチェック ボックスはオンになっています。 一致するテーブルのうち最初の 1000 個のみが表示されます。 このチェック ボックスをオフにすると、条件に一致するすべてのテーブルが表示されます。 テーブルが多数存在する場合、一覧の表示に時間がかかる場合があります。  
  
 **CDC インスタンスに含めるテーブルを選択するには**  
 含めるテーブルの横のチェック ボックスをオンにして、 **[追加]** をクリックします。 新しいインスタンス ウィザードの **[テーブルと列の選択]** ページの一覧にテーブルが追加されます。  
  
 テーブルを追加せずにダイアログ ボックスを閉じる場合は、 **[閉じる]** をクリックします。  
  
> [!NOTE]  
>  サポートされていないデータ型が含まれているテーブルを選択すると、エラー メッセージが表示され、そのテーブルは追加されません。  
  
> [!NOTE]  
>  テーブルの一覧は、ビューアーで表示できます。 ビューアーを使用する場合、情報は読み取り専用です。 ビューアーには、テーブルのキャプチャ対象列の一覧も含まれています。 ビューアーへのアクセス方法については、「 [How to Manage a CDC Instance](manage-a-cdc-instance.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CDC インスタンスのプロパティを編集する方法](how-to-edit-the-cdc-instance-properties.md)   
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [変更をキャプチャするための Oracle テーブルの選択](select-oracle-tables-for-capturing-changes.md)  
  
  
