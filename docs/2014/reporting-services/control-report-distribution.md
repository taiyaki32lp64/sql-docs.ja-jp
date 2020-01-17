---
title: レポートの配信の制御 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- subscriptions [Reporting Services], e-mail
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- subscriptions [Reporting Services], security
- mail [Reporting Services]
ms.assetid: 8f15e2c6-a647-4b05-a519-1743b5d8654c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: de8a27801ef89f10bf303cee17d1c2d0e1081c5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109698"
---
# <a name="control-report-distribution"></a>レポートの配信を制御する
  電子メール配信およびファイル共有配信に関連するセキュリティ上のリスクを減らすように、レポート サーバーを構成できます。  
  
## <a name="securing-reports"></a>レポートの保護  
 レポートの配信を制御する際の最初の手順は、承認されていないアクセスからレポートをセキュリティで保護することです。 レポートでは、サブスクリプションで使用するために、配信ごとに変化しない格納済み資格情報セットを使用する必要があります。 レポート サーバー上のレポートにアクセスできるユーザーなら、だれでもレポートを実行でき、場合によってはレポートを配信することもできます。 このようなことが発生しないように、この操作を必要とするユーザーのみにレポート アクセスを制限する必要があります。 詳細については、次を参照してください。[レポートのセキュリティ保護とリソース](security/secure-reports-and-resources.md)と[フォルダーのセキュリティで保護された](security/secure-folders.md)します。  
  
 データベース セキュリティを使用してアクセスを承認する、高い機密情報を含むレポートは、サブスクリプションとして配信することはできません。  
  
> [!IMPORTANT]  
>  レポートはファイルとして転送されます。 ファイルに適用されるリスクおよび保護方法は、ディスクに保存されるレポートまたは添付ファイルとして送信されるレポートにも同様に適用されます。 ファイルへのアクセス権を持つユーザーは、自己の判断でファイルを配布または使用できます。  
  
## <a name="controlling-e-mail-delivery"></a>電子メール配信の制御  
 特定のホスト ドメインへの電子メールの配信を制限するようにレポート サーバーを構成できます。 たとえば、RSReportServer 構成ファイルに一覧されたドメインを除くすべてのドメインに、レポート サーバーからレポートが配信されないようにすることができます。  
  
 また、サブスクリプションの **[宛先]** フィールドを非表示にするように構成を設定することもできます。 この場合、レポートは、サブスクリプションを定義するユーザーにのみ配信されます。 ただし、レポートがユーザーに送信された後で、このレポートが転送されることを明示的に防ぐことはできません。  
  
 レポートの配信を制御する最も効果的な方法は、レポート サーバーからレポート サーバーの URL のみを送信するように構成することです。 レポート サーバーでは、Windows 認証およびロールベースの承認モデルを使用して、レポートへのアクセスを制御します。 ユーザーが表示権限のないレポートを電子メールで誤って受信しても、レポート サーバーはレポートを表示しません。  
  
## <a name="controlling-file-share-delivery"></a>ファイル共有の配信の制御  
 ファイル共有の配信は、ハード ディスク上のファイルにレポートを送信する際に使用されます。 ファイルがディスクに保存されると、レポート サーバーはユーザー アクセスの制御にロールベースのセキュリティ モデルを使用する必要がなくなります。 ディスクに配信されたレポートを保護するために、ファイル自体またはそのファイルを含むフォルダーにアクセス制御リスト (ACL) を使用できます。 オペレーティング システムによっては、別のセキュリティ オプションを使用できる場合があります。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー電子メール配信用に構成&#40;SSRS 構成マネージャー&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [サブスクリプションと配信 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [ネイティブ モード レポート サーバーのサブスクリプションの作成と管理](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)  
  
  
