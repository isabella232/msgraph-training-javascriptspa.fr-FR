---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822859"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="3fb15-101">Dans cet exercice, vous allez incorporer Microsoft Graph dans l’application.</span><span class="sxs-lookup"><span data-stu-id="3fb15-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="3fb15-102">Pour cette application, vous allez utiliser la bibliothèque de [bibliothèque cliente JavaScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) pour effectuer des appels à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="3fb15-102">For this application, you will use the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript) library to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="3fb15-103">Récupérer les événements de calendrier à partir d’Outlook</span><span class="sxs-lookup"><span data-stu-id="3fb15-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="3fb15-104">Dans cette section, vous allez utiliser la bibliothèque cliente Microsoft Graph pour obtenir des événements de calendrier pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3fb15-104">In this section, you'll use the Microsoft Graph client library to get calendar events for the user.</span></span>

1. <span data-ttu-id="3fb15-105">Créez un fichier à la racine du projet nommé **timezones.js** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="3fb15-105">Create a new file in the root of the project named **timezones.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    <span data-ttu-id="3fb15-106">Ce code mappe les identificateurs de fuseau horaire Windows aux identificateurs de fuseau horaire d’IANA pour des incompatibilités avec moment.js.</span><span class="sxs-lookup"><span data-stu-id="3fb15-106">This code maps Windows time zone identifiers to IANA time zone identifiers for compatibility with moment.js.</span></span>

1. <span data-ttu-id="3fb15-107">Ajoutez la fonction suivante à **graph.js**.</span><span class="sxs-lookup"><span data-stu-id="3fb15-107">Add the following function to **graph.js**.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    <span data-ttu-id="3fb15-108">Que fait ce code ?</span><span class="sxs-lookup"><span data-stu-id="3fb15-108">Consider what this code is doing.</span></span>

    - <span data-ttu-id="3fb15-109">L’URL qui sera appelée est `/me/calendarview`.</span><span class="sxs-lookup"><span data-stu-id="3fb15-109">The URL that will be called is `/me/calendarview`.</span></span>
    - <span data-ttu-id="3fb15-110">La `header` méthode ajoute un `Prefer` en-tête spécifiant le fuseau horaire préféré de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3fb15-110">The `header` method adds a `Prefer` header specifying the user's preferred time zone.</span></span>
    - <span data-ttu-id="3fb15-111">La `query` méthode ajoute les heures de début et de fin pour l’affichage Calendrier.</span><span class="sxs-lookup"><span data-stu-id="3fb15-111">The `query` method adds the start and end times for the calendar view.</span></span>
    - <span data-ttu-id="3fb15-112">La `select` méthode limite les champs renvoyés pour chaque événement à ceux que l’affichage utilise réellement.</span><span class="sxs-lookup"><span data-stu-id="3fb15-112">The `select` method limits the fields returned for each events to just those the view will actually use.</span></span>
    - <span data-ttu-id="3fb15-113">La `orderby` méthode trie les résultats en fonction de l’heure de début, avec l’événement le plus tôt en premier.</span><span class="sxs-lookup"><span data-stu-id="3fb15-113">The `orderby` method sorts the results by the start time, with the earliest event being first.</span></span>
    - <span data-ttu-id="3fb15-114">La `top` méthode demande jusqu’à 50 événements dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="3fb15-114">The `top` method requests up to 50 events in the response.</span></span>

1. <span data-ttu-id="3fb15-115">Ouvrez **ui.js** et ajoutez la fonction suivante.</span><span class="sxs-lookup"><span data-stu-id="3fb15-115">Open **ui.js** and add the following function.</span></span>

    ```javascript
    function showCalendar(events) {
      // TEMPORARY
      // Render the results as JSON
      var alert = createElement('div', 'alert alert-success');

      var pre = createElement('pre', 'alert-pre border bg-light p-2');
      alert.appendChild(pre);

      var code = createElement('code', 'text-break',
        JSON.stringify(events, null, 2));
      pre.appendChild(code);

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }
    ```

1. <span data-ttu-id="3fb15-116">Mettez à jour l' `switch` instruction de la `updatePage` fonction à appeler `showCalendar` lorsque la vue est `Views.calendar` .</span><span class="sxs-lookup"><span data-stu-id="3fb15-116">Update the `switch` statement in the `updatePage` function to call `showCalendar` when the view is `Views.calendar`.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. <span data-ttu-id="3fb15-117">Enregistrez vos modifications et actualisez l’application.</span><span class="sxs-lookup"><span data-stu-id="3fb15-117">Save your changes and refresh the app.</span></span> <span data-ttu-id="3fb15-118">Connectez-vous, puis cliquez sur le lien **calendrier** dans la barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="3fb15-118">Sign in and click the **Calendar** link in the nav bar.</span></span> <span data-ttu-id="3fb15-119">Si tout fonctionne, vous devriez voir une image mémoire JSON des événements dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3fb15-119">If everything works, you should see a JSON dump of events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="3fb15-120">Afficher les résultats</span><span class="sxs-lookup"><span data-stu-id="3fb15-120">Display the results</span></span>

<span data-ttu-id="3fb15-121">Dans cette section, vous allez mettre à jour la `showCalendar` fonction pour afficher les événements de manière plus conviviale.</span><span class="sxs-lookup"><span data-stu-id="3fb15-121">In this section you will update the `showCalendar` function to display the events in a more user-friendly manner.</span></span>

1. <span data-ttu-id="3fb15-122">Remplacez la fonction `showCalendar` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="3fb15-122">Replace the existing `showCalendar` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    <span data-ttu-id="3fb15-123">Cette méthode effectue une boucle dans la collection d’événements et ajoute une ligne de tableau pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="3fb15-123">This loops through the collection of events and adds a table row for each one.</span></span>

1. <span data-ttu-id="3fb15-124">Enregistrer les modifications et actualiser l’application.</span><span class="sxs-lookup"><span data-stu-id="3fb15-124">Save the changes and refresh the app.</span></span> <span data-ttu-id="3fb15-125">Cliquez sur le lien **calendrier** et l’application doit maintenant afficher un tableau d’événements pour la semaine en cours.</span><span class="sxs-lookup"><span data-stu-id="3fb15-125">Click on the **Calendar** link and the app should now render a table of events for the current week.</span></span>

    ![Capture d’écran du tableau des événements](./images/calendar-list.png)
