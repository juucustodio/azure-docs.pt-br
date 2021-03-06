---
title: Solucionar problemas de volumes SMB ou de protocolo duplo para Azure NetApp Files | Microsoft Docs
description: Descreve mensagens de erro e resoluções que podem ajudá-lo a solucionar problemas de SMB ou de protocolo duplo para Azure NetApp Files.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''
ms.assetid: ''
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 02/02/2021
ms.author: b-juche
ms.openlocfilehash: 237fb514229f370fcba79133232e80a6a655048f
ms.sourcegitcommit: 126ee1e8e8f2cb5dc35465b23d23a4e3f747949c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/10/2021
ms.locfileid: "100104409"
---
# <a name="troubleshoot-smb-or-dual-protocol-volumes"></a>Solucionar problemas de volumes SMB ou de protocolo duplo

Este artigo descreve as resoluções para condições de erro que você pode ter ao criar ou gerenciar volumes de protocolo duplo.

## <a name="errors-for-dual-protocol-volumes"></a>Erros para volumes de protocolo duplo

|     Condições de erro    |     Resoluções    |
|-|-|
| O LDAP sobre TLS está habilitado e a criação de volume de protocolo duplo falha com o erro `This Active Directory has no Server root CA Certificate` .    |     Se esse erro ocorrer quando você estiver criando um volume de protocolo duplo, certifique-se de que o certificado de autoridade de certificação raiz seja carregado em sua conta do NetApp.    |
| A criação de volume de protocolo duplo falha com o erro `Failed to validate LDAP configuration, try again after correcting LDAP configuration` .    |  O registro de ponteiro (PTR) do computador host do AD pode estar ausente no servidor DNS. Você precisa criar uma zona de pesquisa inversa no servidor DNS e, em seguida, adicionar um registro PTR da máquina host do AD nessa zona de pesquisa inversa. <br> Por exemplo, suponha que o endereço IP do computador do AD seja `10.X.X.X` , o nome do host do computador do AD (como encontrado usando o `hostname` comando) é `AD1` , e que é `contoso.com` .  O registro PTR adicionado à zona de pesquisa inversa deve ser `10.X.X.X`  ->  `contoso.com` .   |
| A criação de volume de protocolo duplo falha com o erro `Failed to create the Active Directory machine account \\\"TESTAD-C8DD\\\". Reason: Kerberos Error: Pre-authentication information was invalid Details: Error: Machine account creation procedure failed\\n [ 434] Loaded the preliminary configuration.\\n [ 537] Successfully connected to ip 10.X.X.X, port 88 using TCP\\n**[ 950] FAILURE` . |     Esse erro indica que a senha do AD está incorreta quando Active Directory é unida à conta do NetApp. Atualize a conexão do AD com a senha correta e tente novamente. |
| A criação de volume de protocolo duplo falha com o erro `Could not query DNS server. Verify that the network configuration is correct and that DNS servers are available` . |   Esse erro indica que o DNS não está acessível. O motivo pode ser porque o IP do DNS está incorreto ou há um problema de rede. Verifique o IP do DNS inserido na conexão do AD e verifique se o IP está correto. <br> Além disso, certifique-se de que o AD e o volume estejam na mesma região e na mesma VNet. Se estiverem em VNETs diferentes, verifique se o emparelhamento VNet é estabelecido entre os dois VNets.|
| A permissão é negada ao montar um volume de protocolo duplo. | Um volume de protocolo duplo dá suporte aos protocolos NFS e SMB.  Quando você tenta acessar o volume montado no sistema UNIX, o sistema tenta mapear o usuário do UNIX que você usa para um usuário do Windows. Se nenhum mapeamento for encontrado, o erro "permissão negada" ocorrerá. <br> Essa situação se aplica também quando você usa o usuário ' raiz ' para o acesso. <br> Para evitar o problema de "permissão negada", verifique se o Windows Active Directory inclui `pcuser` antes de acessar o ponto de montagem. Se você adicionar `pcuser` depois de encontrar o problema de "permissão negada", Aguarde 24 horas para que a entrada do cache seja limpa antes de tentar acessar novamente. |

## <a name="common-errors-for-smb-and-dual-protocol-volumes"></a>Erros comuns para volumes SMB e de protocolo duplo

|     Condições de erro    |     Resoluções    |
|-|-|
| A criação de volume SMB ou de protocolo duplo falha com o seguinte erro: <br> `{"code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.","details":[{"code":"InternalServerError", "message":"Error when creating - Could not query DNS server. Verify that the network configuration is correct and that DNS servers are available."}]}` | Esse erro indica que o DNS não está acessível. <br> Considere as seguintes soluções: <ul><li>Verifique se o ADDS e o volume estão sendo implantados na mesma região.</li> <li>Verifique se o ADDS e o volume estão usando a mesma VNet. Se eles estiverem usando VNETs diferentes, verifique se os VNets estão emparelhados entre si. Consulte as [diretrizes para Azure NetApp files planejamento de rede](azure-netapp-files-network-topologies.md). </li> <li>O servidor DNS pode ter NSGs (grupos de segurança de rede) aplicados.  Como tal, ele não permite que o tráfego flua. Nesse caso, abra o NSGs para o DNS ou o AD para se conectar a várias portas. Para requisitos de porta, consulte [requisitos para conexões de Active Directory](azure-netapp-files-create-volumes-smb.md#requirements-for-active-directory-connections). </li></ul> <br>As mesmas soluções se aplicam ao Azure ADDS. O Azure ADDS deve ser implantado na mesma região. A VNet deve estar na mesma região ou emparelhada com a VNet usada pelo volume. | 
| A criação de volume SMB ou de protocolo duplo falha com o seguinte erro: <br> `{"code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.","details":[{"code":"InternalServerError", "message":"Error when creating - Failed to create the Active Directory machine account \"SMBTESTAD-C1C8\". Reason: Kerberos Error: Invalid credentials were given Details: Error: Machine account creation procedure failed\n [ 563] Loaded the preliminary configuration.\n**[ 670] FAILURE: Could not authenticate as 'test@contoso.com':\n** Unknown user (KRB5KDC_ERR_C_PRINCIPAL_UNKNOWN)\n. "}]}`  |  <ul><li>Certifique-se de que o nome de usuário inserido está correto. </li> <li>Verifique se o usuário faz parte do grupo de administradores que tem o privilégio para criar contas de computador. </li> <li> Se você usar o Azure ADDS, verifique se o usuário faz parte do grupo do Azure AD `Azure AD DC Administrators` . </li></ul> | 
| A criação de volume SMB ou de protocolo duplo falha com o seguinte erro: <br> `{"code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.","details":[{"code":"InternalServerError", "message":"Error when creating - Failed to create the Active Directory machine account \"SMBTESTAD-A452\". Reason: Kerberos Error: Pre-authentication information was invalid Details: Error: Machine account creation procedure failed\n [ 567] Loaded the preliminary configuration.\n [ 671] Successfully connected to ip 10.X.X.X, port 88 using TCP\n**[ 1099] FAILURE: Could not authenticate as\n** 'user@contoso.com': CIFS server account password does\n** not match password stored in Active Directory\n** (KRB5KDC_ERR_PREAUTH_FAILED)\n. "}]}` | Certifique-se de que a senha inserida para ingressar na conexão do AD esteja correta. |
| A criação de volume SMB ou de protocolo duplo falha com o seguinte erro: `{"code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.","details":[{"code":"InternalServerError","message":"Error when creating - Failed to create the Active Directory machine account \"SMBTESTAD-D9A2\". Reason: SecD Error: ou not found Details: Error: Machine account creation procedure failed\n [ 561] Loaded the preliminary configuration.\n [ 665] Successfully connected to ip 10.X.X.X, port 88 using TCP\n [ 1039] Successfully connected to ip 10.x.x.x, port 389 using TCP\n**[ 1147] FAILURE: Specifed OU 'OU=AADDC Com' does not exist in\n** contoso.com\n. "}]}` | Verifique se o caminho da UO especificado para ingressar na conexão do AD está correto. Se você usar o Azure ADDS, verifique se o caminho da unidade organizacional é `OU=AADDC Computers` . |

## <a name="next-steps"></a>Próximas etapas  

* [Criar um volume SMB](azure-netapp-files-create-volumes-smb.md)
* [Criar um volume de protocolo duplo](create-volumes-dual-protocol.md)
* [Configurar um cliente NFS para o Azure NetApp Files](configure-nfs-clients.md)
