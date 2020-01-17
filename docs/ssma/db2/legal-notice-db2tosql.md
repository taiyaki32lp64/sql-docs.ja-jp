---
title: 法的通知 (DB2toSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d2e558b8-7208-44b4-82b3-4b411a34a8c9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2a99cc9b4eaa1ca45d1d72d3cf3fbab6e6b3571e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141040"
---
# <a name="legal-notice-db2tosql"></a>法的通知 (DB2toSQL)
このソフトウェアおよびマニュアルに記載されている参照用のアプリケーションを含んだ内容は、情報の提供のみを目的としており、明示または黙示にかかわらず、このマニュアルは保証なしで提供されます。 このソフトウェアの仕様およびマニュアルに記載されている事柄は、将来予告なしに変更することがあります。 お客様が本製品を運用した結果の影響については、お客様が負うものとします。  
  
このマニュアルに含まれているサンプルは、概念や特定のステートメントまたは句の利用方法の説明を主目的として提供されています。 多くのサンプルは、特定の概念やステートメントの説明のみを目的としているため、通常の実稼働システムで必要となるようなデータ評価やエラー処理のコードは含んでいません。 提供されているサンプルおよびソース コードに対するテクニカル サポートは行っていません。  
  
特に記載していない場合、このソフトウェアおよびマニュアルで使用している会社、組織、製品、ドメイン名、電子メール アドレス、人物、場所、出来事などの名称は架空のもので、実在する商品名、団体名、個人名などとは一切関係ありません。 お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。 このソフトウェアおよびマニュアルのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。  
  
マイクロソフトは、このマニュアルに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。 このマニュアルはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。  
  
© 2016 Microsoft Corporation. All rights reserved.  
  
Microsoft、Windows、Windows NT、Windows Server、Active Directory、ActiveX、BackOffice、bCentral、BizTalk、DirectX、Excel、Hotmail、IntelliSense、J/Direct、Jscript、Microsoft Press、MSDN、MS-DOS、Outlook、PivotChart、PivotTable、PowerPoint、SharePoint、SQL Server、Visual Basic、Visual C#、Visual C++、Visual FoxPro、Visual InterDev、Visual J#、Visual J++、Visual SourceSafe、Visual Studio、Win32、Win32s、Windows Mobile、Windows Server System、および WinFX は、米国 Microsoft Corporation の米国およびその他の国における登録商標または商標です。  
  
SAP NetWeaver は、ドイツ SAP AG のドイツおよびその他の国における登録商標または商標です。  
  
記載されている会社名、製品名には、各社の商標のものもあります。  
  
## <a name="documentation-policy-for-sql-server-support-and-upgrade"></a>SQL Server のサポートおよびアップグレードに関するドキュメント ポリシー  
SQL Server のドキュメントに記載されている内容は、十分なテストを実施した後にはじめて公開されます。 -SQL Server オンライン ブック、readme ファイル、既知の問題ドキュメント、およびサポート技術情報の記事 - 製品ドキュメントには、SQL Server の機能とは安全にすべての顧客によって一般的な使用するのに十分な堅牢な機能に関する内容が含まれています。 このポリシーは、リリースおよびサービス パックの Readme ファイルを含む、すべての SQL Server のドキュメントに適用されます。Readme は、オンライン ブックの追加ファイルとして扱われます。  
  
機能によっては、お客様が直接使用しないものもあり、そのような機能に関してはドキュメントに記載されていません。 Microsoft が発行する SQL Server のドキュメントに記載されていない機能については、サード パーティの書籍や Web サイトの内容は Microsoft カスタマー サポートによってサポートされません。実稼働データベースやアプリケーションでは使用しないでください。  
  
お客様は、ドキュメントに記載されていない API、ストアド プロシージャ、拡張ストアド プロシージャ、関数、ビュー、テーブル、列、プロパティ、メタデータなどを使用しないでください。 Microsoft カスタマー サポートでは、ドキュメントに記載されていないエントリ ポイントを応用または使用したデータベースやアプリケーションをサポートしません。  
  
ドキュメントに記載されていないエントリ ポイントを応用または使用するアプリケーションやデータベースについては、将来のバージョンの SQL Server に対応させるためのサーバーおよびデータベースのアップグレードは保証されません。 SQL Server 機能の使用は、Microsoft SQL Server のドキュメントに記載されている方法に限定されます。 機能が Microsoft SQL Server のドキュメントに記載されていない場合は、SQL Server のサポート対象から除外されます。  
  
