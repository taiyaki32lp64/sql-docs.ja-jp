---
title: レポート サーバー アイテムのプロパティ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- item-specific properties [Reporting Services]
- report items [Reporting Services], properties
- items [Reporting Services], properties
ms.assetid: 21edec6d-9897-48fb-8c75-182305b1dbdb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6ed8a56892cfd70b43341ffff8349faa56094a97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62519142"
---
# <a name="report-server-item-properties"></a>レポート サーバー アイテムのプロパティ
  アイテム プロパティは、レポート サーバー データベースのアイテムに固有のプロパティです。 アイテム プロパティには、レポート、リンク レポート、フォルダー、リソース、モデル、データ ソースなどがあります。  
  
 次のアイテム プロパティ名は予約されています。 同じ名前のユーザー定義プロパティは作成できません。 レポート サーバー Web サービス メソッドを使用すると、これらのプロパティの多くを読み取ったり、修正したりできます。  
  
## <a name="item-properties"></a>アイテム プロパティ  
 次のプロパティは、レポート サーバー データベースのすべてのアイテムに適用されます。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|**CreatedBy**|レポート サーバー データベースへアイテムを最初に追加したユーザーの名前。|  
|**CreationDate**|アイテムがレポート サーバー データベースに追加された日付と時刻。|  
|**[説明]**|アイテムの説明。|  
|**[非表示]**|ユーザーがアイテムを表示および使用できるかどうかを示す値。|  
|**ID**|レポート サーバー データベースのアイテムの ID。|  
|**ModifiedBy**|レポート サーバー データベースのアイテムを最後に変更したユーザーの名前。|  
|**ModifiedDate**|ユーザーがアイテムを最後に変更した日付と時刻。|  
|**名前**|レポート サーバー データベースのアイテムの名前。|  
|**[パス]**|アイテムの完全なパス名です。 レポート サーバー データベースのアイテムのパスの長さは最大 260 字です。|  
|**Size**|レポート サーバー データベースのアイテムのサイズ (バイト単位)。|  
|**型**|レポート サーバー データベースのアイテムの種類。|  
|**VirtualPath**|レポート サーバー データベースのアイテムの仮想パス。 <xref:ReportService2010.CatalogItem.VirtualPath%2A> プロパティの値は、ユーザーがそのアイテムを表示するときに使用するパスです。 たとえば、report1 というレポートがユーザーの個人的な My Reports フォルダー内にある場合、仮想パスは /My Reports となります。 アイテムの実際のパスは /Users/username/My Reports です。|  
  
## <a name="folder-properties"></a>フォルダー プロパティ  
 これまで説明したアイテム プロパティの他に、次のプロパティがレポート サーバー データベースのフォルダーに適用されます。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|**Reserved**|フォルダーの <xref:ReportService2010.ReportingService2010.GetProperties%2A> メソッドが返す値は、レポート サーバーによって予約されています。 予約されたフォルダーには Users、My Reports、および / が含まれています。 予約されたフォルダーは、変更も削除もできません。|  
  
## <a name="report-properties"></a>レポート プロパティ  
 これまで説明したアイテム プロパティの他に、次のプロパティがレポート サーバー データベースのレポートに適用されます。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|**言語**|レポートで使用される言語。 値は、Internet Engineering Task Force (IETF) RFC1766 仕様で定義されている言語コードです。 先頭の 2 文字は基本言語を指定します。 ハイフンで区切られた 2 番目の部分は、言語のバリエーションや方言を指定します。 レポート定義の `Style` 要素に関連付けられた `Body` 要素に値が指定されていない場合は、既定値がレポート サーバーの言語になります。|  
|`ReportProcessingTimeout`|各レポートのタイムアウト値 (秒単位)。 この値を設定すると、指定した時間が経過した時点でレポートの処理が中止されます。 有効値は `-1` ～ `2`、`147`、`483`、`647` です。 値が `-1` の場合、処理中にレポートがタイムアウトしません。 値が場合`null`、システム プロパティの値`ReportProcessingTimeout`レポート処理のタイムアウトのために使用します。既定値は `null` です。 詳細については、「[レポート サーバーのシステム プロパティ](reporting-services-properties-report-server-system-properties.md)」を参照してください。|  
|**ExecutionDate**|レポートのスナップショットが最後に作成された日付と時刻。|  
|**CanRunUnattended**|スケジュールに基づいてレポートを自動実行できるかどうかを示す値。 このプロパティを `true` に設定すると、レポート パラメーターの既定値が定義され、データ ソースの資格情報がレポートと一緒に格納されるか、資格情報取得オプションが `None` に設定されます。 このプロパティを `false` に設定すると、レポートを自動実行するための前提条件が満たされません。 「[自動実行アカウントを構成する &#40;SSRS 構成マネージャー&#41;](../../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。|  
|**HasParameterDefaultValues**|レポートのすべてのレポート パラメーターが有効な既定値に設定されているかどうかを示す値。 レポートにレポート パラメーターがない場合も、値は `true` です。 このプロパティが `false` に設定されている場合は、1 つ以上のレポート パラメーターに有効な既定値がありません。|  
|**HasDataSourceCredentials**|レポートに関連付けられているすべてのデータ ソースの資格情報取得オプション セットが `None` または `Store` であることを示す値。 このプロパティが `false` に設定されている場合は、レポートに関連付けられているいずれかのデータ ソースの資格情報取得オプション セットが `Integrated` または `Prompt` です。|  
|**IsSnapshotExecution**|レポートがスナップショットであるかどうかを示す値。|  
|**HasScheduleReadyDataSources**|レポートのデータ ソースが、実行スケジュールをサポートするように構成されているかどうかを示す値。 このプロパティが `false` に設定されている場合、ユーザーはレポートをサブスクライブできません。|  
  
## <a name="resource-properties"></a>リソース プロパティ  
 これまで説明したアイテム プロパティの他に、次のプロパティがレポート サーバー データベースのリソースに適用されます。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|**MimeType**|レポート サーバー データベースのリソースの MIME の種類。|  
  
## <a name="see-also"></a>参照  
 [Web サービスと .NET Framework を使用してのアプリケーションの構築](building-applications-using-the-web-service-and-the-net-framework.md)   
 [レポート サーバー Web サービス](../report-server-web-service.md)   
 [テクニカル リファレンス (SSRS)](../../technical-reference-ssrs.md)  
  
  
