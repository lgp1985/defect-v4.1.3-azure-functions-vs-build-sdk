# defect-v4.1.3-azure-functions-vs-build-sdk
This repo is to demonstrate faulty `Microsoft.NET.Sdk.Functions` v4.1.3 in Windows 10.
Theres 2 Function Apps in the solution, the only diference is the update performed via Manage NuGet Packages... > Updates.

The [FunctionApp1](/Azure-functions-defect/FunctionApp1) is OOTB project created with Visual Studio 2022 wizard.

The [FunctionApp2](/Azure-functions-defect/FunctionApp2) only difference is that after created I gone to Manage NuGet Packages... > Updates and accepted the update of _Microsoft.NET.Sdk.Functions_ to its latest version.
Same steps as in [this video](https://user-images.githubusercontent.com/810024/196772668-5c9d55da-7af4-441c-ba3f-62784b7c13a3.mp4).

## More info about environment
Worth mentioning that both projects works under Windows 11
```log
PowerShell 7.2.7
Copyright (c) Microsoft Corporation.

https://aka.ms/powershell
Type 'help' to get help.

PS C:\Users\lgp19> systeminfo

Nome do host:                              AERO-DO-LG
Nome do sistema operacional:               Microsoft Windows 11 Pro
Versão do sistema operacional:             10.0.22621 N/A compilação 22621
Fabricante do sistema operacional:         Microsoft Corporation
Configuração do SO:                        Estação de trabalho autônoma
Tipo de compilação do sistema operacional: Multiprocessor Free
Proprietário registrado:                   lgp1985@outlook.com
Organização registrada:                    N/A
Identificação do produto:                  00330-81483-80974-AA534
Data da instalação original:               21/10/2022, 11:03:21
Tempo de Inicialização do Sistema:         26/10/2022, 09:33:39
Fabricante do sistema:                     GIGABYTE
Modelo do sistema:                         AERO 16 XE5
Tipo de sistema:                           x64-based PC
Processador(es):                           1 processador(es) instalado(s).
                                           [01]: Intel64 Family 6 Model 154 Stepping 3 GenuineIntel ~2300 Mhz
Versão do BIOS:                            American Megatrends International, LLC. FB0A, 13/09/2022
Pasta do Windows:                          C:\WINDOWS
Pasta do sistema:                          C:\WINDOWS\system32
Inicializar dispositivo:                   \Device\HarddiskVolume1
Localidade do sistema:                     pt-br;Português (Brasil)
Localidade de entrada:                     en-us;Inglês (Estados Unidos)
Fuso horário:                              (UTC-03:00) Brasília
Memória física total:                      65.197 MB
Memória física disponível:                 48.257 MB
Memória Virtual: Tamanho Máximo:           74.925 MB
Memória Virtual: Disponível:               55.866 MB
Memória Virtual: Em Uso:                   19.059 MB
Local(is) de arquivo de paginação:         C:\pagefile.sys
Domínio:                                   WORKGROUP
Servidor de Logon:                         \\AERO-DO-LG
Hotfix(es):                                3 hotfix(es) instalado(s).
                                           [01]: KB5017271
                                           [02]: KB5019509
                                           [03]: KB5017233
Placa(s) de Rede:                          4 NIC(s) instalado(s).
                                           [01]: Xbox Wireless Adapter for Windows
                                                 Nome da conexão: Ethernet
                                                 DHCP ativado:    Não
                                                 Endereço(es) IP
                                           [02]: Realtek USB GbE Family Controller
                                                 Nome da conexão: Ethernet 2
                                                 Status:          Mídia desconectada
                                           [03]: Intel(R) Wi-Fi 6E AX210 160MHz
                                                 Nome da conexão: Wi-Fi
                                                 DHCP ativado:    Sim
                                                 Servidor DHCP:   192.168.1.1
                                                 Endereço(es) IP
                                                 [01]: 192.168.1.81
                                                 [02]: fe80::97e9:b7ce:b2c4:ea13
                                                 [03]: 2001:1284:f013:3278:306d:90d9:9bca:91cb
                                                 [04]: 2001:1284:f013:3278:1bd7:f5b1:ccf7:ae3a
                                           [04]: Bluetooth Device (Personal Area Network)
                                                 Nome da conexão: Conexão de Rede Bluetooth
                                                 Status:          Mídia desconectada
Requisitos do Hyper-V:                     Hipervisor detectado. Recursos necessários para o Hyper-V não serão exibidos.
PS C:\Users\lgp19>
```

VS2022 info
```log
Microsoft Visual Studio Enterprise 2022
Version 17.3.6
VisualStudio.17.Release/17.3.6+32929.385
Microsoft .NET Framework
Version 4.8.09032

Installed Version: Enterprise

ASP.NET and Web Tools   17.3.376.3011
ASP.NET and Web Tools

Azure App Service Tools v3.0.0   17.3.376.3011
Azure App Service Tools v3.0.0

Azure Functions and Web Jobs Tools   17.3.376.3011
Azure Functions and Web Jobs Tools

C# Tools   4.3.0-3.22470.13+80a8ce8d5fdb9ceda4101e2acb8e8eb7be4ebcea
C# components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Common Azure Tools   1.10
Provides common services for use by Azure Mobile Services and Microsoft Azure Tools.

Microsoft Azure Tools for Visual Studio   2.9
Support for Azure Cloud Services projects

Microsoft JVM Debugger   1.0
Provides support for connecting the Visual Studio debugger to JDWP compatible Java Virtual Machines

NuGet Package Manager   6.3.0
NuGet Package Manager in Visual Studio. For more information about NuGet, visit https://docs.nuget.org/

Razor (ASP.NET Core)   17.0.0.2232702+e1d654e792aa2fe6646a6935bcca80ff0aff4387
Provides languages services for ASP.NET Core Razor.

SQL Server Data Tools   17.0.62207.04100
Microsoft SQL Server Data Tools

TypeScript Tools   17.0.10701.2001
TypeScript Tools for Microsoft Visual Studio

Visual Basic Tools   4.3.0-3.22470.13+80a8ce8d5fdb9ceda4101e2acb8e8eb7be4ebcea
Visual Basic components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Visual F# Tools   17.1.0-beta.22363.4+1b94f89d4d1f41f20f9be73c76f4b229d4e49078
Microsoft Visual F# Tools

Visual Studio IntelliCode   2.2
AI-assisted development for Visual Studio.
```

### But fails on Windows 10
```log
PowerShell 7.2.6
Copyright (c) Microsoft Corporation.

https://aka.ms/powershell
Type 'help' to get help.

   A new PowerShell stable release is available: v7.2.7
   Upgrade now, or check out the release page at:
     https://aka.ms/PowerShell-Release?tag=v7.2.7

PS C:\Users\C112029> systeminfo

Host Name:                 CPC-C1120-LYS23
OS Name:                   Microsoft Windows 10 Enterprise
OS Version:                10.0.19044 N/A Build 19044
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Member Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          N/A
Registered Organization:   N/A
Product ID:                00329-00000-00003-AA468
Original Install Date:     10/17/2022, 10:49:37 PM
System Boot Time:          10/19/2022, 1:50:37 PM
System Manufacturer:       Microsoft Corporation
System Model:              Virtual Machine
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: AMD64 Family 25 Model 1 Stepping 1 AuthenticAMD ~2445 Mhz
BIOS Version:              Microsoft Corporation Hyper-V UEFI Release v4.1, 5/9/2022
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume3
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC) Coordinated Universal Time
Total Physical Memory:     16,333 MB
Available Physical Memory: 5,534 MB
Virtual Memory: Max Size:  19,277 MB
Virtual Memory: Available: 3,031 MB
Virtual Memory: In Use:    16,246 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    flyfrontier.com
Logon Server:              \\F9CORCUSDC02
Hotfix(s):                 5 Hotfix(s) Installed.
                           [01]: KB5017022
                           [02]: KB5003791
                           [03]: KB5017308
                           [04]: KB5014032
                           [05]: KB5016705
Network Card(s):           1 NIC(s) Installed.
                           [01]: Microsoft Hyper-V Network Adapter
                                 Connection Name: Ethernet
                                 DHCP Enabled:    Yes
                                 DHCP Server:     168.63.129.16
                                 IP address(es)
                                 [01]: 10.70.80.10
                                 [02]: fe80::c07b:da6a:7311:5a8f
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.
PS C:\Users\C112029>
```

VS2022 info
```log
Microsoft Visual Studio Professional 2022
Version 17.3.6
VisualStudio.17.Release/17.3.6+32929.385
Microsoft .NET Framework
Version 4.8.04084

Installed Version: Professional

ADL Tools Service Provider   1.0
This package contains services used by Data Lake tools

ASA Service Provider   1.0

ASP.NET and Web Tools   17.3.376.3011
ASP.NET and Web Tools

Azure App Service Tools v3.0.0   17.3.376.3011
Azure App Service Tools v3.0.0

Azure Data Lake Tools for Visual Studio   2.6.5000.0
Microsoft Azure Data Lake Tools for Visual Studio

Azure Functions and Web Jobs Tools   17.3.376.3011
Azure Functions and Web Jobs Tools

Azure Stream Analytics Tools for Visual Studio   2.6.5000.0
Microsoft Azure Stream Analytics Tools for Visual Studio

C# Tools   4.3.0-3.22470.13+80a8ce8d5fdb9ceda4101e2acb8e8eb7be4ebcea
C# components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Common Azure Tools   1.10
Provides common services for use by Azure Mobile Services and Microsoft Azure Tools.

Microsoft Azure Hive Query Language Service   2.6.5000.0
Language service for Hive query

Microsoft Azure Stream Analytics Language Service   2.6.5000.0
Language service for Azure Stream Analytics

Microsoft Azure Tools for Visual Studio   2.9
Support for Azure Cloud Services projects

Microsoft JVM Debugger   1.0
Provides support for connecting the Visual Studio debugger to JDWP compatible Java Virtual Machines

Node.js Tools   1.5.40629.1 Commit Hash:3f5cc0329815af3ffb948f08857446d206a9af36
Adds support for developing and debugging Node.js apps in Visual Studio

NuGet Package Manager   6.3.0
NuGet Package Manager in Visual Studio. For more information about NuGet, visit https://docs.nuget.org/

Razor (ASP.NET Core)   17.0.0.2232702+e1d654e792aa2fe6646a6935bcca80ff0aff4387
Provides languages services for ASP.NET Core Razor.

SQL Server Data Tools   17.0.62207.04100
Microsoft SQL Server Data Tools

ToolWindowHostedEditor   1.0
Hosting json editor into a tool window

TypeScript Tools   17.0.10701.2001
TypeScript Tools for Microsoft Visual Studio

Visual Basic Tools   4.3.0-3.22470.13+80a8ce8d5fdb9ceda4101e2acb8e8eb7be4ebcea
Visual Basic components used in the IDE. Depending on your project type and settings, a different version of the compiler may be used.

Visual F# Tools   17.1.0-beta.22363.4+1b94f89d4d1f41f20f9be73c76f4b229d4e49078
Microsoft Visual F# Tools

Visual Studio IntelliCode   2.2
AI-assisted development for Visual Studio.
```
