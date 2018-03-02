---
title: Matrice di supporto di Azure Site Recovery per la replica in Azure | Microsoft Docs
description: Riepiloga i sistemi operativi e componenti supportati per Azure Site Recovery
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/06/2018
ms.author: rajanaki
ms.openlocfilehash: a17d0918ea5938daf81c469fd6402a7dc9764831
ms.sourcegitcommit: d87b039e13a5f8df1ee9d82a727e6bc04715c341
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/21/2018
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-to-azure"></a>Matrice di supporto di Azure Site Recovery per la replica da locale ad Azure


In questo articolo vengono riepilogati le configurazioni e i componenti supportati per Azure Site Recovery durante la replica e il ripristino in Azure. Per altre informazioni sui requisiti di Azure Site Recovery, vedere i [prerequisiti](site-recovery-prereq.md).

> [!NOTE]
> Assicurarsi di eseguire l'aggiornamento alla versione più recente dell'agente e del provider di Site Recovery per ottenere la compatibilità con gli aggiornamenti nella matrice di supporto.


## <a name="support-for-deployment-options"></a>Supporto per opzioni di distribuzione

**Distribuzione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)** |
--- | --- | ---
**Portale di Azure** | Macchine virtuali VMware locali in Archiviazione di Azure, con Azure Resource Manager o archiviazione e reti classiche.<br/><br/> Failover in VM classiche o basate su Resource Manager. | VM Hyper-V locali in Archiviazione di Azure, con Resource Manager o archiviazione e reti classiche.<br/><br/> Failover in VM classiche o basate su Resource Manager.
**Portale classico** | Solo modalità manutenzione. Non è possibile creare nuovi insiemi di credenziali. | Solo modalità manutenzione.
**PowerShell** | Supportato | Supportato


## <a name="support-for-datacenter-management-servers"></a>Supporto per server di gestione dei data center

### <a name="virtualization-management-entities"></a>Entità di gestione della virtualizzazione

**Distribuzione** | **Supporto**
--- | ---
**Server fisico/VM VMware** | vCenter 6.5, 6.0 o 5.5
**Hyper-V (con Virtual Machine Manager)** | System Center Virtual Machine Manager 2016 e System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > Un cloud System Center Virtual Machine Manager 2016 con una combinazione di host Windows Server 2016 e 2012 R2 non è attualmente supportato.
  > Le configurazioni che includono l'aggiornamento di un SCVMM 2012 R2 esistente alla versione 2016 non sono attualmente supportate.
### <a name="host-servers"></a>Server host

**Distribuzione** | **Supporto**
--- | ---
**Server fisico/VM VMware** | vSphere 6.5, 6.0 e 5.5
**Hyper-V (con/senza Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 con gli aggiornamenti più recenti.<br></br>Se si usa SCVMM, gli host Windows Server 2016 dovranno essere gestiti da SCVMM 2016.


  >[!Note]
  >Un sito di Hyper-V con una combinazione di host che eseguono Windows Server 2016 e 2012 R2 non è attualmente supportato. Il ripristino in un percorso alternativo per le VM in un host Windows Server 2016 non è attualmente supportato.

## <a name="support-for-replicated-machine-os-versions"></a>Supporto per le versioni dei sistemi operativi dei computer replicati

In caso di replica in Azure, le macchine virtuali protette devono soddisfare i [requisiti di Azure](#failed-over-azure-vm-requirements).
La tabella seguente offre un riepilogo dei sistemi operativi replicati supportati nei vari scenari di distribuzione quando si usa Azure Site Recovery. Il supporto è applicabile per qualsiasi carico di lavoro in esecuzione nel sistema operativo indicato.

 **Server fisico/VMware** | **Hyper-V (con/senza VMM)** |
--- | --- |
Windows Server 2016 a 64 bit (Server Core, server con Esperienza desktop)\*, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 con almeno SP1<br/><br/> Red Hat Enterprise Linux: da 5.2 a 5.11, da 6.1 a 6.9, da 7.0 a 7.4<br/><br/>CentOS: da 5.2 a 5.11, da 6.1 a 6.9, da 7.0 a 7.4 <br/><br/>Server Ubuntu 14.04 LTS[ (versioni del kernel supportate)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Server Ubuntu 16.04 LTS[ (versioni del kernel supportate)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Debian 7 <br/><br/>Debian 8<br/><br/>Oracle Enterprise Linux 6.4 o 6.5 che esegue il kernel compatibile Red Hat o Unbreakable Enterprise Kernel versione 3 (UEK3) <br/><br/>SUSE Linux Enterprise Server 11 SP3 <br/><br/>SUSE Linux Enterprise Server 11 SP4 <br/>(L'aggiornamento dei computer di replica da SLES 11 SP3 a SLES 11 SP4 non è supportato. Se un computer replicato è stato aggiornato da 11SP3 SLES a SLES 11 SP4, è necessario disabilitare la replica e proteggere di nuovo il computer dopo l'aggiornamento.) | Qualsiasi sistema operativo guest [supportato da Azure](https://technet.microsoft.com/library/cc794868.aspx)

>[!NOTE]
>
> \*Windows Server 2016 Nano Server non è supportato.
>
> Nelle distribuzioni di Linux sono supportati solo i kernel di scorta che fanno parte di una versione/aggiornamento secondaria della distribuzione.
>
> Gli aggiornamenti tra versioni principali di una distribuzione di Linux in una macchina virtuale VMware o un server fisico protetto mediante Azure Site Recovery non sono supportati. Durante l'aggiornamento del sistema operativo tra versioni principali (ad esempio da CentOS 6.\* a CentOS 7.\*), disabilitare la replica per il computer, aggiornare il sistema operativo del computer e quindi abilitare nuovamente la replica.
>


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>Versioni del kernel Ubuntu supportate per server VMware/fisici

**Versione** | **Versione del servizio Mobility** | **Versione del kernel** |
--- | --- | --- |
14.04 LTS | 9.10 | Da 3.13.0-24 generica a 3.13.0-121 generica<br/>Da 3.16.0-25 generica a 3.16.0-77 generica<br/>Da 3.19.0-18 generica a 3.19.0-80 generica<br/>Da 4.2.0-18 generica a 4.2.0-42 generica<br/>Da 4.4.0-21 generica a 4.4.0-81 generica |
14.04 LTS | 9.11 | Da 3.13.0-24 generica a 3.13.0-128 generica<br/>Da 3.16.0-25 generica a 3.16.0-77 generica<br/>Da 3.19.0-18 generica a 3.19.0-80 generica<br/>Da 4.2.0-18 generica a 4.2.0-42 generica<br/>Da 4.4.0-21 generica a 4.4.0-91 generica |
14.04 LTS | 9.12 | Da 3.13.0-24 generica a 3.13.0-132 generica<br/>Da 3.16.0-25 generica a 3.16.0-77 generica<br/>Da 3.19.0-18 generica a 3.19.0-80 generica<br/>Da 4.2.0-18 generica a 4.2.0-42 generica<br/>Da 4.4.0-21 generica a 4.4.0-96 generica |
14.04 LTS | 9.13 | Da 3.13.0-24 generica a 3.13.0-137 generica<br/>Da 3.16.0-25 generica a 3.16.0-77 generica<br/>Da 3.19.0-18 generica a 3.19.0-80 generica<br/>Da 4.2.0-18 generica a 4.2.0-42 generica<br/>Da 4.4.0-21 generica a 4.4.0-104 generica |
16.04 LTS | 9.10 | Da 4.4.0-21 generica a 4.4.0-81 generica<br/>Da 4.8.0-34 generica a 4.8.0-56 generica<br/>Da 4.10.0-14 generica a 4.10.0-24 generica |
16.04 LTS | 9.11 | Da 4.4.0-21 generica a 4.4.0-91 generica<br/>Da 4.8.0-34 generica a 4.8.0-58 generica<br/>Da 4.10.0-14 generica a 4.10.0-32 generica |
16.04 LTS | 9.12 | Da 4.4.0-21 generica a 4.4.0-96 generica<br/>Da 4.8.0-34 generica a 4.8.0-58 generica<br/>Da 4.10.0-14 generica a 4.10.0-35 generica |
16.04 LTS | 9.13 | Da 4.4.0-21 generica a 4.4.0-104 generica<br/>Da 4.8.0-34 generica a 4.8.0-58 generica<br/>Da 4.10.0-14 generica a 4.10.0-42 generica |

## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>File system e configurazioni di archiviazione guest supportate in Linux (server VMware/fisici)

I file system e i software di configurazione dell'archiviazione seguenti sono supportati nei server Linux eseguiti in server fisici o VMware:
* File system: ext3, ext4, ReiserFS (solo Suse Linux Enterprise Server), XFS
* Gestore volumi: LVM2
* Software con percorsi multipli: mapper dispositivi

I dispositivi di archiviazione paravirtualizzati, ovvero dispositivi esportati da driver paravirtualizzati, non sono supportati.<br/>
I dispositivi di I/O a blocchi a code multiple non sono supportati.<br/>
I server fisici con il controller di archiviazione HP CCISS non sono supportati.<br/>

>[!Note]
> Sui server Linux le seguenti directory (se impostate come partizioni o file system separati) devono essere tutte nello stesso disco (il disco del sistema operativo) nel server di origine: / (root), /boot, /usr, /usr/local, /var e così via, mentre /boot deve essere in una partizione del disco e non in un volume LVM<br/><br/>
>


## <a name="support-for-network-configuration"></a>Supporto per la configurazione di rete
Le tabelle seguenti offrono un riepilogo delle configurazioni di rete supportate nei vari scenari di distribuzione che usano Azure Site Recovery per la replica in Azure.

### <a name="host-network-configuration"></a>Configurazione di rete per host

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Gruppo NIC | Sì<br/><br/>Non supportato quando i computer fisici vengono replicati| Sì
VLAN | Sì | Sì
IPv4 | Sì | Sì
IPv6 | No  | No 

### <a name="guest-vm-network-configuration"></a>Configurazione di rete per VM guest

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Gruppo NIC | No  | No 
IPv4 | Sì | Sì
IPv6 | No  | No 
IP statico (Windows) | Sì | Sì
IP statico (Linux) | Sì <br/><br/>Le macchine virtuali sono configurate per l'uso di DHCP in caso di failback  | No 
Più NIC | Sì | Sì

### <a name="failed-over-azure-vm-network-configuration"></a>Configurazione di rete per VM di Azure sottoposte a failover

**Rete di Azure** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Express Route | Sì | Sì
ILB | Sì | Sì
ELB | Sì | Sì
servizio Gestione traffico | Sì | Sì
Più NIC | Sì | Sì
IP riservato | Sì | Sì
IPv4 | Sì | Sì
Conservazione IP origine | Sì | Sì
Endpoint servizio di rete virtuale (i firewall di Archiviazione di Azure e le reti virtuali) | No  | No 


## <a name="support-for-storage"></a>Supporto per archiviazione
Le tabelle seguenti offrono un riepilogo delle configurazioni di archiviazione supportate nei vari scenari di distribuzione che usano Azure Site Recovery per la replica in Azure.

### <a name="host-storage-configuration"></a>Configurazione di archiviazione per host

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | --- | ---
NFS | Sì per VMware<br/><br/> No per server fisici | N/D
SMB 3.0 | N/D | Sì
SAN (iSCSI) | Sì | Sì
Percorsi multipli (MPIO)<br></br>Testata con: DSM Microsoft, EMC PowerPath 5.7 SP4, DSM EMC PowerPath per CLARiiON | Sì | Sì

### <a name="guest-or-physical-server-storage-configuration"></a>Configurazione di archiviazione per server fisici o guest

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
VMDK | Sì | N/D
VHD/VHDX | N/D | Sì
VM di seconda generazione | N/D | Sì
EFI/UEFI| Migrazione ad Azure per macchine virtuali VMware con Windows Server 2012 e versioni successive. </br></br> ** Vedere la nota alla fine della tabella.  | Sì
Disco cluster condiviso | No  | No 
Disco crittografato | No  | No 
NFS | No  | N/D
SMB 3.0 | No  | No 
RDM | Sì<br/><br/> N/D per server fisici | N/D
Disco superiore a 1 TB | Sì<br/><br/>Fino a 4095 GB | Sì<br/><br/>Fino a 4095 GB
Disco con dimensioni logiche di settore a 4 KB e dimensioni fisiche di settore a 4 KB | Sì | Non supportato per VM di generazione 1<br/><br/>Non supportato per VM di generazione 2
Disco con dimensioni logiche di settore a 4 KB e dimensioni fisiche di settore a 512 byte | Sì |  Sì
Volume con disco con striping superiore a 1 TB<br/><br/> Gestione volumi logici (LVM) | Sì | Sì
Spazi di archiviazione | No  | Sì
Aggiunta/rimozione a caldo disco | No  | No 
Esclusione disco | Sì | Sì
Percorsi multipli (MPIO) | N/D | Sì

> [!NOTE]
> ** È possibile eseguire la migrazione in Azure di macchine virtuali VMware con avvio UEFI che eseguono Windows Server 2012 o versioni successive. Si applicano le restrizioni seguenti.
> - Solo migrazione ad Azure. Il failback nel sito VMware locale non è supportato.
> - Non sono supportate più di 4 partizioni sul disco del sistema operativo del server.
> - Richiede il servizio Mobility di Azure Site Recovery versione 9.13 o successiva.
> - Non supportato per i server fisici.

**Archiviazione di Azure** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Archiviazione con ridondanza locale | Sì | Sì
Archiviazione con ridondanza geografica | Sì | Sì
RA-GRS | Sì | Sì
Archiviazione ad accesso sporadico | No  | No 
Archiviazione ad accesso frequente| No  | No 
BLOB in blocchi | No  | No 
Crittografia dei dati inattivi (SSE)| Sì | Sì
Archiviazione Premium | Sì | Sì
Servizio di importazione/esportazione | No  | No 
Endpoint servizio di rete virtuale rete, ovvero firewall e reti virtuali di Archiviazione di Azure, configurati in un account di archiviazione di destinazione o in un account di archiviazione della cache usato per l'archiviazione dei dati di replica | No  | No 
Account di archiviazione V2 generico (livelli di accesso frequente e sporadico) | No  | No 


## <a name="support-for-azure-compute-configuration"></a>Supporto per configurazione di calcolo di Azure

**Funzionalità di calcolo** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Set di disponibilità | Sì | Sì
HUB | Sì | Sì  
Dischi gestiti | Sì | Sì<br/><br/>Il failback in locale da macchina virtuale Azure con i dischi gestiti non è attualmente supportato.

## <a name="failed-over-azure-vm-requirements"></a>Requisiti per VM di Azure sottoposte a failover

È possibile distribuire Site Recovery per replicare macchine virtuali e server fisici in esecuzione su qualsiasi sistema operativo supportato da Azure, vale a dire la maggior parte delle versioni di Windows e Linux. In caso di replica in Azure, le macchine virtuali locali da replicare devono essere conformi ai requisiti di Azure riportati di seguito.

**Entità** | **Requisiti** | **Dettagli**
--- | --- | ---
**Sistema operativo guest** | Replica da Hyper-V ad Azure: Site Recovery supporta tutti i sistemi operativi [supportati da Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> Per la replica di server fisici e VMware, controllare i [prerequisiti](site-recovery-vmware-to-azure-classic.md) | Il controllo dei prerequisiti avrà esito negativo se non supportato.
**Architettura sistema operativo guest** | 64 bit | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Dimensioni disco del sistema operativo** | Fino a 2048 GB se si replicano **macchine virtuali VMware o server fisici in Azure**.<br/><br/>Fino a 2048 GB per le macchine virtuali **Hyper-V di prima generazione**.<br/><br/>Fino a 300 GB per le **macchine virtuali Hyper-V di seconda generazione**.  | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Numero di dischi del sistema operativo** | 1 | Il controllo dei prerequisiti avrà esito negativo se non supportato.
**Numero di dischi dati** | 64 o meno se si replicano **VM VMware in Azure**; 16 o meno se si replicano **VM Hyper-V in Azure** | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Dimensioni dei dischi rigidi virtuali dei dischi dati** | Fino a 4095 GB | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Schede di rete** | Sono supportate più schede |
**Disco rigido virtuale condiviso** | Non supportate | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Disco FC** | Non supportate | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Formato disco rigido** | VHD  <br/><br/> VHDX | Anche se VHDX al momento non è supportato in Azure, in Site Recovery VHDX viene convertito automaticamente in VHD quando si esegue il failover in Azure. Quando si esegue il failback in locale, le macchine virtuali continuano a utilizzare il formato VHDX.
**BitLocker** | Non supportate | Prima di proteggere una macchina virtuale è necessario disabilitare BitLocker.
**Nome VM** | Tra 1 e 63 caratteri. Limitato a lettere, numeri e trattini. Il nome della macchina virtuale deve iniziare e terminare con una lettera o un numero. | Aggiornare il valore nelle proprietà della macchina virtuale in Site Recovery.
**Tipo di VM** | Prima generazione<br/><br/> Seconda generazione - Windows | Sono supportate le macchine virtuali di seconda generazione con disco del sistema operativo di base che include uno o più volumi di dati in formato VHDX e inferiori a 300 GB di spazio su disco.<br></br>Le macchine virtuali Linux di seconda generazione non sono supportate. [Altre informazioni](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Supporto per azioni su insiemi di credenziali di Servizi di ripristino

**Azione** | **Server fisico/VMware** | **Hyper-V (senza Virtual Machine Manager)** | **Hyper-V (con Virtual Machine Manager)**
--- | --- | --- | ---
Spostamento insieme di credenziali tra gruppi di risorse<br/><br/> All'interno e tra sottoscrizioni | No  | No  | No 
Spostamento di risorse di archiviazione, rete e VM di Azure tra gruppi di risorse<br/><br/> All'interno e tra sottoscrizioni | No  | No  | No 


## <a name="support-for-provider-and-agent"></a>Supporto per provider e agente

**Nome** | **Descrizione** | **Versione più recente** | **Dettagli**
--- | --- | --- | --- | ---
**Provider di Azure Site Recovery** | Coordina le comunicazioni tra server locali e Azure <br/><br/> Installato nei server Virtual Machine Manager locali o nei server Hyper-V se non è presente un server Virtual Machine Manager | 5.1.2700.1 (disponibile dal portale) | [Funzionalità e correzioni più recenti](https://aka.ms/latest_asr_updates)
**Installazione unificata di Azure Site Recovery (da VMware ad Azure)** | Coordina le comunicazioni tra server VMware locali e Azure  <br/><br/> Installato su server VMware locali | 9.12.4653.1 (disponibile dal portale) | [Funzionalità e correzioni più recenti](https://aka.ms/latest_asr_updates)
**Servizio Mobility** | Coordina la replica fra server VMware locali/server fisici e sito Azure/secondario<br/><br/> Installato in server fisici o in macchine virtuali VMware da replicare  | 9.12.4653.1 (disponibile dal portale) | [Funzionalità e correzioni più recenti](https://aka.ms/latest_asr_updates)
**Agente di Servizi di ripristino di Microsoft Azure (MARS)** | Coordina la replica tra le macchine virtuali Hyper-V e Azure<br/><br/> Installato nei server Hyper-V locali (con o senza un server Virtual Machine Manager) | Agente più recente (disponibile dal portale) |






## <a name="next-steps"></a>Passaggi successivi
[Verifica dei prerequisiti](site-recovery-prereq.md)
