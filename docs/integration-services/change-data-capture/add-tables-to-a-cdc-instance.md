---
title: CDC へのテーブルの追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- addTabs
ms.assetid: ad260e19-c021-4035-9311-c02fc96ceaea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa9bf38512b2ba817156f216161d21bc1d27c129
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294863"
---
# <a name="add-tables-to-a-cdc-instance"></a>CDC へのテーブルの追加

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
>  テーブルの一覧は、ビューアーで表示できます。 ビューアーを使用する場合、情報は読み取り専用です。 ビューアーには、テーブルのキャプチャ対象列の一覧も含まれています。 ビューアーへのアクセス方法については、「 [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CDC インスタンスのプロパティを編集する方法](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [変更をキャプチャするための Oracle テーブルの選択](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)  
  
  
