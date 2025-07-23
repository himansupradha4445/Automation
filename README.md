# Automation

## XPath Types

### Absolute XPath
- It defines the complete path from the **root element** to the **target element**, **without skipping** any nodes in between.
- Absolute XPath starts with `/` (single forward slash) and often uses `[index]` to specify the position of elements.
- **Example**:  
  ```xpath
  /html/body/div[2]/div/div[1]/form/input[2]
### Relative XPath
- It is more flexible and specific to the target element, not requiring the full path from the root.
- Relative XPath starts with // (double forward slash) and uses a variety of symbols, functions, and axes to locate elements.
- **Example**:  
  ```xpath
  //input[@type='submit']

  

## Handling Dropdowns Using Selenium `Select` Class

### 1. **Import the `Select` Class**

```java
import org.openqa.selenium.support.ui.Select;
```

### 2. **Locate the Dropdown Element**

```html
<select id="country">
  <option value="us">United States</option>
  <option value="in">India</option>
  <option value="ca">Canada</option>
</select>
```

- Locate the `<select>` element using Selenium:

```java
WebElement countryDropdown = driver.findElement(By.id("country"));
```

### 3. **Create a Select Object**

```java
Select select = new Select(countryDropdown);
```

### 4. **Select Options**

You can select options in three different ways:

- **By Visible Text**
  
```java
select.selectByVisibleText("India");
```

- **By Value (the value attribute)**

```java
select.selectByValue("ca");
```

- **By Index (index starts from 0)**

```java
select.selectByIndex(1);  // "India" if it's second in the list
```

### 5. **Other Useful Methods**

- **Get Selected Option**

```java
WebElement selectedOption = select.getFirstSelectedOption();
System.out.println(selectedOption.getText());
```

- **Get All Options**

```java
List<WebElement> options = select.getOptions();
for (WebElement option : options) {
    System.out.println(option.getText());
}
```

- **Check if Multiple Selections Are Allowed**

```java
boolean isMultiple = select.isMultiple();
```

- **Deselect Methods** (only for multi-select dropdowns)

```java
select.deselectAll();
select.deselectByValue("ca");
select.deselectByVisibleText("India");
select.deselectByIndex(1);
```

- **Example Full Code**

```java
WebElement countryDropdown = driver.findElement(By.id("country"));
Select select = new Select(countryDropdown);

select.selectByVisibleText("India");  // selecting India
System.out.println("Selected country: " + select.getFirstSelectedOption().getText());
```

## **Handling Dynamic Dropdowns**

### 1. **Locate the Dropdown Element**
```html
<div class="dropdown">
  <div class="selected">Select a country</div>
  <ul class="options">
    <li>United States</li>
    <li>India</li>
    <li>Canada</li>
  </ul>
</div>
```
### 2. **Click on the dropdown to expand it.**
```java
WebElement dropdown = driver.findElement(By.cssSelector(".dropdown .selected"));
dropdown.click();
```
### 3. **Get all the options**
```java
List<WebElement> options = driver.findElements(By.cssSelector(".dropdown .options li"));
```
### 4. **Loop through options and click the one you want**
```java
for (WebElement option: options) {
    if (option.getText().equals("India")) {
        option.click();
        break;
    }
}
```
## Mouse Hover Actions

**Steps to perform a mouse hover:**

### 1. Import the Actions class:

```java
import org.openqa.selenium.interactions.Actions;
```

### 2. Create an Actions object:

```java
Actions actions = new Actions(driver);
```

### 3. Move to the element (hover):

```java
actions.moveToElement(element).perform();
```

**Example:**
Suppose you have this HTML:

```html
<div class="menu">
  <button id="products">Products</button>
  <div class="submenu">
    <a href="/laptops">Laptops</a>
    <a href="/phones">Phones</a>
  </div>
</div>
```

When you hover over the Products button, a submenu appears.

## LOCATORSTARTEGY

```html
<!DOCTYPE html>
<html>
<head>
    <title>Locator Strategies Example</title>
</head>
<body>

<h1>Welcome to My Website</h1>

<form id="loginForm">
    <input type="text" id="username" name="username" placeholder="Enter Username" class="input-field">
    <input type="password" id="password" name="password" placeholder="Enter Password" class="input-field">
    <button type="submit" class="btn btn-login">Login</button>
</form>

<a href="/forgot-password" id="forgotLink">Forgot Password?</a>

</body>
</html>
```

### 1. ID Locator

```java
 WebElement username = driver.findElement(By.id("username"));
        username.sendKeys("testUser");
```

### 2. Name Locator

```java
 WebElement password = driver.findElement(By.name("password"));
        password.sendKeys("testPass");
```

### 3. Class Name Locator

```java
 WebElement loginButton = driver.findElement(By.className("btn-login"));
        loginButton.click();
```

### 4. Tag Name Locator

```java
WebElement heading = driver.findElement(By.tagName("h1"));
        System.out.println("Page Heading: " + heading.getText());
```

### 5. Link Text Locator

```java
 WebElement forgotLink = driver.findElement(By.linkText("Forgot Password?"));
        forgotLink.click();
```

### 6. Partial Link Text Locator

```java
 WebElement partialForgotLink = driver.findElement(By.partialLinkText("Forgot"));
        partialForgotLink.click();
```
### 7. CSS Selector Locator

- ID
```java
driver.findElement(By.cssSelector("#username"));
```
**Syntax**-# is used for ID.
- Class Name
```java
driver.findElement(By.cssSelector(".btn-login"));
```
**Syntax**-. is used for Class Name.
- Attribute
```java
driver.findElement(By.cssSelector("input[name='username']"));
```
**Syntax**: tagname[attribute='value']
- Indexing
```java
WebElement element = driver.findElement(By.cssSelector("div:nth-child(1)"));
```
**Syntax**:tag:nth-child(index)
- Parent-Child (Direct Child)
```java
driver.findElement(By.cssSelector("div > span"));
```
**Syntax**:
```text
parent > child
```
- Parent-Child (Any Descendant)
```java
driver.findElement(By.cssSelector("div span"));
```
**Syntax**:

```text
parent descendant
```
- Regular Expression
  - ^= (starts with)
  ```java
  driver.findElement(By.cssSelector("input[name^='user']"));
  ```
  **Syntax**:
  ```text
  tagname[attribute^='value']
  ```
  - $= (ends with)
  ```java
  driver.findElement(By.cssSelector("input[name$='name']"));
  ```
  **Syntax**:
  ```text
  tagname[attribute$='value']
  ```
  - *= (contains)
  ```java
  driver.findElement(By.cssSelector("input[name*='pass']"));
  ```
  **Syntax**:
  ```text
  tagname[attribute*='value']
  ```

### 8. XPath Locator
- Attribute
```java
driver.findElement(By.xpath("//input[@name='password']"));
```
**Syntax**: //tagname[@attribute='value']
- Indexing
```java
// Select the second button with class='submit-btn'
WebElement element = driver.findElement(By.xpath("(//button[@class='submit-btn'])[2]"));
```
**Syntax**:xpath_expression[index]
- Parent-Child (Direct Child)
```java
driver.findElement(By.xpath("//div/span"));
```
**Syntax**:
```text
//parent/child
```
- Parent-Child (Any Descendant)
```java
driver.findElement(By.xpath("//div//span"));
```
**Syntax**:
```text
//ancestor//descendant
```
- Regular Expression
  - contains()
    ```java
    driver.findElement(By.xpath("//input[contains(@name, 'pass')]"));
    ```
  **Syntax**:
   ```text
      //tagname[contains(@attribute,'partialValue')]
    ```
  - starts-with()
    ```java
    driver.findElement(By.xpath("//input[starts-with(@id, 'user')]"));
    ```
  **Syntax**:
    ```text
    //tagname[starts-with(@attribute,'partialStart')]
    ```
  - Match text using contains()
    ```java
    driver.findElement(By.xpath("//button[contains(text(), 'Login')]"));
    ```
    **Syntax**:
    ```text
    //tagname[contains(text(),'partialText')]
    ```

## METHODS OF WEBDRIVER
- 1. Browser Window Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `get(String url)` | Open a URL | `driver.get("https://google.com");` |
| `getTitle()` | Get the page title | `String title = driver.getTitle();` |
| `getCurrentUrl()` | Get the current URL | `String url = driver.getCurrentUrl();` |
| `getPageSource()` | Get the page HTML source code | `String source = driver.getPageSource();` |
| `close()` | Close the current browser window | `driver.close();` |
| `quit()` | Close all browser windows and end session | `driver.quit();` |

---

- 2. Navigation Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `navigate().to(String url)` | Navigate to a URL | `driver.navigate().to("https://google.com");` |
| `navigate().back()` | Go back to the previous page | `driver.navigate().back();` |
| `navigate().forward()` | Move forward to the next page | `driver.navigate().forward();` |
| `navigate().refresh()` | Refresh the current page | `driver.navigate().refresh();` |

- 3. Browser Window Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `get(String url)` | Open a URL | `driver.get("https://google.com");` |
| `getTitle()` | Get the page title | `String title = driver.getTitle();` |
| `getCurrentUrl()` | Get the current URL | `String url = driver.getCurrentUrl();` |
| `getPageSource()` | Get the page HTML source code | `String source = driver.getPageSource();` |
| `close()` | Close the current browser window | `driver.close();` |
| `quit()` | Close all browser windows and end session | `driver.quit();` |

- 4. Window Management Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `manage().window().maximize()` | Maximize the window | `driver.manage().window().maximize();` |
| `manage().window().minimize()` | Minimize the window | `driver.manage().window().minimize();` |
| `manage().window().fullscreen()` | Fullscreen the window | `driver.manage().window().fullscreen();` |
| `manage().window().setSize(Dimension size)` | Set window size | `driver.manage().window().setSize(new Dimension(1024, 768));` |

- 5. Timeout Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `manage().timeouts().implicitlyWait(Duration time)` | Set implicit wait time | `driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));` |
| `manage().timeouts().pageLoadTimeout(Duration time)` | Set page load timeout | `driver.manage().timeouts().pageLoadTimeout(Duration.ofSeconds(30));` |
| `manage().timeouts().scriptTimeout(Duration time)` | Set script timeout | `driver.manage().timeouts().scriptTimeout(Duration.ofSeconds(20));` |

- 6. Cookie Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `manage().getCookies()` | Get all cookies | `Set<Cookie> cookies = driver.manage().getCookies();` |
| `manage().getCookieNamed(String name)` | Get cookie by name | `Cookie cookie = driver.manage().getCookieNamed("session_id");` |
| `manage().addCookie(Cookie cookie)` | Add a cookie | `driver.manage().addCookie(new Cookie("username", "himansu"));` |
| `manage().deleteCookieNamed(String name)` | Delete cookie by name | `driver.manage().deleteCookieNamed("username");` |
| `manage().deleteAllCookies()` | Delete all cookies | `driver.manage().deleteAllCookies();` |

- 7. SwitchTo Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `switchTo().frame(int index)` | Switch to frame by index | `driver.switchTo().frame(0);` |
| `switchTo().frame(String nameOrId)` | Switch to frame by name or ID | `driver.switchTo().frame("frameName");` |
| `switchTo().frame(WebElement frameElement)` | Switch to frame using WebElement | `driver.switchTo().frame(driver.findElement(By.id("frameId")));` |
| `switchTo().parentFrame()` | Switch to parent frame | `driver.switchTo().parentFrame();` |
| `switchTo().defaultContent()` | Switch to default content | `driver.switchTo().defaultContent();` |
| `switchTo().window(String windowHandle)` | Switch to another window or tab | `driver.switchTo().window(windowHandle);` |
| `switchTo().alert()` | Switch to alert popup | `driver.switchTo().alert().accept();` |

- 8. Finding Elements Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `findElement(By locator)` | Find a single element | `WebElement element = driver.findElement(By.id("username"));` |
| `findElements(By locator)` | Find multiple elements | `List<WebElement> links = driver.findElements(By.tagName("a"));` |

----------

## WEBELEMENTMETHODS

| Method | Description | Example |
|:-------|:------------|:--------|
| `click()` | Click the element | `driver.findElement(By.id("loginBtn")).click();` |
| `sendKeys(CharSequence... keysToSend)` | Enter text into a text box | `driver.findElement(By.id("username")).sendKeys("himansu");` |
| `clear()` | Clear the text field | `driver.findElement(By.id("username")).clear();` |
| `getText()` | Get the visible text of the element | `String text = driver.findElement(By.id("msg")).getText();` |
| `getAttribute(String attributeName)` | Get the value of a specific attribute | `String value = driver.findElement(By.id("username")).getAttribute("value");` |
| `getCssValue(String propertyName)` | Get the value of a CSS property | `String color = driver.findElement(By.id("btn")).getCssValue("color");` |
| `getTagName()` | Get the tag name of the element | `String tag = driver.findElement(By.id("logo")).getTagName();` |
| `isDisplayed()` | Check if the element is visible | `boolean isVisible = driver.findElement(By.id("popup")).isDisplayed();` |
| `isEnabled()` | Check if the element is enabled | `boolean isEnabled = driver.findElement(By.id("submit")).isEnabled();` |
| `isSelected()` | Check if a checkbox or radio button is selected | `boolean isChecked = driver.findElement(By.id("remember")).isSelected();` |
| `submit()` | Submit a form | `driver.findElement(By.id("formLogin")).submit();` |

## Actions Class Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `click()` | Click at the current mouse location | `new Actions(driver).click().perform();` |
| `click(WebElement element)` | Click on a specific element | `new Actions(driver).click(element).perform();` |
| `doubleClick()` | Double-click at the current mouse location | `new Actions(driver).doubleClick().perform();` |
| `doubleClick(WebElement element)` | Double-click on a specific element | `new Actions(driver).doubleClick(element).perform();` |
| `contextClick()` | Right-click at the current mouse location | `new Actions(driver).contextClick().perform();` |
| `contextClick(WebElement element)` | Right-click on a specific element | `new Actions(driver).contextClick(element).perform();` |
| `moveToElement(WebElement element)` | Hover mouse over an element | `new Actions(driver).moveToElement(element).perform();` |
| `dragAndDrop(WebElement source, WebElement target)` | Drag source element and drop onto target element | `new Actions(driver).dragAndDrop(source, target).perform();` |
| `sendKeys(CharSequence keys)` | Send keys (keyboard actions) | `new Actions(driver).sendKeys(Keys.ENTER).perform();` |
| `keyDown(Keys key)` | Press and hold a key | `new Actions(driver).keyDown(Keys.CONTROL).perform();` |
| `keyUp(Keys key)` | Release a pressed key | `new Actions(driver).keyUp(Keys.CONTROL).perform();` |

## JavascriptExecutor Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `executeScript(String script, Object... args)` | Execute JavaScript code in the browser | `((JavascriptExecutor) driver).executeScript("alert('Hello World');");` |
| `executeAsyncScript(String script, Object... args)` | Execute asynchronous JavaScript code | `((JavascriptExecutor) driver).executeAsyncScript("window.setTimeout(arguments[arguments.length - 1], 5000);");` |

## Select Class Methods

| Method | Description | Example |
|:-------|:------------|:--------|
| `selectByVisibleText(String text)` | Select option by visible text | `new Select(driver.findElement(By.id("country"))).selectByVisibleText("India");` |
| `selectByIndex(int index)` | Select option by index | `new Select(driver.findElement(By.id("country"))).selectByIndex(2);` |
| `selectByValue(String value)` | Select option by value attribute | `new Select(driver.findElement(By.id("country"))).selectByValue("IN");` |
| `getOptions()` | Get all options from dropdown | `List<WebElement> options = new Select(driver.findElement(By.id("country"))).getOptions();` |
| `getFirstSelectedOption()` | Get the first selected option | `WebElement selected = new Select(driver.findElement(By.id("country"))).getFirstSelectedOption();` |
| `isMultiple()` | Check if dropdown allows multiple selections | `boolean multiple = new Select(driver.findElement(By.id("country"))).isMultiple();` |
| `deselectAll()` | Deselect all selected options (only for multi-select) | `new Select(driver.findElement(By.id("languages"))).deselectAll();` |
| `deselectByVisibleText(String text)` | Deselect option by visible text | `new Select(driver.findElement(By.id("languages"))).deselectByVisibleText("English");` |
| `deselectByIndex(int index)` | Deselect option by index | `new Select(driver.findElement(By.id("languages"))).deselectByIndex(1);` |
| `deselectByValue(String value)` | Deselect option by value | `new Select(driver.findElement(By.id("languages"))).deselectByValue("en");` |


## TEST CASE and TEST SUIT

### Test Case : It is a set of steps used to verify a particular functionality of an application.
EXAMPLE : Web Application Login

- **Test Case ID**: TC001  
- **Title**: Verify login with valid credentials  
- **Description**: Ensure the user can log in successfully with valid credentials.

🔹 Pre-Conditions
- User is on the login page
- Valid credentials exist in the system

🔹 Test Steps
1. Launch the application URL  
2. Enter a valid username: `user@example.com`  
3. Enter a valid password: `password123`  
4. Click on the **Login** button

🔹 Expected Result
- The user should be redirected to the **Dashboard/Home** page.

---

### Test Suits : It is a collection of test cases, logically grouped together to test a specific module or functionalty.

EXAMPLE: User Login Module  
This test suite contains multiple test cases related to the Login feature of the application.

| Test Case ID | Test Case Description                      |
|--------------|---------------------------------------------|
| TC001        | Login with valid credentials               |
| TC002        | Login with invalid password                |
| TC003        | Login with empty username/password fields  |
| TC004        | Reset password flow                        |
| TC005        | Login page UI elements presence            |











