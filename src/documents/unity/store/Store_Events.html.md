---
layout: "content"
image: "Events"
title: "Events"
text: "Learn how to observe and handle economy events triggered by unity3d-store to customize your game-specific behavior."
position: 5
theme: 'platforms'
collection: 'unity_store'
module: 'store'
platform: 'unity'
---

#Event Handling

##About

SOOMLA allows you to subscribe to store events, be notified when they occur, and implement your own application-specific behavior to handle them once they occur. SOOMLA's unity3d-store's event handling mechanism is based on the event-handling methods of android-store and ios-store. Throughout android-store and ios-store events are fired and in unity3d-store they are observed and handled.

###Tips & Reminders

- As mentioned in [Getting Started](/unity/store/Store_GettingStarted), make sure you add the event prefabs (StoreEvents and CoreEvents) to your earliest loading scene.

- It is recommended that you register all events before initializing Store.

##How it works

Events are triggered when SOOMLA wants to notify you on different things that happened involving Store operations.

For example, When a user buys a currency pack, his currency balance is updated. As a result, a `CurrencyBalanceChangedEvent` is fired.

##Observing & Handling Events

The `StoreEvents` class is where all events go through. To handle various events, just add your game-specific behavior to the delegates in the `StoreEvents` class.

For example, if you want to listen for a `MarketPurchaseStarted` event:

``` cs
StoreEvents.OnMarketPurchaseStarted += onMarketPurchaseStarted;

public void onMarketPurchaseStarted(PurchasableVirtualItem pvi) {
    // your game specific implementation here
}
```

<div class="info-box">Your game-specific behavior is an addition to the default behavior implemented by SOOMLA. You don't replace SOOMLA's behavior.</div>

##Store Events

This is a list of all events in SOOMLA Store and the way to listen to them:

###OnSoomlaStoreInitialized

This event will be thrown when Soomla Store module is initialized and ready.

``` cs
StoreEvents.OnSoomlaStoreInitialized += onSoomlaStoreInitialized;

public void onSoomlaStoreInitialized() {
    // ... your game specific implementation here ...
}
```
**NOTE:** One thing you need to notice is that if you want to listen to OnSoomlaStoreInitialized event you have to set up the listener before you initialize SoomlaStore.
So you'll need to do:
````
StoreEvents.OnSoomlaStoreInitialized += onSoomlaStoreInitialized;
````
before
````
Soomla.SoomlaStore.Initialize(new Soomla.Example.MuffinRushAssets());
````

###OnCurrencyBalanceChanged

This event will be thrown when the balance of a specific currency has changed.

``` cs
StoreEvents.OnCurrencyBalanceChanged += onCurrencyBalanceChanged;

public void onCurrencyBalanceChanged(VirtualCurrency virtualCurrency, int balance, int amountAdded) {
    // virtualCurrency is the currency that its balance was changed
    // balance is the balance of the currency after the change
    // amountAdded is the amount that was added to the currency balance (in case the number of currencies was removed this will be a negative value)

    // ... your game specific implementation here ...
}
```

###OnGoodBalanceChanged

This event will be thrown when the balance of a specific virtual good has changed.

``` cs
StoreEvents.OnGoodBalanceChanged += onGoodBalanceChanged;

public void onGoodBalanceChanged(VirtualGood good, int balance, int amountAdded) {
    // virtualCurrency is the virtual good that its balance was changed
    // balance is the balance of the currency after the change
    // amountAdded is the amount that was added to the currency balance (in case the number of currencies was removed this will be a negative value)

    // ... your game specific implementation here ...
}
```

###OnMarketPurchaseStarted

This event will be thrown when market purchase operation has started.

``` cs
StoreEvents.OnMarketPurchaseStarted += onMarketPurchaseStarted;

public void onMarketPurchaseStarted(PurchasableVirtualItem pvi) {
    // pvi is the PurchasableVirtualItem that its purchase operation has just started

    // ... your game specific implementation here ...
}
```

###OnMarketPurchase

This event will be thrown when a market purchase operation has completed successfully.

``` cs
StoreEvents.OnMarketPurchase += onMarketPurchase;

public void onMarketPurchase(PurchasableVirtualItem pvi, string payload, Dictionary<string, string> extra) {
    // pvi is the PurchasableVirtualItem that was just purchased
    // payload is a text that you can give when you initiate the purchase operation and you want to receive back upon completion
    // extra will contain platform specific information about the market purchase.
    //      Android: The "extra" dictionary will contain "orderId" and "purchaseToken".
    //      iOS: The "extra" dictionary will contain "receipt" and "token".

    // ... your game specific implementation here ...
}
```

###OnMarketPurchaseCancelled

This event will be thrown when a market purchase operation has cancelled by the user.

``` cs
StoreEvents.OnMarketPurchaseCancelled += onMarketPurchaseCancelled;

public void onMarketPurchaseCancelled(PurchasableVirtualItem pvi) {
    // pvi is the PurchasableVirtualItem whose purchase operation has just cancelled

    // ... your game specific implementation here ...
}
```

###OnMarketRefund

This event will be thrown when a market refund operation has completed successfully.

``` cs
StoreEvents.OnMarketRefund += onMarketRefund;

public void onMarketRefund(PurchasableVirtualItem pvi) {
    // pvi is the PurchasableVirtualItem to refund

    // ... your game specific implementation here ...
}
```

###OnMarketItemsRefreshStarted

This event will be thrown when a refresh market items operation has started.

``` cs
StoreEvents.OnMarketItemsRefreshStarted += onMarketItemsRefreshStarted;

public void onMarketItemsRefreshStarted() {

    // ... your game specific implementation here ...
}
```

###OnMarketItemsRefreshFinished

This event will be thrown when a refresh market items operation has finished.

``` cs
StoreEvents.OnMarketItemsRefreshFinished += onMarketItemsRefreshFinished;

public void onMarketItemsRefreshFinished(List<MarketItem> items) {
    // items is the list of Market items that was fetched from the Market

    // ... your game specific implementation here ...
}
```

###OnRestoreTransactionsStarted

This event will be thrown when restore transactions operation has started.

``` cs
StoreEvents.OnRestoreTransactionsStarted += onRestoreTransactionsStarted;

public void onRestoreTransactionsStarted() {

    // ... your game specific implementation here ...
}
```

###OnRestoreTransactionsFinished

This event will be thrown when restore transactions operation has completed successfully.

``` cs
StoreEvents.OnRestoreTransactionsFinished += onRestoreTransactionsFinished;

public void onRestoreTransactionsFinished(bool success) {
    // success is a boolean value that says if the restore transactions operation hass succeeded or failed

    // ... your game specific implementation here ...
}
```

###OnItemPurchaseStarted

This event will be thrown when item purchase operation has started.

``` cs
StoreEvents.OnItemPurchaseStarted += onItemPurchaseStarted;

public void onItemPurchaseStarted(PurchasableVirtualItem pvi) {
    // pvi is the PurchasableVirtualItem that its purchase operation has just started

    // ... your game specific implementation here ...
}
```

###OnItemPurchased

This event will be thrown when item purchase operation has completed successfully.

``` cs
StoreEvents.OnItemPurchased += onItemPurchased;

public void onItemPurchased(PurchasableVirtualItem pvi, string payload) {
    // pvi is the PurchasableVirtualItem that was just purchased
    // payload is a text that you can give when you initiate the purchase operation and you want to receive back upon completion

    // ... your game specific implementation here ...
}
```

###OnGoodEquipped

This event will be thrown when virtual good equipping operation has completed successfully.

``` cs
StoreEvents.OnGoodEquipped += onGoodEquipped;

public void onGoodEquipped(EquippableVG good) {
    // good is the virtual good that was just equipped

    // ... your game specific implementation here ...
}
```

###OnGoodUnEquipped

This event will be thrown when virtual good un-equipping operation has completed successfully.

``` cs
StoreEvents.OnGoodUnEquipped += onGoodUnequipped;

public void onGoodUnequipped(EquippableVG good) {
    // good is the virtual good that was just unequipped

    // ... your game specific implementation here ...
}
```

###OnGoodUpgrade

This event will be thrown when virtual good upgrading operation has completed successfully.

``` cs
StoreEvents.OnGoodUpgrade += onGoodUpgrade;

public void onGoodUpgrade(VirtualGood good, UpgradeVG currentUpgrade) {
    // good is the virtual good that was just upgraded
    // currentUpgrade is the upgrade after the operation copmleted

    // ... your game specific implementation here ...
}
```

###OnBillingSupported

This event will be thrown when the billing service is initialized and ready.

``` cs
StoreEvents.OnBillingSupported += onBillingSupported;

public void onBillingSupported() {

    // ... your game specific implementation here ...
}
```

###OnBillingNotSupported

This event will be thrown when the billing service fails to initialize.

``` cs
StoreEvents.OnBillingNotSupported += onBillingNotSupported;

public void onBillingNotSupported() {

    // ... your game specific implementation here ...
}
```

###OnUnexpectedErrorInStore

This event will be thrown when the billing service fails to initialize.

``` cs
StoreEvents.OnUnexpectedErrorInStore += onUnexpectedErrorInStore;

public void onUnexpectedErrorInStore(string message) {
    // message is the description of the error

    // ... your game specific implementation here ...
}
```

## Android Specific Events

###OnIabServiceStarted

This event will be thrown when the in-app billing service is started.

``` cs
StoreEvents.OnIabServiceStarted += onIabServiceStarted;

public void onIabServiceStarted() {

    // ... your game specific implementation here ...
}
```

###OnIabServiceStopped

This event will be thrown when the in-app billing service is stopped.

``` cs
StoreEvents.OnIabServiceStopped += onIabServiceStopped;

public void onIabServiceStopped() {

    // ... your game specific implementation here ...
}
```