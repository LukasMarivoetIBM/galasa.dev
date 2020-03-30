---
path: "/docs/managers/selenium-manager"
title: "Selenium Manager"
---

**ALPHA - This Manager is being actively developed. It is subject to change and has not been extensively tested.**

## Overview
This Manager enables the test to run Selenium WebDrivers in order to drive Web Browsers during the test. Browsers can have actions performed against them  to navigate WebPages and extract information about the current page. <br><br> As an absolute minimum, the CPS property <br> <code>selenium.instance.PRIMARY.gecko.path</code><br> must be provided as the manager will default to using a GECKO WebDriver if no WebDriver is provided. <br><br> The CPS property <br> <code>selenium.instance.PRIMARY.web.driver</code><br> can be used to set a different WebDriver to be used. This will also require the corresponding driver path to be set. <br> eg. <code>selenium.instance.PRIMARY.web.driver=CHROME</code><br> requires <code>selenium.instance.PRIMARY.chrome.path=...</code><br>

## Limitations
The Selenium Manager only supports GECKO, CHROME, EDGE and IE WebDrivers




## Code snippets

Use the following code snippets to help you get started with the Selenium Manager.
 
### Create the Selenium Manager

The following snippet shows the minimum code that is required to request the Selenium Manager in a test:

```
@SeleniumManager
public ISeleniumManager seleniumManager;
```

The code creates an interface to the Selenium Manager which will allow the tester to provision WebPages to test against.

### Create a WebPage

```
IWebPage page = seleniumManager.allocateWebPage("https://galasa.dev/");
```

The code creates a WebPage with a Selenium WebDriver controlling the browser. This object provides an interface for the tester to perform actions on the page to navigate around, check the page content and switch between windows.

At the end of the test, the Selenium Manager automatically closes down the WebDriver which removes the WebPage.

There is no limit in Galasa on how many Selenium WebPages can be used within a single test. The only limit is the ability of the Galasa Ecosystem they are running on to support the Selenium WebDrivers not timing out.

### Navigating around a WebPage Browser

```
page.clearElementByCssSelector("input.js-search-input.search__input--adv");
page.sendKeysToElementByClass("js-search-input.search__input--adv", "Galasa");
page.clickElementById("search_button_homepage");
```

The code showcases different actions which can be performed on a WebPage interface to interact with different WebElements on the Browser. These WebElements are selected using a range of different techniques which allows the tester flexibility in how they are selected.

### Extracting WebPage information

```
WebElement element = page.findElementById("search_button_homepage");
String pageTitle = page.getTitle();
String pageSource = page.getPageSource();
```

The code shows different ways of gaining information about the WebPage to be tested against. Extracting the title is a very simple way of checking if the WebDriver is on the correct page and making sure that a WebElement is found.

## Configuration Properties

The following are properties used to configure the Selenium Manager.
 
<details>
<summary>Selenium DSE Instance CPS Property</summary>

| Property: | Selenium DSE Instance CPS Property |
| --------------------------------------- | :------------------------------------- |
| Name: | selenium.dse.instance.name |
| Description: | Provides a DSE instance for selenium properties |
| Required:  | No |
| Default value: | PRIMARY |
| Valid values: | A valid uppercase String |
| Examples: | <code>selenium.dse.instance.name=PRIMARY</code> |

</details>
 
<details>
<summary>Selenium Gecko Profile CPS Property</summary>

| Property: | Selenium Gecko Profile CPS Property |
| --------------------------------------- | :------------------------------------- |
| Name: | selenium.instance.INSTANCE.gecko.profile |
| Description: | Provides a profile to use when using the gecko driver for extensions |
| Required:  | No |
| Default value: | $default |
| Valid values: | A valid String name of a profile |
| Examples: | <code>selenium.instance.PRIMARY.gecko.profile=default</code> |

</details>
 
<details>
<summary>Selenium Driver Type CPS Property</summary>

| Property: | Selenium Driver Type CPS Property |
| --------------------------------------- | :------------------------------------- |
| Name: | selenium.instance.INSTANCE.web.driver |
| Description: | Provides the browser of the webdriver needed for a given instance |
| Required:  | Yes |
| Default value: | $default |
| Valid values: | GECKO,IE,EDGE,CHROME |
| Examples: | <code>selenium.instance.PRIMARY.web.driver=GECKO</code> |

</details>
 
<details>
<summary>Selenium Driver Path CPS Property</summary>

| Property: | Selenium Driver Path CPS Property |
| --------------------------------------- | :------------------------------------- |
| Name: | selenium.instance.INSTANCE.browser.path |
| Description: | Provides a path to the webdriver on the system being tested |
| Required:  | Yes |
| Default value: | $default |
| Valid values: | A valid String representation of a path |
| Examples: | <code>selenium.instance.PRIMARY.chrome.path=/usr/bin/chromedriver</code> |

</details>