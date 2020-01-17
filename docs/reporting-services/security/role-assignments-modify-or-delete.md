---
title: ロールの割り当てを変更または削除する (SSRS Web ポータル) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 28695a4849b29c6e593f42489fc149efd9a8db53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570644"
---
# <a name="role-assignments---modify-or-delete"></a>ロールの割り当て - 変更または削除

ロールの割り当てとは、実行できるタスクを定義する、あらかじめ定義されたロールに、グループまたはユーザー アカウントをマップすることです。 それによって、ユーザーがフォルダー、レポート、モデル、またはその他のコンテンツの種類に対して実行できるタスクの種類が決定されます。 ロールの割り当てを作成、変更、または削除するには、SSRS Web ポータルを使用します。 特定のユーザーまたはグループに対して作成したロールの割り当ては、後で異なるロールを選択することによって変更できます。 レポート サーバーに対する権限を取り消したい場合は、ロールの割り当てをレポート サーバーから削除します。  

目的によっては、別の方法を用いた方がよい場合もあります。 つまり、新しいロール定義の作成やカスタマイズ、Active Directory 内グループ アカウントのメンバーシップ変更などです。  

たとえば、あるグループのユーザーが、自分たちのコンテンツを管理する必要があるが、コンテンツ マネージャーに関連付けられているすべての権限が付与されるべきではないとします。 "部門コンテンツ マネージャー" という新しいロール定義を作成できます。 これに、コンテンツ マネージャーの **[Set security policies for items]\(アイテムごとにセキュリティ ポリシーを設定\)** を除く、すべてのタスクを含めることができます。

同様に、システム管理者やネットワーク管理者にとっては、Web ポータルでロールの割り当てを管理するよりも、Active Directory のグループ アカウントを管理した方が簡単である可能性があります。 グループ アカウントに対するロールの割り当てを 1 つだけ作成することによって、ロールの割り当ての管理に伴うオーバーヘッドを低減できます。 その後、ユーザーがレポートにアクセスする必要がなくなったら、グループ メンバーシップを変更できます。
  
 ロールの割り当てを変更または削除することが最善の方法であると判断した場合は、必ずシステム ロールの割り当てとアイテム ロールの割り当ての両方を確認してください。 Web ポータルでロールの割り当てを構成する際に使用するページは、ロールの種類によって異なります。
  
## <a name="to-modify-or-delete-a-system-role-assignment"></a>システム ロールの割り当てを変更または削除するには
  
1. [レポート サーバーの Web ポータル &#40;SSRS Native Mode&#41;](../../reporting-services/web-portal-ssrs-native-mode.md) にアクセスします。

2. **[サイトの設定]**  >  **[セキュリティ]** を選択します。 現在、サーバーまたはスケールアウト配置に対して定義されているシステムレベルのロールの割り当てが、アカウント名ごとに一覧表示されます。

3. 変更または削除するロールの割り当てを探します。

4. 特定のユーザーまたはグループに対してロールを追加または削除するには、 **[編集]** を選択します。

5. ロールの割り当てを削除するには、ユーザーまたはグループ名の隣にあるチェック ボックスをオンにして、 **[削除]** を選択します。

### <a name="to-modify-or-delete-an-item-role-assignment"></a>アイテム ロールの割り当てを変更または削除するには

1. Web ポータルにアクセスし、ロールの割り当てを編集または削除するアイテムを探します。

2. アイテムの上にマウス ポインターを移動し、下矢印を選択します。

3. ドロップダウン メニューで、 **[セキュリティ]** を選択します。

4. 変更または削除するロールの割り当てを探します。

5. 特定のユーザーまたはグループに対してロールを追加または削除するには、 **[編集]** を選択します。

6. ロールの割り当てを削除するには、ユーザーまたはグループ名の隣にあるチェック ボックスをオンにして、 **[削除]** を選択します。

## <a name="see-also"></a>参照

[ロールの割り当てを作成および管理する](../../reporting-services/security/create-and-manage-role-assignments.md)  
[ロールの割り当て](../../reporting-services/security/role-assignments.md)  
