---
title: ADO 履歴 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a84ccbb97c26ea92f31212933aac79bde2784b72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927165"
---
# <a name="ado-features-for-each-release"></a>各リリースの ADO の機能

このトピックでは、ADO、ADO MD、および ADOX の各リリースで導入された新機能を使用します。

## <a name="ado-60"></a>ADO 6.0

 ADO 6.0 は Windows Vista、Windows Data Access Components (Windows DAC) 6.0 の一部として含まれます。 ADO 6.0 は、ADO 2.8 に相当する機能。

## <a name="ado-28"></a>ADO 2.8

 ADO 2.8 は、Windows XP および Windows Server 2003 では、一部の Microsoft Data Access Components (MDAC) 2.8 として含まれていました。 MDAC 2.8 の再頒布可能パッケージのバージョンも使用します。Windows 2000 のみにこの再頒布可能パッケージのバージョンをインストールすることに注意してください。 ADO 2.8 は、いくつかのセキュリティ関連の問題を説明します。

 *信頼済みゾーン外は、ハード ドライブへのアクセスが許可されていません。*
クロス ドメインの信頼関係の低いサイトに関連するスクリプトは、次の操作は無効になっています。**Stream.SaveToFile**、 **Stream.LoadFromFile**、 **Recordset.Save**、および**Recordset.Open**と組み合わせて使用される、 **adCmdFile**フラグまたは、Microsoft OLE DB 永続化プロバイダーが (MSPersist)。

 **Recordset.Open** _、_ **Recordset.Save** _、_ **Stream.SaveToFile** _、および_ **Stream.LoadFromFile** _物理ファイルのみで動作します。_
これらのメソッドは、ファイル ハンドルが指す物理ファイルのみを検証するようになりました。

 **Recordset.ActiveCommand** _HTML/ASP ページから呼び出されたときにエラーが返されます。_
これにより、**コマンド**誤用されるオブジェクト。

 _数_**レコード セット** _、入れ子になったによって返される_ **図形** _コマンドには上限が設けられています。_
入れ子になった shape コマンドは 512 の最大値を返すようになりました**レコード セット**します。 つまり、**図形**コマンドは、任意の深さでネスト不要になったことができます。 最大レベルの深さは、512 文字です代わりに、各コマンドを実行する 1 つ (子) の場合**Recordset**します。 任意のレベルでは、場合、**図形**コマンドが複数返されます**レコード セット**レベルの深さの上限は 512 未満になります。

## <a name="ado-27"></a>ADO 2.7

 *64 ビット プラットフォーム サポート*ADO 2.7 には 64 ビット プロセッサのサポートが導入されています。

## <a name="ado-26"></a>ADO 2.6

 **CubDef.GetSchemaObject** _メソッド_ADO 2.6 以降では、ADO MD 取得できるオブジェクトで指定された一意の名前を使用して、 [UniqueName プロパティ (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)します。 親オブジェクトの名前は、既知である必要はありませんし、親のコレクションは、スキーマ オブジェクトを取得する事前設定する必要はありません。 参照してください[GetSchemaObject メソッド (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)します。

 *コマンド ストリーム*、**コマンド**オブジェクト ストリーム形式でのコマンドのサポートを使用する代わりに、 **CommandText**プロパティ。 [CommandStream プロパティ (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) XML テンプレートまたはとしてアップデート グラムを指定するために使用できる、**コマンド**for SQL Server、Microsoft OLE DB プロバイダーで入力します。

 **言語** _プロパティ_ [言語](../../ado/reference/ado-api/dialect-property.md)構文を定義する新しいプロパティは、一般的なルールを文字列またはストリームを解析するプロバイダーを使用することです。

 **Command.Execute** _メソッド_、 [メソッドの実行](../../ado/reference/ado-api/execute-method-ado-command.md)ADO の**コマンド** オブジェクトは入力と出力のストリームを使用して強化されています。

 *フィールド statusvalues*を変更する場合、ユーザーは DB_E_ERRORSOCCURRED エラーが発生した場合、**フィールド**の**レコード セット**、ADO に収まるようになりました、 **Field.Status**プロパティを適切な状態情報、ユーザーには、問題点の詳細についてがあるできるようにします。 参照してください[Status プロパティ (ADO Field)](../../ado/reference/ado-api/status-property-ado-field.md)します。

 **NamedParameters** _プロパティ_ [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md)の新しいプロパティである、**コマンド** という名前のプロバイダーを使用することを示すオブジェクトパラメーター。

 *ストリームの結果セット*ADO は、データ ソースから結果セットを返すことができます、 **Stream**、なく**レコード セット**オブジェクト。 Microsoft OLE DB Provider の最新バージョンの SQL Server を使用して取得できます XML の結果、プロバイダーから"XML の"クエリを実行しています。 A **Stream**結果セットを受け取る、ソースとして"XML の"コマンドを使用して開くことができます。 参照してください[をストリームに結果セットを取得する](../../ado/guide/data/retrieving-resultsets-into-streams.md)します。

 *1 つの行の結果セット*、ADO**レコード**オブジェクトは、コマンド文字列では開くようになりましたまたは**コマンド**オブジェクトをプロバイダーからのデータの 1 つの行を返します。 これにより、MDAC 2.6 プロバイダーを使用したパフォーマンスの向上。 参照してください[Open メソッド (ADO Record)](../../ado/reference/ado-api/open-method-ado-record.md)します。

## <a name="ado-25"></a>ADO 2.5

 **レコード**_オブジェクト_ADO 2.5 が導入されています、**レコード**表示してから行を管理するオブジェクト、**レコード セット**またはデータ プロバイダー、またはオブジェクトのカプセル化します。ファイルやディレクトリなどの半構造化データ。

 **Stream** _オブジェクト_ADO 2.5 も導入されています。、 **Stream**バイナリまたはテキスト データのストリームを表すオブジェクト。

 *URL バインディング*ADO 2.5 は、データ ストア オブジェクトの名前、接続文字列とコマンド テキストの代替として、URL の使用方法を紹介します。 既存の URL を使用できます**接続**と**レコード セット**、オブジェクトとして新しい**レコード**と**Stream**オブジェクト。

 *データ プロバイダーの URL バインディングをサポートしている*ADO 2.5 には、URL スキームを認識する OLE DB プロバイダーがサポートされています。 これには、for Windows 2000 のファイル システムにアクセスし、既存の HTTP スキームを認識する Internet Publishing、OLE DB プロバイダーが含まれます。
