---
title: ADO.NET の新機能
ms.date: 03/30/2017
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
ms.openlocfilehash: 0a02ca3885524c5fcf8def603acdce33a972d283
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791263"
---
# <a name="whats-new-in-adonet"></a>ADO.NET の新機能

.NET Framework 4.5 の ADO.NET には、次の新機能が追加されています。

## <a name="sqlclient-data-provider"></a>SqlClient Data Provider

次の機能は、.NET Framework 4.5 の SQL Server の .NET Framework Data Provider に新しく追加されています。

- ConnectRetryCount と ConnectRetryInterval の接続文字列キーワード (<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>) を使用すると、アイドル状態の接続の復元機能を制御できます。

- SQL Server からアプリケーションへのストリーミングサポートでは、サーバー上のデータが非構造化であるシナリオがサポートされます。  詳細については、「 [SqlClient Streaming Support](sqlclient-streaming-support.md) 」を参照してください。

- 非同期のプログラミングにサポートが追加されています。  詳細については、「[非同期プログラミング](asynchronous-programming.md)」を参照してください。

- 接続エラーは、拡張イベント ログに記録されるようになりました。 詳細については、「[ADO.NET のデータ追跡](data-tracing.md)」を参照してください。

- SqlClient で SQL Server の高可用性、ディザスターリカバリー機能、AlwaysOn がサポートされるようになりました。 詳細については、「[高可用性、ディザスターリカバリーのための SqlClient サポート](./sql/sqlclient-support-for-high-availability-disaster-recovery.md)」を参照してください。

- SQL Server 認証を使用する場合は<xref:System.Security.SecureString> 、パスワードをとして渡すことができます。 詳細については、「<xref:System.Data.SqlClient.SqlCredential>」を参照してください。

- `TrustServerCertificate` が`Encrypt` false であり、が true の場合、SQL Server の SSL 証明書のサーバー名 (または ip アドレス) は、接続文字列で指定されているサーバー名 (または ip アドレス) と完全に一致する必要があります。 それ以外の場合、接続試行は失敗します。 詳細については、「`Encrypt`」の <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 接続オプションの説明を参照してください。

  この変更によって既存のアプリケーションが接続しなくなる場合、次のいずれかを使用してアプリケーションを修正できます。

  - 共通名 (CN) またはサブジェクト代替名 (SAN) フィールドに短い名前を指定する証明書を発行します。 このソリューションは、データベース ミラーリングをする場合に有効です。

  - 短い名前を完全修飾ドメイン名にマップする別名を追加します。

  - 接続文字列では完全修飾ドメイン名を使用します。

- SqlClient は拡張保護をサポートしています。 拡張保護の詳細については、「[拡張保護を使用したデータベースエンジンへの接続](https://go.microsoft.com/fwlink/?LinkId=219978)」を参照してください。

- SqlClient は LocalDB データベースへの接続をサポートします。 詳細については、「 [LocalDB の SqlClient サポート](./sql/sqlclient-support-for-localdb.md)」を参照してください。

- `Type System Version=SQL Server 2012;` は、`Type System Version` 接続プロパティに渡す新しい値です。 `Type System Version=Latest;` 値は廃止されており、`Type System Version=SQL Server 2008;` と同等になっています。 詳細については、「<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。

- SqlClient は、スパース列に追加のサポートを提供します。このサポートは SQL Server 2008 で追加された機能です。 アプリケーションがスパース列を使用するテーブルのデータに既にアクセスしていると、パフォーマンスが向上します。 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> の IsColumnSet 列は、列が列セットのメンバーであるスパース列であるかどうかを示します。 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>列がスパース列であるかどうかを示します (詳細については[SQL Server スキーマコレクション](sql-server-schema-collections.md)を参照してください)。 スパース列の詳細については、「[スパース列の使用](https://go.microsoft.com/fwlink/?LinkId=224244)」を参照してください。

- 空間データ型を含むアセンブリ Microsoft.SqlServer.Types.dll は、Version 10.0 から Version 11.0 にアップグレードされました。 このアセンブリを参照するホスト アプリケーションでは、エラーが発生する可能性があります。 詳細については、「[データベースエンジン機能における重大な変更](https://go.microsoft.com/fwlink/?LinkId=224367)」を参照してください。

## <a name="adonet-entity-framework"></a>ADO.NET Entity Framework

.NET Framework 4.5 は、Entity Framework 5.0 を使用する場合に新しいシナリオを可能にする Api を追加します。 Entity Framework 5.0 に追加された改善点と機能の詳細については、次のトピックを参照してください。[新機能](https://go.microsoft.com/fwlink/?LinkID=251106)と[Entity Framework のリリースとバージョン管理](https://go.microsoft.com/fwlink/?LinkId=234899)について説明します。

## <a name="see-also"></a>関連項目

- [ADO.NET](index.md)
- [ADO.NET の概要](ado-net-overview.md)
- [SQL Server と ADO.NET](./sql/index.md)
- [WCF Data Services 5.0 の新機能](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))
