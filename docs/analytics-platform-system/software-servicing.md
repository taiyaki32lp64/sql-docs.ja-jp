---
title: ソフトウェアのサービス
description: Analytics Platform System (APS) でのソフトウェアサービス。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400312"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Analytics Platform System のソフトウェアサービス
このセクションでは、WSUS や Analytics Platform System の修正プログラムなど、分析プラットフォームシステムアプライアンスのソフトウェアサービス要件について概要を説明します。  
  
## <a name="Basics"></a>ソフトウェアサービスの基礎  
**WSUS:** Windows Server Update Services (WSUS) から更新プログラムを受信するように、分析プラットフォームシステムアプライアンスを構成する必要があります。 これらの更新プログラムには、アプライアンスソフトウェアに対する重要な変更が含まれています。 構成が完了すると、多くの更新プログラムが自動的にインストールされ、ハンズオン管理は不要になります。 通常、WSUS の更新プログラムは、新しいアプライアンスのセットアップ時に実行される [ [Windows Server Update Services &#40;wsus&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md) ] ステップで構成されます。 それ以外の場合は、後でこの構成手順を実行できます。 WSUS の詳細については、 [wsus web サイトガイド](https://go.microsoft.com/fwlink/?LinkId=202417)を参照してください。  
  
**修正プログラム:** また、Analytics Platform System の修正プログラムを適用することが必要になる場合もあります。 *修正プログラム*は、分析プラットフォームシステムソフトウェアの問題を解決するために、特定の顧客向けに作成されたソフトウェア更新プログラムです。 各修正プログラムは、お客様固有の問題の修正プログラムをインストールする実行可能ファイルです。 各修正プログラムには、Windows、SQL Server、および分析プラットフォームシステム用に以前にリリースされたソフトウェア更新プログラムの累積も含まれています。 修正プログラムをインストールする必要がある場合は、Microsoft サポートから修正プログラムと手順が提供されます。  
  
**更新プログラムの適用範囲:** 分析プラットフォームシステムに修正プログラムまたは Service Pack を適用するには、アプライアンス全体をオフラインにする必要があります。  
  
**SSIS 変換先アダプターおよびクライアントツール:** SSIS 変換先アダプターの MSI またはクライアントツールの MSI に加えられた変更を含む修正プログラムを適用すると、管理ノードの**C:\PDWINST\ClientTools**ディレクトリで msi ファイルが更新されます。 この修正プログラムでは、更新された MSI ファイルからコンポーネントが自動的にインストールされません。 これらのコンポーネントを更新するには、顧客が古いバージョンのコンポーネントをアンインストールし、更新された MSI ファイルから新しいバージョンをインストールする必要があります。 SSIS 変換先アダプターの MSI またはクライアントツールの MSI に加えられた変更を含む修正プログラムをアンインストールする場合、それらのコンポーネントの MSI ファイルは以前のバージョンに戻されます。 これらのコンポーネントを以前のバージョンに戻すには、顧客が既存の (新しい) バージョンのコンポーネントをアンインストールし、元に戻した MSI ファイルから古いバージョンを再インストールする必要があります。  
  
## <a name="software-servicing-topics"></a>ソフトウェアサービスに関するトピック  
次のトピックでは、アプライアンスでソフトウェアサービスを管理する方法について説明します。  
  
-   [Microsoft Update &#40;Analytics Platform System&#41;をダウンロードして適用します](download-and-apply-microsoft-updates.md)  
  
-   [Microsoft 更新プログラムのアンインストール &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [Analytics platform system の修正プログラム &#40;analytics Platform System&#41;を適用します](apply-analytics-platform-system-hotfixes.md)  
  
-   [Analytics platform system の修正プログラム &#40;Analytics Platform System&#41;をアンインストールする](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
