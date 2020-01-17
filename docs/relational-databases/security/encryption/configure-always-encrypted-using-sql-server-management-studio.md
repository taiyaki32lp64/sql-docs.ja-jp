---
title: SSMS を使用した Always Encrypted の構成
description: SQL Server Management Studio (SSMS) を使用して Always Encrypted データベースを構成し、管理するためのタスクについて説明します。
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c033cf8200103fe6198661f7ed0e3e2a6c3966a
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557869"
---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>SQL Server Management Studio を使用した Always Encrypted の構成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、 [SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md)を使用して Always Encrypted を構成し、Always Encrypted を使用したデータベースを管理するためのタスクについて説明します。

## <a name="security-considerations-when-using-ssms-to-configure-always-encrypted"></a>SSMS を使用して Always Encrypted を構成するときのセキュリティに関する考慮事項

SSMS を使用して Always Encrypted を構成する場合、SSMS によって Always Encrypted のキーと機密データの両方が処理されます。結果、キーとデータは両方とも SSMS プロセス内ではプレーンテキストの形式で表示されます。 したがって、セキュリティで保護されたコンピューターで SSMS を実行することが重要です。 データベースが SQL Server でホストされている場合は、SQL Server インスタンスをホストするコンピューターとは異なるコンピューターで SSMS を実行する必要があります。 Always Encrypted の主な目的は、データベース システムが侵害されても、暗号化された機密データが確実に保護されるようにすることにあるので、SQL Server コンピューター上でキーまたは機密データを処理する PowerShell スクリプトが実行されると、機能の効果が低下したり無効になったりするおそれがあります。 追加の推奨事項については、 [Security Considerations for Key Management](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)(キー管理でのセキュリティに関する考慮事項) を参照してください。

SSMS では、データベースを管理するユーザー (DBA) と、暗号化された機密情報を管理し、プレーンテキスト データへのアクセス権を持つユーザー (セキュリティ管理者かアプリケーション管理者または両者) の間で、ロールの分離はサポートされていません。 組織でロールの分離が実施される場合は、PowerShell を使用して Always Encrypted を構成する必要があります。 詳細については、「[Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」および「[PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)」を参照してください。 

## <a name="always-encrypted-tasks-using-ssms"></a>SSMS を使用した Always Encrypted のタスク

- [SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)
- [SQL Server Management Studio を使用して Always Encrypted キーを交換する](rotate-always-encrypted-keys-using-ssms.md)
- [Always Encrypted ウィザードを使用して列暗号化を構成する](always-encrypted-wizard.md)
- [DAC パッケージでの Always Encrypted を使用した列暗号化の構成](configure-always-encrypted-using-dacpac.md)
- [SQL Server Management Studio で Always Encrypted を使用した列のクエリを実行する](always-encrypted-query-columns-ssms.md)
- [Always Encrypted を使用したデータベースのエクスポートとインポート](always-encrypted-migrate-using-bacpac.md)
- [Always Encrypted を使用したデータベースのバックアップと復元](always-encrypted-migrate-using-backup-restore.md)
- [SQL Server インポートおよびエクスポート ウィザードで Always Encrypted を使用して列間でデータを移行する](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>参照
- [常に暗号化](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [PowerShell を使用した Always Encrypted の構成](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)
