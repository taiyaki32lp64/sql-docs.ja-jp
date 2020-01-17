---
title: 変更をキャプチャするための Oracle テーブルの選択 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1e0ce4f9888602ef8083dc4f64e98ac4ad6154e5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294589"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>変更をキャプチャするための Oracle テーブルの選択

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このダイアログ ボックスを使用すると、CDC インスタンスに含めるテーブルを選択できます。 選択したテーブルは、新しいインスタンス ウィザードの **[テーブルと列の選択]** ページの一覧に追加されます。 このダイアログ ボックスでは次の操作を実行できます。  
  
 既定では、このダイアログ ボックスのテーブルの一覧にはテーブルが含まれていません。 チェック ボックス列の最上部にあるチェック ボックスをオンにしてすべてのテーブルを選択するか、特定のテーブルを検索することができます。  
  
 **特定のテーブルを検索するには**  
 次のように検索条件を入力し、 **[検索]** をクリックします。  
  
-   **[スキーマ]** : データベース スキーマを一覧から選択します。 そのスキーマを持つテーブルだけが一覧に表示されます。  
  
-   **[テーブル名パターン]** : 任意の文字列を入力します。 入力した文字列を含むテーブルのみが表示されます。  
  
> [!NOTE]  
>  これらのフィールドの一方または両方に条件を入力できます。  
  
-   **[一致するテーブルのうち最初の 1000 個を表示する]** : 既定では、このチェック ボックスはオンになっています。 一致するテーブルのうち最初の 1000 個のみが表示されます。 このチェック ボックスをオフにすると、条件に一致するすべてのテーブルが表示されます。 テーブルが多数存在する場合、一覧の表示に時間がかかる場合があります。  
  
 **CDC インスタンスに含めるテーブルを選択するには**  
 含めるテーブルの横のチェック ボックスをオンにして、 **[追加]** をクリックします。 新しいインスタンス ウィザードの **[テーブルと列の選択]** ページの一覧にテーブルが追加されます。  
  
 その他のテーブルを追加せずにダイアログ ボックスを閉じる場合は、 **[閉じる]** をクリックします。  
  
> [!NOTE]  
>  サポートされていないデータ型が含まれているテーブルを選択すると、エラー メッセージが表示され、そのテーブルは追加されません。  
  
## <a name="see-also"></a>参照  
 [SQL Server 変更データベース インスタンスを作成する方法](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle のテーブルおよび列の選択](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
