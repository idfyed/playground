---
title: 'Diglias Playground'
---

## Abstract

Diglias Playground is a set of instructions, documentation and tools that can be used by a Diglias customer during evaluation of the Diglias services. It is not a complete integration instruction. Using the playground it is possible to develop a web application that uses Diglias for authentication and identification of users.

## Intended Audience

The Diglias Playground is intended primarily for technically minded persons that needs to understand the technical structure of the Diglias service and how to integrate it in the customer environment.

## API Documentation

A good starting point is to get familiar with the different integration points are trough the EAPI through the API documentation. A number of concepts and terms referred to in the remainder of this document is explained in the documentation:

* [EAPI - Authentication](https://test.diglias.com/doc-rp/eapi.jsp)

## Evaluation Android App

To login to a web application integrated with the playground, the Android version of the Diglias app is used. (The production version is available for Android and iOS devices)
For the Diglias Playground a specific version of the Diglias app is used, to be able to install the app on a device the following steps needs to be taken.

### Request Google+ Membership

The Google+ group “Diglias Playground” can be found here: <https://plus.google.com/communities/114257454961570698089>
It is a private Google Plus group and membership will have to be requested and granted by Diglias.
Please note that the Google Account used to request membership should be the same account that later on will be used in the Google Play Store app, when installing the app on a device.

### Enroll In the Test Program

Once granted access to the Google Plus group, enrollment in to the test app program is achived by clicking the following link and followingin the instructions: <https://play.google.com/apps/testing/com.diglias.loginapp.prodtest﻿>

### Install the App

When enrollment in the test program has been completed, the app can be installed on any device using the same Google Account used when enrolling.
To install the app you can either follow this link with the browser of your device <https://play.google.com/store/apps/details?id=com.diglias.loginapp.prodtest> or
Open the Play Store App on the device and search for “Diglias Prod Test”.

## Playground Relying Party

To allow evaluation and practical test of the API and the service a test relying party has been set up in a non production environment, hence there is no guaranteed availability of the relying party and it should under no circumstances be used in a production situation.

### Relying Party Configuration

The playground relying party uses Diglias for authentication and will require the user to submit an e-mail address, a mobile phone number and a verified swedish personal identification number.

| | Parameter | Value |
|-|-----------|-------|
|Customer Id|auth_companyname|playground|
|Company MAC Key|N/A|LW4eUhQkJfwJGgQU8JCT/g==|

### Attributes

The playground relying party will request the following information from users logging in:

|Attribute|Attribute name|Comment|
|---------|--------------|-------|
|E-mail address|`email`|Mandatory - unverified
|Mobile phone number|`mobile`|Mandatory - unverified
Personal identification Number|`personalIdentificationNumber`|Mandatory - verified

## Emulating a Login

Using the form at <https://prodtest-login.diglias.com/test-eapi/> a login can be emulated. This webform performs an operation that normally would be done by the application integrating Diglias for authentication and identification.
In the form the CompanyName `playground`, and the key `LW4eUhQkJfwJGgQU8JCT/g==` should be entered. All other values can be kept as default.

![alt text](assets/images/test-eapi-form.png "Form for tetsing EAPI")

The first time a test Diglias tries to login to the playground relying party, the login will be refused. Since the relying party has been configured to request a verified personal identification number, the user will first have to “Level Up” to be able to login.

## Emulating a Level Up

To be able to login to the playground relying party, the used Diglias identity needs to have a verified personal identification number. For test purposes, this (a level up) can be achieved by emulating a verification operation. Use the same form (<https://prodtest-login.diglias.com/test-eapi/>) as used when emulating a login and supply the following information:

|Company Name|`playgroundAmbassador`
Key|`5osdC7Gs6OfHdHO9ZB7DaQ==`
Ambassador|`auth_rp_personalIdentificationNumber=197501015050`

The timestamp field will be automatically populated when the Ambassador field is filled out. To minimize the risk of a timeout, fill out the Ambassador field last, and submit the form immediately after.

During the level up, the user will be expected to set a PIN in the Diglias app when the personal identification number is appended to the Diglias.

Once the level up is completed, the user is able to login to the playground relying party.

## API Endpoint

To be able to integrate with the playground the API endpoint (<https://prodtest-login.diglias.com/main-eapi/begin>) should be used. This is necessary for the playground login to work properly with the playground version of the app and the relying party configurations.

## Sample Code

A set of sample integrations built in on different platforms:

|Platform|Features|Repository|
|--------|--------|----------|
|PHP|A basic authentication flow using the “playground” RP.|<https://github.com/diglias/sample-php-app>|
|node.js / Javascript|A basic authentication flow using the “playground” RP. The app will handle level-up/connect in the case where the Diglias Me used is missing a required attribute through the “playgroundAmbassador” RP.|<https://github.com/diglias/sample-node-app>|

You need sample code for a platform not listed? Let us know!

## Contact & Feedback

If you have any questions, improvement suggestions or any other reason to talk to us; please don’t hesitate to contact us:

<playground@diglias.com>
