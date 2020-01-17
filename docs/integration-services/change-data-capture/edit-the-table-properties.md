---
title: テーブルのプロパティの編集 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- editTabProps
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ae05c1015fe885c7488af0b0c9c7e340dc25d056
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294736"
---
# <a name="edit-the-table-properties"></a>テーブルのプロパティの編集

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  変更がキャプチャされている選択したテーブルの特定の列を編集するには、このダイアログ ボックスを使用します。 **[セキュリティ ロール]** と **[キャプチャ インスタンス]** の情報を編集することもできます。  
  
### <a name="to-edit-the-columns-to-include-in-the-cdc-instance"></a>CDC インスタンスに含める列を編集するには  
  
1.  次のいずれかまたは両方の操作を行います。  
  
    -   CDC インスタンスに含める追加の列の横のチェック ボックスをオンにします。  
  
    -   CDC インスタンスに含めない列の横のチェック ボックスをオフにします。  
  
### <a name="to-edit-the-security-role"></a>セキュリティ ロールを編集するには  
  
1.  **"セキュリティ ロール"** フィールドで、新しい名前を入力するか、セキュリティ ロールの名前を編集します。  
  
### <a name="to-create-a-new-capture-instance"></a>新しいキャプチャ インスタンスを作成するには  
  
1.  **[セキュリティ ロール]** セクションの **"名前"** フィールドに、キャプチャ インスタンスの名前を入力します。 既定では、このフィールドに入力される名前は、現在のキャプチャ インスタンスの名前の末尾に **_NEW** を追加したものです (例: **old_instance_NEW**)。  
  
2.  キャプチャ インスタンスを次のいずれかとして保存します。  
  
    -   **[新しいキャプチャ インスタンス]** : この場合、新しいキャプチャ インスタンスが保存され、古いキャプチャ インスタンスは削除されません。  
  
         **注**:テーブルごとに 2 つまでのキャプチャ インスタンスを設定できます。 既に 2 つのキャプチャ インスタンスがある場合、このオプションは利用できません。  
  
    -   **[既存のものを置換]** : この場合、現在のキャプチャ インスタンスが削除され、作成したキャプチャ インスタンスで置換されます。 このテーブルに 2 つのキャプチャ インスタンスが定義されている場合、置換するキャプチャ インスタンスを選択する必要があります。  
  
 **注**: **[テーブル]** タブのテーブルの一覧からキャプチャ インスタンスを削除できます。  
  
 このダイアログ ボックスで情報の入力を終了したら、 **[OK]** をクリックして変更を受け入れます。  
  
## <a name="see-also"></a>参照  
 [CDC インスタンスのプロパティを編集する方法](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [変更をキャプチャするために選択したテーブルに対する変更](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  
