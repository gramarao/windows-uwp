---
Description: You can use the SendRequestAsync method to send requests to the Microsoft Store for operations that do not yet have an API available in the Windows SDK.
title: Send requests to the Microsoft Store
ms.assetid: 070B9CA4-6D70-4116-9B18-FBF246716EF0
ms.date: 03/22/2018
ms.topic: article
keywords: windows 10, uwp, StoreRequestHelper, SendRequestAsync
ms.localizationpriority: medium
---
# Send requests to the Microsoft Store

Starting in Windows 10, version 1607, the Windows SDK provides APIs for Store-related operations (such as in-app purchases) in the [Windows.Services.Store](/uwp/api/windows.services.store) namespace. However, although the services that support the Store are constantly being updated, expanded, and improved between OS releases, new APIs are typically added to the Windows SDK only during major OS releases.

We provide the [SendRequestAsync](/uwp/api/windows.services.store.storerequesthelper.sendrequestasync) method as a flexible way to make new Store operations available to Universal Windows Platform (UWP) apps before a new version of the Windows SDK is released. You can use this method to send requests to the Store for new operations that do not yet have a corresponding API available in the latest release of the Windows SDK.

> [!NOTE]
> The **SendRequestAsync** method is available only to apps that target Windows 10, version 1607, or later. Some of the requests supported by this method are only supported in releases after Windows 10, version 1607.

**SendRequestAsync** is a static method of the [StoreRequestHelper](/uwp/api/windows.services.store.storerequesthelper) class. To call this method, you must pass the following information to the method:
* A [StoreContext](/uwp/api/windows.services.store.storecontext) object that provides information about the user for which you want to perform the operation. For more information about this object, see [Get started with the StoreContext class](in-app-purchases-and-trials.md#get-started-with-the-storecontext-class).
* An integer that identifies the request that you want to send to the Store.
* If the request supports any arguments, you can also pass a JSON-formatted string that contains the arguments to pass along with the request.

The following example demonstrates how to call this method. This example requires using statements for the **Windows.Services.Store** and **System.Threading.Tasks** namespaces.

```csharp
public async Task<bool> AddUserToFlightGroup()
{
    StoreSendRequestResult result = await StoreRequestHelper.SendRequestAsync(
        StoreContext.GetDefault(), 8,
        "{ \"type\": \"AddToFlightGroup\", \"parameters\": { \"flightGroupId\": \"your group ID\" } }");

    if (result.ExtendedError == null)
    {
        return true;
    }

    return false;
}
```

See the following sections for information about the requests that are currently available via the **SendRequestAsync** method. We will update this article when support for new requests are added.

## Request for in-app ratings and reviews

You can programmatically launch a dialog from your app that asks your customer to rate your app and submit a review by passing the request integer 16 to the **SendRequestAsync** method. For more information, see [Show a rating and review dialog in your app](request-ratings-and-reviews.md#show-a-rating-and-review-dialog-in-your-app).

## Related topics

* [Show a rating and review dialog in your app](request-ratings-and-reviews.md#show-a-rating-and-review-dialog-in-your-app)
* [SendRequestAsync](/uwp/api/windows.services.store.storerequesthelper.sendrequestasync)
