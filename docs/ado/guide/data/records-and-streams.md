---
title: レコードとストリーム |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4636df1451ba946b9a7bfb62e3d6775c35b1d6f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924494"
---
# <a name="records-and-streams"></a>レコードとストリーム
ADO は、現在、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトとしてのリレーショナル データベースなどのデータ ソース内の情報にアクセスする主要な手段です。 ただし、一部のプロバイダーのサポート、[レコード](../../../ado/reference/ado-api/record-object-ado.md)と[Stream](../../../ado/reference/ado-api/stream-object-ado.md)のプロバイダーからのデータを操作できる代替または補完的なオブジェクトとしてのオブジェクト。 詳細についての**レコード**動作、プロバイダーのドキュメントを参照してください。  
  
## <a name="records"></a>[レコード]  
 **レコード**オブジェクトは 1 行では、基本的に関数**Recordset**秒。 ただし、**レコード**と比較する機能が制限**レコード セット**さまざまなプロパティとメソッドがあります。内のデータ ソース、**レコード**オブジェクトは、プロバイダーから 1 行のデータを返すコマンドを指定できます。 使用して**レコード**オブジェクトなく**Recordset**を 1 行のデータを返すクエリから結果を受信するオブジェクトが複雑になるほどをインスタンス化のオーバーヘッドを取り除いて**レコード セット**オブジェクト。  
  
 **レコード**オブジェクトは、従来のリレーショナル データベース以外のデータ ソースのプロバイダーと特に別の目的をなど、使用できる、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 処理する必要がある情報の多くに存在します、データベース内のテーブルとしてではなくメッセージとして電子メール システムとファイルの最新のファイル システム。 **レコード**と**Stream**オブジェクトは、リレーショナル データベース以外のソースに格納されている情報へのアクセスを容易にします。  
  
 **レコード**オブジェクトが表すし、電子メール システムでファイル システムまたはフォルダー、およびメッセージにディレクトリやファイルなどのデータを管理します。 このため、ソースを**レコード**の開いている現在の行は、**レコード セット**、絶対 URL または相対 URL を開くと組み合わせて[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
 通常、**レコード セット**コンテナーまたはフォルダーやディレクトリなどの階層の親を表すために使用できます。 A**レコード**ファイルやドキュメントなど、親コンテナーに 1 つのノードに関する特定の情報を返すために使用できます。 主な理由**レコード**この種の情報を表すために使用されてこれらのデータ ソースが異種ことです。 つまり、各**レコード**さまざまなセットとフィールドの数があります。 従来**レコード セット**データベースから行を含むは、同種。 つまり、各行がフィールドの種類と同じ数のことです。  
  
 使用しての詳細については、**レコード**インターネット発行プロバイダーなどのプロバイダーからこの異種データを処理するオブジェクトを参照してください[for Internet Publishing ADO を使用する](../../../ado/guide/data/using-ado-for-internet-publishing.md)します。  
  
## <a name="streams"></a>ストリーム  
 **Stream**オブジェクトは、読み取り、書き込み、およびバイトのストリームを管理する手段を提供します。 このバイト ストリームは、テキストまたはバイナリがあり、システム リソースによってのみサイズに制限されます。 通常、ADO **Stream**オブジェクトは、次の目的で使用します。  
  
-   データを格納する、 **Recordset** XML 形式で保存します。 これらの XML ストリームから保存**レコード セット**s は、新しいを開くときに、ソースとして使用できます**レコード セット**します。 詳細については、次を参照してください。[ストリームと永続性](../../../ado/guide/data/streams-and-persistence.md)します。  
  
-   含まれている[CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md)の代わりに、プロバイダーに対して実行される[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)します。 たとえば、XML アップデート グラムは、SQL Server 用のプロセス Microsoft OLE DB プロバイダーに対してコマンドのソースとして使用できます。  
  
-   以外の形式で、プロバイダーから結果を受信する、 **Recordset**、Microsoft OLE DB Provider for SQL Server から XML の結果などです。 詳細については、次を参照してください。[をストリームに結果セットを取得する](../../../ado/guide/data/retrieving-resultsets-into-streams.md)します。  
  
-   テキストまたはファイルまたは for Internet Publishing Microsoft OLE DB プロバイダーなどのプロバイダーで使用して通常のメッセージを構成するバイトを格納するには このように使用の詳細については**Stream** 、オブジェクトを参照してください[for Internet Publishing ADO を使用する](../../../ado/guide/data/using-ado-for-internet-publishing.md)します。  
  
 A **Stream**でオブジェクトを開くことができます。  
  
-   URL で指定された単純なファイル。  
  
-   フィールドを**レコード**または**Recordset**を含む、 **Stream**オブジェクト。  
  
-   既定のストリームを**レコード**または**Recordset**複合ファイルまたはディレクトリを表すオブジェクト。  
  
-   簡単なファイルの URL を含むリソース フィールド。  
  
-   すべてでは、特定のソースがありません。 ここで、 **Stream**オブジェクトはメモリで開かれます。 データを書き込まれ、別に保存し、 **Stream**またはファイル。  
  
-   BLOB のフィールドを**Recordset**します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ストリームと永続性](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [コマンド ストリーム](../../../ado/guide/data/command-streams.md)  
  
-   [ストリーム形式で結果セットを取得する](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [インターネットへの発行に ADO を使用する](../../../ado/guide/data/using-ado-for-internet-publishing.md)
