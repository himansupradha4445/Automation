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
