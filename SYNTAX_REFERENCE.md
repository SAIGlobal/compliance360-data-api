# Compliance 360 API Syntax Reference
The documentation below provides a syntax reference for the Compliance 360 REST api.

## Identifiers
All objects in the Compliance 360 system are identified by scoped tokens. The token format has the following structure:

### Format
<strong>{SCOPE}:{ID}</strong>

| Item  | Description                                                  |
|------ | -----------                                                  |
| SCOPE | The scope is a uri string that uniquely identifies the item. |
| ID    | The numeric Id of the component.                             |

### Scope Segments
| Item      | Description                                                  |
|------     | -----------                                                  |
| Module    | The name of the application module.                          |
| Component | The name of the component.                                   |
| Type      | The type name of component.                                  |

```
Example:
EmployeeManagement/Employee/Default:20
```
## Selection
By default the API will return responses that only include the object Id token value. If you 
would like to have data values included in the response, then they must be explicitly requested. 

### Format
The selection is a comma separated list of field names
```
Example:
FirstName,LastName,DateCreated
```

## Filtering
The API supports a robust filtering schema with support for multiple criteria, nested criteria statements, \"AND\" and  \"OR\" grouping and multiple comparison operators.

### Criteria Format
A criteria statement is in the format <strong>{FIELD}{OPERATOR}{VALUE}</strong>
```
Example:
FirstName=John
```

### Criteria Operators

| Operator      | Description                   |
|------         | -----------                   |
| =             | Equals.                       |
| !=            | Not Equals.                   |
| <             | Less than.                    |
| <=            | Less than or equal to.        |
| >             | Greater than.                 |
| >=            | Greater than or equal to.     |
| ~             | Contains the value.           |
| !~            | Does not contain the value.   |
| =~            | Starts with the value.        |
| ~=            | Ends with the value.          |

### And / Or and Grouping
Criteria statements can be combined with AND/OR logic and can be grouped with parentheses "( )"

| Operator      | Description                   |
|------         | -----------                   |
| &             | AND operator.                 |
| ;             | Alternate AND operator.       |
| \|            | OR operator.                  |

### String Criteria
Please note that all string criteria values must be quoted with single or double quotes. Both of the examples below are valid string type criteria statements.
```
Example 1:
FirstName="John"

Example 2:
FirstName='John'
```

### Complex Criteria Example
The example below will return records where the FirstName starts with "J" and 
the LastName is equal to "O'Malley" or the HireDate is greater than "1/1/2018".
```
Example:
(FirstName=~'J';LastName="O'Malley")|(HireDate>'2010-01-01T00:00:00')
```

## Order
A comma separated list of field tokens used to specify sort operations during \"Find\" processes.

### Order Token Format
<strong>{SORT_DIRECTION}{FIELD}</strong>

| Operator      | Description                   |
|------         | -----------                   |
| -             | Sort descending               |
| +             | Sort ascending                |

### Order Example
The example below will sort by FirstName ascending and then by HireDate descending.
```
Example:
+FirstName,-HireDate
```
