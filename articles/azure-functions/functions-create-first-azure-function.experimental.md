---
title: Creare la prima funzione nel portale di Azure | Microsoft Docs
description: Informazioni su come creare la prima funzione di Azure per l'esecuzione senza server tramite il portale di Azure.
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/05/2018
ms.author: glenga
ms.custom: mvc, devcenter
experiment: 
<<<<<<< HEAD
ms.openlocfilehash: 9c038b1330bdd9ee0c922b98158c45f3c7b797ae
ms.sourcegitcommit: 059dae3d8a0e716adc95ad2296843a45745a415d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
=======
ms.openlocfilehash: e6ca80d90460f89c014ef1e425bc888cafaf93df
ms.sourcegitcommit: d87b039e13a5f8df1ee9d82a727e6bc04715c341
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/21/2018
>>>>>>> e9608243da864c46ce93986fe11980d2656272ea
---
# <a name="create-your-first-function-in-the-azure-portal"></a>Creare la prima funzione nel portale di Azure

Funzioni di Azure consente di eseguire il codice in un ambiente [senza server](https://azure.microsoft.com/overview/serverless-computing/), senza dover prima creare una macchina virtuale o pubblicare un'applicazione Web. Questo argomento fornisce informazioni su come usare Funzioni per creare una funzione di benvenuto nel portale di Azure.

![Creare un'app per le funzioni nel portale di Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a>Accedere ad Azure

Accedere al portale di Azure all'indirizzo<http://portal.azure.com> con il proprio account Azure.

## <a name="create-a-function-app"></a>Creare un'app per le funzioni

Per ospitare l'esecuzione delle funzioni è necessaria un'app per le funzioni. Un'app per le funzioni consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal-experiment.md)]

Si creerà ora una funzione nella nuova app per le funzioni.

## <a name="create-function"></a>Creare una funzione attivata tramite HTTP

1. Espandere la nuova app per le funzioni e quindi fare clic sul pulsante **+** accanto a **Funzioni**.

2.  Nella pagina **Iniziare rapidamente con una funzione preconfezionata** selezionare **Webhook e API**, **scegliere un linguaggio** per la funzione e fare clic su **Creare questa funzione**. 
   
    ![Guida di avvio rapido di Funzioni nel portale di Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Viene creata una funzione nel linguaggio prescelto usando il modello per una funzione attivata tramite HTTP. Questo argomento illustra una funzione script C# nel portale, ma è possibile creare una funzione in qualsiasi [linguaggio supportato](supported-languages.md). 

Ora è possibile eseguire la nuova funzione inviando una richiesta HTTP.

## <a name="test-the-function"></a>Testare la funzione

1. Nella nuova funzione fare clic su **</> Recupera URL della funzione** nell'angolo in alto a destra, selezionare **default (Function key)** (predefinita - tasto funzione) e quindi fare clic su **Copia**. 

    ![Creare l'URL della funzione dal portale di Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Incollare l'URL della funzione nella barra degli indirizzi del browser. Aggiungere il valore della stringa di query `&name=<yourname>` alla fine dell'URL e premere il tasto `Enter` per eseguire la richiesta. Nel browser dovrebbe venire visualizzata la risposta restituita dalla funzione.  

    L'esempio seguente mostra la risposta nel browser Edge (altri browser potrebbero includere il codice XML):

    ![Risposta della funzione nel browser.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    L'URL della richiesta include una chiave necessaria per impostazione predefinita per accedere a una funzione tramite HTTP.   

3. Quando viene eseguita la funzione, vengono scritte nei log informazioni di traccia. Per visualizzare l'output di traccia dell'esecuzione precedente, tornare alla funzione nel portale e fare clic sulla freccia nella parte inferiore della schermata per espandere **Log**. 

   ![Visualizzatore log di Funzioni nel portale di Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Clean-up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata un'app per le funzioni con una semplice funzione attivata tramite HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni rivedere [Binding HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).



