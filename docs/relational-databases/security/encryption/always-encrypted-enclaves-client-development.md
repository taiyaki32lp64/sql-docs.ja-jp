---
title: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7ec032a9a6bd6d02372d77d8844d5e4938fbe945
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74492005"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使うと、[Always Encrypted](always-encrypted-database-engine.md) が拡張され、暗号化された機密データベース列に対するアプリケーション クエリの高度な機能が有効になります。 セキュリティで保護されたエンクレーブのテクノロジを利用することで、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] のクエリ Executor は、暗号化された列に対する計算を、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] プロセス内のセキュリティで保護されたエンクレーブにデリゲートできるようになります。

## <a name="client-driver-for-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted 用のクライアント ドライバー

セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用してアプリケーションを開発するには、セキュリティで保護されたエンクレーブがサポートされているバージョンの SQL クライアント ドライバーが必要です。 クライアント ドライバーでは、次の重要な役割が行われます。
- セキュリティで保護されたエンクレーブを使用するクエリが実行のために [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] に送信される前に、ドライバーによってエンクレーブの構成証明が開始され、セキュリティで保護されたエンクレーブが信頼できること、および機密データの処理に安全に使用できることが確認されます。 構成証明について詳しくは、「[セキュリティで保護されたエンクレーブの構成証明](always-encrypted-enclaves.md#secure-enclave-attestation)」をご覧ください。
- 構成証明が成功すると、クライアント ドライバーにより、共有シークレットをネゴシエートすることで、エンクレーブとのセキュリティで保護されたセッションが確立されます。
- ドライバーでは、共有シークレットを使用して、エンクレーブがクエリを処理するために必要な列暗号化キーが暗号化され、そのキーが [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] に送信されます。そこからキーは、キーの暗号化解除が行われるセキュリティで保護されたエンクレーブに転送されます。 
- 最後に、ドライバーによって実行のためにクエリが送信され、セキュリティで保護されたエンクレーブ内で計算がトリガーされます。

セキュリティで保護されたエンクレーブの機能を使用するには、データベースへの接続時にエンクレーブの計算を有効にするようにアプリケーションとクライアント ドライバーを構成し、エンクレーブの構成証明サービスをポイントする構成証明サービスのエンドポイント (エンクレーブ構成証明 URL) を指定する必要があります。 詳細は、使用しているドライバーと構成証明サービス/プロトコルによって異なります。

## <a name="next-steps"></a>次のステップ

セキュリティで保護されたエンクレーブが設定された Always Encrypted は、次のクライアント ドライバーでサポートされます。
- .NET Framework 4.7.2 以降の .NET Framework Data Provider for SQL Server 
    - 詳しくは、「[Always Encrypted と .NET Framework Data Provider for SQL Server を使用する](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)」をご覧ください。
    - 詳しいチュートリアルについては、「[チュートリアル: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET Framework アプリケーションの開発](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)
- .NET Framework 4.6 以降および .NET Core 2.1 以降の Microsoft .NET Data Provider for SQL Server 
    - 詳しくは、「[Always Encrypted と Microsoft .NET Data Provider for SQL Server を使用する](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)」をご覧ください。
    - 詳しいチュートリアルについては、「[チュートリアル: セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する .NET アプリケーションの開発](../../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)」をご覧ください。
- Microsoft ODBC Driver for SQL Server バージョン 17.4 以降。 
    - 詳しくは、「[Using Always Encrypted with the ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)」(ODBC ドライバーでの Always Encrypted の使用) をご覧ください。 
    - ODBC を使用するデータベース接続でエンクレーブ計算を有効にする方法については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves)」をご覧ください。
