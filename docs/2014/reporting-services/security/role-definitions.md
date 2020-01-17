---
title: ロールの定義 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- roles [Reporting Services], security
- security [Reporting Services], role definitions
- role-based security [Reporting Services], role definitions
ms.assetid: d1b8dbf0-4462-402e-92dd-0e4835002b6e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6518a46c44a97fbb386b4479454e89a0eccb1a39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101750"
---
# <a name="role-definitions"></a>ロールの定義
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、*ロール**の定義*は、ユーザーがレポート サーバー上で実行できる操作を定義する、一連の名前付きタスクです。 ロールの定義によって、レポート サーバーがセキュリティを強制的に適用する際に使用するルールが提供されます。 ユーザーがレポートのパブリッシュなどのタスクを試行すると、レポート サーバーでは、ユーザーのロールの割り当てを確認し、そのタスクがロールの定義に含まれているかどうかを判別します。 該当するタスクがロールの定義に含まれている場合、要求が送信されます。  
  
## <a name="using-roles-to-authorize-access-to-a-report-server"></a>ロールを使用したレポート サーバーへのアクセスの承認  
 ロールは、ロールの割り当てで使用されている場合のみ有効になります。 ロールでセキュリティを提供する方法の詳細については、「 [ロールの割り当て](role-assignments.md)」を参照してください。  
  
## <a name="types-of-role-definitions"></a>ロールの定義の種類  
 ロールの定義は、アイテムレベルの定義またはシステムレベルの定義です。 *アイテムレベルのロールの定義* には、レポート サーバーで格納および管理されているアイテムに関連するタスクが含まれています。 アイテムレベルのロールの定義に含めることのできるタスクには、"レポートの管理"、"フォルダーの表示"、および "個別のサブスクリプションを管理" などがあります。 *システム ロールの定義* には、サイト全体に適用するタスクが含まれています。 システム ロールに含めるタスクには、"レポート サーバーのプロパティを表示" などがあります。  
  
## <a name="predefined-roles"></a>Predefined Roles  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、ユーザーが実行するさまざまなレベルの操作に対応した定義済みロールが用意されています。 使用できる定義済みロールを次に示します。  
  
-   コンテンツ マネージャー、パブリッシャー、閲覧者、レポート ビルダー、および個人用レポートは、アイテムレベルのロールの定義であり、レポート サーバー コンテンツにアクセスするためのロールの割り当てを作成する際に使用できます。  
  
-   システム管理者およびシステム ユーザーは、システム レベルのロールの定義であり、サイト操作へのアクセスを承認する際に使用できます。  
  
 詳細については、「 [定義済みロール](role-definitions-predefined-roles.md)」を参照してください。  
  
## <a name="creating-a-role-definition"></a>ロールの定義の作成  
 ロールを作成するには、Management Studio を使用して名前を指定し、ロールに含めるタスクを指定します。 アイテムのタスクとシステムのタスクに対しては、ロールの定義を個別に作成する必要があります。 ロールには、アイテムレベルまたはシステムレベルのタスクを含めることができますが、両方を含めることはできません。 ロールの定義を作成するには、定義の名前を入力し、一連のタスクを選択します。 ロールの定義を作成するには、そのための権限が必要です。 その権限は、"アイテムごとにセキュリティを設定します" タスクで与えられます。 既定では、管理者および定義済みの **コンテンツ マネージャー** ロールに割り当てられているユーザーがこのタスクを実行できます。  
  
 ロールには、一意の名前を付ける必要があります。 ロールの定義を有効にするには、1 つ以上のタスクを含める必要があります。 詳細については、「 [タスクと権限](tasks-and-permissions.md)」を参照してください。  
  
 ロールの定義を作成するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を使用します。 詳細については、「 [ロールを作成、削除、または変更する &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)」を参照してください。  
  
 ロールの定義を作成した後、その定義を使用するには、ロールの割り当てで定義を選択します。 詳細については、「 [レポート サーバーへのユーザー アクセスを許可する &#40;レポート マネージャー&#41;](grant-user-access-to-a-report-server.md)」を参照してください。  
  
## <a name="customize-or-delete-a-role-definition"></a>ロールの定義のカスタマイズと削除  
 定義済みロールは、変更したりカスタム ロールに置き換えたりできます。 ロールを変更するには、ロールの定義でタスクを追加または削除します。 ただし、ロールの名前を変更することはできません。 変更を行うと、そのロールの定義を含むすべてのロールの割り当てにすぐに適用されます。  
  
 使用しなくなったロールの定義は削除できます。 個人用レポート機能が有効である限り、この機能用に選択されているロールの定義は削除できません。 個人用レポートに使用しているロールの定義を削除するには、先に個人用レポート機能を無効にするか、個人用レポート機能で使用するロールの定義を別のものに選択し直す必要があります。  
  
## <a name="see-also"></a>参照  
 [タスクと権限](tasks-and-permissions.md)   
 [ネイティブ モードのレポート サーバーに対する権限の許可](granting-permissions-on-a-native-mode-report-server.md)   
 [ロールを作成、削除、または変更する (Management Studio)](role-definitions-create-delete-or-modify.md)   
 [レポート サーバーへのユーザー アクセスを許可する &#40;レポート マネージャー&#41;](grant-user-access-to-a-report-server.md)   
 [ロールの割り当てを変更または削除する &#40;レポート マネージャー&#41;](role-assignments-modify-or-delete.md)   
 [SharePoint サイト上のレポート サーバー アイテムに対する権限の設定 &#40;Reporting Services の SharePoint 統合モード&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
  
  
