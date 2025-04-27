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

## ** Handling Dynamic Dropdowns**

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
### 2. ** Click on the dropdown to expand it.**
```java
WebElement dropdown = driver.findElement(By.cssSelector(".dropdown .selected"));
dropdown.click();
```
### 3. ** Get all the options**
```java
List<WebElement> options = driver.findElements(By.cssSelector(".dropdown .options li"));
```
### 4. ** Loop through options and click the one you want**
```java
for (WebElement option : options) {
    if (option.getText().equals("India")) {
        option.click();
        break;
    }
}
```








