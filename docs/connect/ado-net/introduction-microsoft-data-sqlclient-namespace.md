---
title: Microsoft.Data.SqlClient 名前空間の概要
description: Microsoft. Data. SqlClient 名前空間の [概要] ページ。
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4f4034c557c13054dcfb6ed425ca996b0c5363f6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452384"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 名前空間の概要

![Download-DownArrow-Circled](../../ssdt/media/download.png)[ADO.NET をダウンロードする](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

このページでは、既存の system.string 名前空間に対して追加の機能を提供する方法について説明します。
  
## <a name="release-notes"></a>リリース ノート
すべてのリリースノートは、 [GitHub リポジトリ](https://github.com/dotnet/SqlClient/tree/master/release-notes)で入手できます。

## <a name="new-features"></a>新しい機能

### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>.NET Framework 4.7.2 よりも新しい機能

データ分類-CTP 2.0 以降、Azure SQL Database および Microsoft SQL Server 2019 で利用できます。

UTF-8 サポート-CTP 2.3 以降、Microsoft SQL Server SQL Server 2019 で利用できます。

### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>.NET Core 2.2 を超える新機能

データ分類-CTP 2.0 以降、Azure SQL Database および Microsoft SQL Server 2019 で利用できます。

UTF-8 サポート-CTP 2.3 以降、Microsoft SQL Server SQL Server 2019 で利用できます。

Enclaves を使用した Always Encrypted Always Encrypted は Microsoft SQL Server 2016 以降で使用できます。 エンクレーブサポートは、Microsoft Sql Server 2019 CTP 2.0 で導入されました。

認証-パスワード認証モードを Active Directory します。

### <a name="data-classification"></a>データ分類

データ分類では、基になるソースが機能をサポートし、[データの機密度に関するメタデータが含まれている場合に、SqlDataReader 経由で取得したオブジェクトに関する読み取り専用のデータの秘密度と分類情報を公開する新しい api のセットを使用します。分類](../../relational-databases/security/sql-data-discovery-and-classification.md)。

```csharp
public class SqlDataReader
{
    public Microsoft.Data.SqlClient.DataClassification.SensitivityClassification SensitivityClassification
}

namespace Microsoft.Data.SqlClient.DataClassification
{
    public class ColumnSensitivity
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.SensitivityProperty> SensitivityProperties
    }
    public class InformationType
    {
        public string Id
        public string Name
    }
    public class Label
    {
        public string Id
        public string Name
    }
    public class SensitivityClassification
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.ColumnSensitivity> ColumnSensitivities
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.InformationType> InformationTypes
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.Label> Labels
    }
    public class SensitivityProperty
    {
        public Microsoft.Data.SqlClient.DataClassification.InformationType InformationType
        public Microsoft.Data.SqlClient.DataClassification.Label Label
    }
}
```

### <a name="utf-8-support"></a>UTF-8 のサポート

UTF-8 のサポートでは、アプリケーションコードを変更する必要はありません。 これらの SqlClient の変更は、サーバーが UTF-8 をサポートし、基になる列の照合順序が UTF-8 である場合に、クライアントとサーバー間の通信を最適化するだけです。 [SQL Server 2019 preview の新機能](../../sql-server/what-s-new-in-sql-server-ver15.md)の「utf-8」セクションを参照してください。

### <a name="always-encrypted-with-enclaves"></a>常に enclaves で暗号化

一般に、.NET Framework**および組み込み列マスターキーストアプロバイダー**を使用する既存のドキュメントも、.net Core で動作するようになりました。

 [Always Encrypted と .NET Framework Data Provider を使用して開発する](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: Windows 証明書ストアで機微なデータを保護し、暗号化キーを保存する](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>認証

_認証_接続文字列オプションを使用して、さまざまな認証モードを指定できます。 詳細については、 [SqlAuthenticationMethod のドキュメント](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2)を参照してください。

> [!NOTE]
> Azure Key Vault プロバイダーのようなカスタムキーストアプロバイダーは、Microsoft. Data. SqlClient をサポートするように更新する必要があります。 同様に、エンクレーブプロバイダーも更新して、Microsoft. Data. SqlClient をサポートする必要があります。
> Always Encrypted は、.NET Framework および .NET Core ターゲットに対してのみサポートされます。 .NET Standard に特定の暗号化の依存関係がないため、.NET Standard に対してはサポートされません。
