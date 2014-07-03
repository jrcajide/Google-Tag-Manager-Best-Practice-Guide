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

## Visual Overview

![Before](https://d3j5vwomefv46c.cloudfront.net/photos/large/859071575.png)

![After](https://d3j5vwomefv46c.cloudfront.net/photos/large/859071727.png)

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

The code block looks as follows

```html
<!-- Google Tag Manager -->
<noscript><iframe src="//www.googletagmanager.com/ns.html?id=GTM-XXYYZZ"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'//www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXYYZZ');</script>
<!-- End Google Tag Manager -->

```

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

Create one account for your organisation. The account is the top level for GTM and allows you to have multiple containers.

### B.2. Users

Users can be assigned to an account or container level. 

The following permissions can be applied to users.

#### Account Permissions

1. View Account Users
2. Manage Account Users

#### Container Permissions

1. No Access
2. View Only
3. View and Edit
4. View, Edit, Delete and Publish

### B.3. Containers

Containers can be created as either a 1) Website conatiner or 2) App container

Depending on how complex your websites are you can either create one container to go across all your domains or create a uniqie container for each domain.

#### 1) Use One Container for Multiple Domains

Every website is built in teh exact same structure and is managed by one team

#### 2) Use Multiple Containers for Multiple Domains

Websites are not built in the exact same format and each domain is managed by a seperate team

For apps use a seperate contaner for each app and per device. 

### B.4. Tags (Inc Auto-Event Tags)

Tags can be set-up using tag templates where possible.

Where templates are not avaiable a custom html or custom image tag can be added.

Macros can be used in custom html tags using the syntax `{{macro name}}`

#### Naming Convention

Follow a strict name convention to easily understand the tag provider and what the tag does.

    Tag - [Name Of Tag or Tag Provider] - [Type Of Tag] - [Other Details]

eg.

    Tag - Universal Analytics - Page View

### B.5. Rules 

Rules are used to define when tags should be triggered. They use macros to define the data that the rules are based on.

#### Naming Convention

Start all rules with lowercase.

Try to base the rule name as close to the actual rules you define

eg.

    event equals addToBasket
or

    dataLayer - page.type equals Confirmation

### B.6. Macros

Macros are used to extract and/or manipulate data on the page for websites or screen for apps. 

There are a range or macros avaialble for the web and a different range avaiable for apps.

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

When any tags are added you should use the debug mode to test everything is working correctly before publishing. The preview and debug mode works by setting a cookie on your computer which means you can test the changes localy on your computer before pushing anything to the live website

### B.8. Versions

When you are reay to ublish your changes create a new version of the container

### B.9. Publish

Publish the version of the container to live. Include any comments

### B.10. Roll-back

If any issues arise from the latest published container you can revert to a previous version

### C.1. Debug Tags, Rules and Macros

Using the debugger you can check what tags are being executed on the page.
