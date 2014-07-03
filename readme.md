## Google Tag Manager Best Practise Guide

There are 3 key areas to Google Tag Manager

#### A. Website Code

1. dataLayer - On Page Load
2. GTM Container Code
3. dataLayer.push() - On Events

#### B. Google Tag Manager Interface

1. Accounts
2. Users
3. Containers
4. Tags (Inc Auto-Event Tags)
5. Rules 
6. Macros
7. Preview & Debug
8. Versions
9. Publish
10. Roll-back

#### C. The Debugger (Web Only)

1. Debug Tags, Rules and Macros

## Breakdown

### A.1. dataLayer - On Page Load

The dataLayer is a javascript object that allows you to structure data in an organised and consistent manner across all pages. The dataLayer should be placed in the `<head>` of the page and contains data that is avaialble when the page loads.

eg.

```js
var dataLayer = {
    site : { enviroment : 'production',
             countryCode: 'UK'},
    page : { type : 'home',
             url: '/'}
}

```
### A.2. GTM Container Code

The Google Tag Mnaager container code is what connects your website to the GTM interface. Anything configured in GTM will be downloaded to the page via this blog of code.

The recommended placement for the container code is just after the opening `<body>`. This is due to the noscript code that is included in the code

**Important:** The GTM container code should always go after the dataLayer code (page load code from A.1.).

### A.3. dataLayer.push() - On Events

dataLayer.push() is used when an event occurs after the page has loaded and this event needs to be tracked. A simple example is when a user adds an item to the basket and is not taken straight to the checkout but instead an AJAX event occurs to update the basket with the new item. 

You should always include the key 'event' with an vaule describing the event.

eg.

```js
dataLayer.push({
    event : 'addToBasket',
    basketProducts : { id : 'NT1234',
                       name : 'Nike Trainers',
                       price : 49.99}
})

```




### B.1. Accounts
### B.2. Users
### B.3. Containers
### B.4. Tags (Inc Auto-Event Tags)

#### Naming Convention

Follow a strict name convention to easily understand the tag provider and what the tag does.

    Tag - [Name Of Tag or Tag Provider] - [Type Of Tag] - [Other Details]

eg.

    Tag - Universal Analytics - Page View

### B.5. Rules 

#### Naming Convention

Start all rules with lowercase.

Try to base the rule name as close to the actual rules you define

eg.

    event equals addToBasket
or

    dataLayer - page.type equals Confirmation

### B.6. Macros

#### Naming Convention

Start all rules with lowercase and the type of macro you are using.

eg.

    dataLayer - [exact key you will be refrencing]
    dataLayer - page.type

or 

    custom js - [name to describe code]
    custom js - capture user date of birth

or

    lookup table - [name to describe lookup logic/behaviour]
    lookup table - google analytics ID based on domain


### B.7. Preview & Debug
### B.8. Versions
### B.9. Publish
### B.10. Roll-back

### C.1. Debug Tags, Rules and Macros
