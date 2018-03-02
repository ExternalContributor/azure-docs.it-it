---
title: "Domande frequenti e problemi noti di Identità del servizio gestito (MSI) per Azure Active Directory"
description: "Problemi noti di Identità del servizio gestito per Azure Active Directory."
services: active-directory
documentationcenter: 
author: daveba
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: identity
ms.date: 12/15/2017
ms.author: daveba
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: b0b5b991b7d2baaa40ebedbd19247717e91aa027
ms.sourcegitcommit: 12fa5f8018d4f34077d5bab323ce7c919e51ce47
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2018
---
# <a name="faq-and-known-issues-with-managed-service-identity-msi-for-azure-active-directory"></a>Domande frequenti e problemi noti di Identità del servizio gestito (MSI) per Azure Active Directory

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="does-msi-work-with-azure-cloud-services"></a>Identità del servizio gestito funziona con Servizi cloud di Azure?

No. Non è previsto il supporto di Identità del servizio gestito in Servizi cloud di Azure.

### <a name="does-msi-work-with-the-active-directory-authentication-library-adal-or-the-microsoft-authentication-library-msal"></a>L'Identità del servizio gestito funziona con Active Directory Authentication Library (ADAL) o con Microsoft Authentication Library (MSAL)?

No, l'Identità del servizio gestito non è ancora integrata con ADAL o MSAL. Per informazioni su come acquisire il token dell'identità del servizio gestito usando l'endpoint REST dell'identità del servizio gestito, vedere [Come usare un'identità del servizio gestito di una macchina virtuale di Azure per l'acquisizione di token](msi-how-to-use-vm-msi-token.md).

### <a name="what-are-the-supported-linux-distributions"></a>Quali sono le distribuzioni di Linux supportate?

Le distribuzioni di Linux seguenti supportano MSI: 

- CoreOS Stable
- CentOS 7.1
- RedHat 7.2
- Ubuntu 15.04

Le altre distribuzioni di Linux attualmente non sono supportate e l'estensione potrebbe non riuscire nelle distribuzioni non supportate.

L'estensione funziona in CentOS 6.9. Tuttavia, a causa della mancanza del supporto di sistema nella versione 6.9, l'estensione non si riavvia automaticamente in caso di arresto anomalo o di arresto. Viene riavviata al riavvio della VM. Per riavviare manualmente l'estensione, vedere [Come si riavvia l'estensione MSI?](#how-do-you-restart-the-msi-extension)

### <a name="how-do-you-restart-the-msi-extension"></a>Come si riavvia l'estensione MSI?
In Windows e alcune versioni di Linux, se si arresta l'estensione, è possibile usare il cmdlet seguente per riavviarla manualmente:

```powershell
Set-AzureRmVMExtension -Name <extension name>  -Type <extension Type>  -Location <location> -Publisher Microsoft.ManagedIdentity -VMName <vm name> -ResourceGroupName <resource group name> -ForceRerun <Any string different from any last value used>
```

Dove: 
- Il nome e il tipo di estensione per Windows è: ManagedIdentityExtensionForWindows
- Il nome e il tipo di estensione per Linux è: ManagedIdentityExtensionForLinux

### <a name="are-there-rbac-roles-for-user-assigned-identities"></a>Sono disponibili ruoli di controllo degli accessi in base al ruolo per le identità assegnate all'utente?
Sì:
1. Collaboratore MSI: 

- Può: eseguire operazioni CRUD sulle identità assegnate all'utente. 
- Non può: assegnare a una risorsa un'identità assegnata all'utente. (Ad esempio, assegnare l'identità a una macchina virtuale)

2. Operatore MSI: 

- Può: assegnare a una risorsa un'identità assegnata all'utente. (Ad esempio, assegnare l'identità a una macchina virtuale)
- Non può: eseguire operazioni CRUD sulle identità assegnate all'utente.

Nota: il ruolo di collaboratore predefinito può eseguire tutte le azioni descritte in precedenza: 
- Eseguire operazioni CRUD sulle identità assegnate all'utente
- Assegnare a una risorsa un'identità assegnata all'utente. (Ad esempio, assegnare l'identità a una macchina virtuale)


## <a name="known-issues"></a>Problemi noti

### <a name="automation-script-fails-when-attempting-schema-export-for-msi-extension"></a>Si verifica un errore di "Script di automazione" durante il tentativo di esportazione dello schema per l'estensione dell'identità del servizio gestito

Se l'identità del servizio gestito è abilitata in una macchina virtuale, viene visualizzato l'errore seguente quando si tenta di usare la funzionalità "Script di automazione" per la macchina virtuale o il relativo gruppo di risorse:

![Errore di esportazione dello script di automazione per l'identità del servizio gestito](~/articles/active-directory/media/msi-known-issues/automation-script-export-error.png)

L'estensione della macchina virtuale dell'identità del servizio gestito non supporta attualmente la possibilità di esportare lo schema in un modello di gruppo di risorse. Di conseguenza, il modello generato non include i parametri di configurazione per abilitare l'identità del servizio gestito per la risorsa. È possibile aggiungere manualmente queste sezioni seguendo gli esempi in [Configurare un'Identità del servizio gestito della macchina virtuale tramite un modello](msi-qs-configure-template-windows-vm.md).

Quando è disponibile per l'estensione della macchina virtuale dell'identità del servizio gestito, la funzionalità di esportazione dello schema sarà elencata in [Esportazione di gruppi di risorse contenenti estensioni macchina virtuale](~/articles/virtual-machines/windows/extensions-export-templates.md#supported-virtual-machine-extensions).

### <a name="configuration-blade-does-not-appear-in-the-azure-portal"></a>Il pannello di configurazione non viene visualizzato nel portale di Azure

Se il pannello di configurazione della macchina virtuale non viene visualizzato nella macchina virtuale vuol dire che l'Identità del servizio gestito non è stata ancora abilitata nel portale della propria area geografica.  Ricontrollare in seguito.  È anche possibile abilitare l'Identità del servizio gestito per la macchina virtuale tramite [PowerShell](msi-qs-configure-powershell-windows-vm.md) o l'[interfaccia della riga di comando di Azure](msi-qs-configure-cli-windows-vm.md).

### <a name="cannot-assign-access-to-virtual-machines-in-the-access-control-iam-blade"></a>Impossibile assegnare l'accesso alle macchine virtuali nel pannello Controllo di accesso (IAM)

Se la **macchina virtuale** non viene visualizzata nel portale di Azure come opzione per **Assegna accesso a** in **Controllo di accesso (IAM)** > **Aggiungi autorizzazioni**, vuol dire che l'Identità del servizio gestito non è stata ancora abilitata nel portale della propria area geografica. Ricontrollare in seguito.  È comunque possibile selezionare l'Identità del servizio gestito per l'assegnazione di ruolo eseguendo una ricerca dell'entità servizio dell'Identità del servizio gestito.  Immettere il nome della macchina virtuale nel campo **Seleziona** per visualizzare l'entità servizio nei risultati della ricerca.

### <a name="vm-fails-to-start-after-being-moved-from-resource-group-or-subscription"></a>La macchina virtuale non viene avviata dopo essere stata spostata dal gruppo di risorse o dalla sottoscrizione

Se si sposta una macchina virtuale in esecuzione, questa continuerà a eseguire durante lo spostamento. Tuttavia, dopo lo spostamento, se la macchina virtuale viene arrestata e riavviata, non si avvierà. Questo problema si verifica perché la macchina virtuale non aggiorna il riferimento all'Identità del servizio gestito e continua a puntare a questa nel gruppo di risorse precedente.

**Soluzione alternativa** 
 
Attivare un aggiornamento nella macchina virtuale così da poter ottenere i valori corretti per l'Identità del servizio gestito. È possibile apportare una modifica alla proprietà della macchina virtuale per aggiornare il riferimento all'identità del servizio gestito. Ad esempio, è possibile impostare un nuovo valore di tag nella macchina virtuale con il comando seguente:

```azurecli-interactive
 az  vm update -n <VM Name> -g <Resource Group> --set tags.fixVM=1
```
 
Questo comando imposta un nuovo tag "fixVM" con valore 1 nella macchina virtuale. 
 
Impostando questa proprietà, la macchina virtuale si aggiorna inserendo l'URI della risorsa dell'Identità del servizio gestito corretto. La macchina virtuale dovrebbe a questo punto avviarsi. 
 
Dopo aver avviato la macchina virtuale, il tag può essere rimosso tramite il seguente comando:

```azurecli-interactive
az vm update -n <VM Name> -g <Resource Group> --remove tags.fixVM
```

## <a name="known-issues-with-user-assigned-msi-private-preview-feature"></a>Problemi noti con l'identità del servizio gestito assegnata dall'utente *(Funzionalità di anteprima privata)*

- L'unico modo per rimuovere tutte le identità del servizio gestito assegnate dall'utente è abilitare l'identità del servizio gestito assegnata dal sistema. 
- Il provisioning dell'estensione VM in una VM potrebbe non riuscire a causa degli errori di ricerca DNS. Riavviare la macchina virtuale e riprovare. 
- L'aggiunta di un'identità del servizio gestito non esistente potrebbe causare errori nella VM. *Nota: la correzione per impedire il completamento di Assign-Identity se l'identità del servizio gestito non esiste, verrà distribuita a breve*
- Attualmente l'esercitazione per Archiviazione di Azure è disponibile solo negli Stati Uniti centrali EUAP. 
- Non è supportata la creazione di un'identità del servizio gestito assegnata dall'utente con caratteri speciali (ad esempio, il carattere di sottolineatura).
- Quando si aggiunge un'altra identità assegnata dall'utente, clientID potrebbe non riuscire a richiederne i token. Come piano di mitigazione, riavviare l'estensione della macchina virtuale per l'identità del servizio gestito con i due comandi bash seguenti:
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler disable"`
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler enable"`
- VMAgent su Windows attualmente non supporta l'identità del servizio gestito assegnata dall'utente. 
- Quando una macchina virtuale ha un'identità del servizio gestito assegnata dall'utente ma non un'identità del servizio gestito assegnata dal sistema, l'interfaccia utente del portale visualizzerà l'identità del servizio gestito come abilitata. Per abilitare l'identità del servizio gestito assegnata dal sistema, usare un modello di Azure Resource Manager, un'interfaccia della riga di comando di Azure o un SDK.
