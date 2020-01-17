---
title: Microsoft ActiveX Data Objects (ADO) |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ca9c22cb54c54441f848ecbf367e92e30c1fd83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921878"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ADO は、C++ プログラムで SQL Server への接続に使用されます。 もちろん、クラウドでの Azure SQL Database に接続するこの機能はもします。

この記事では、各セクションでは、ADO のコンポーネントについて説明します。

> [!NOTE]
> ADO.NET は、ADO と異なります。 ADO.NET、およびその他の多くの SQL 接続ドライバーとその言語は開始位置として説明[SQL Server ドライバー](../connect/sql-connection-libraries.md)します。

  
## <a name="ado"></a>ADO (ADO)  
 Microsoft ActiveX データ オブジェクト (ADO) では、クライアント アプリケーションからアクセスして、さまざまな OLE DB プロバイダー経由のソースからデータを操作が有効にします。 その主な利点は、使いやすさ、高速、低いメモリのオーバーヘッドが小さく、ディスク フット プリントです。 ADO には、クライアント/サーバーと Web ベースのアプリケーションを構築するための主な機能がサポートしています。  
  
## <a name="ado-md"></a>ADO MD (ADO MD)  
 Microsoft ActiveX Data Objects (多次元) (ADO MD) は、Microsoft Visual Basic、および Microsoft Visual C などの言語から多次元データを簡単にアクセスを提供します。 ADO MD CubeDef およびセルセット オブジェクトなどの多次元データに固有のオブジェクトを Microsoft ActiveX データ オブジェクト (ADO) を拡張します。 ADO MD とには、多次元スキーマを参照し、キューブを照会および結果を取得することができます。  
  
 ADO と同様には、ADO MD は、データにアクセスするのに、基になる OLE DB プロバイダーを使用します。 ADO MD を使用するには、プロバイダーは OLE DB for OLAP 仕様で定義されている多次元データ プロバイダー (MDP) をある必要があります。 Mdp 表形式のデータ プロバイダー (Tdp) ではなく多次元のビューでデータを示すでデータの表形式ビュー。 特定の構文と、プロバイダーでサポートされている動作の詳細については、OLAP OLE DB プロバイダーは、ドキュメントを参照してください。  
  
## <a name="rds"></a>RDS  
 リモート データ サービス (RDS) は、ADO がクライアント アプリケーションまたは Web ページをサーバーからデータを移動、クライアントでは、データを操作して更新プログラムを 1 回のラウンド トリップでサーバーに返すの機能です。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX データ オブジェクトの拡張機能をデータ定義言語 (ADOX) セキュリティでは、ADO オブジェクトとプログラミング モデルの拡張機能です。 ADOX には、スキーマの作成と変更、セキュリティのオブジェクトが含まれます。 操作のスキーマにオブジェクト ベースのアプローチであるために、さまざまなデータ ソースのネイティブの構文を使って違いに関係なく動作するコードを記述できます。  
  
 ADOX は、コア ADO オブジェクト コンパニオン ライブラリです。 作成、変更、およびテーブルやプロシージャなどのスキーマ オブジェクトを削除するその他のオブジェクトを公開します。 ユーザーとグループの管理と付与して、オブジェクトに対する権限の取り消しをセキュリティ オブジェクトも含まれています。  
  
## <a name="documentation"></a>ドキュメント  
 [ADO セキュリティ デザイン機能に関する問題](../ado/guide/ado-security-design-issues.md)  
  
 [ADO プログラマー ガイド](../ado/guide/ado-programmer-s-guide.md)  
  
 ADO、RDS、ADO MD、および ADOX の使用の概要。  
  
 [ADO プログラマー リファレンス](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO のドキュメントのこのセクションには、各 ADO、RDS、ADO MD、および ADOX オブジェクト、コレクション、プロパティ、動的なプロパティ、メソッド、イベント、および列挙体のトピックが含まれています。  
  
 [ADO の用語集](../ado/ado-glossary.md)  
  
## <a name="support"></a>サポート  
 無料の ADO の問題に関するヘルプ、ADO パブリック ニュースグループへの投稿をお試しください。 このニュースグループは、ADO をカバーする Microsoft 製品サポート サービス (PSS) のサポート担当者と他の経験豊富な ADO 開発者が監視されます。  
  
 サポート オプションの詳細については、Microsoft ヘルプとサポート Web サイトで参照できます。


