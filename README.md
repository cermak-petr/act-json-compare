# act-json-compare
Apify act for comparing 2 JSON arrays of objects.

This act fetches JSON arrays from two urls ("old" and "new"), 
compares them and creates a new result set based on the act settings.
By default the final result set will contain only new and updated records.

**INPUT**

Input is a JSON object with the following properties:

```javascript
{
  "oldJson": OLD_JSON_URL,
  "newJson": NEW_JSON_URL,
  "idAttr": ID_ATTRIBUTE_NAME,
  "return": WHICH_RECORDS_TO_RETURN,    // optional, default: "new, updated"
  "addStatus": ADD_TEXT_STATUS          // optional, default: false
  "statusAttr": STATUS_ATTR_NAME        // optional, default: "status"
  "addChanges": ADD_CHANGE_INFO         // optional, default: false
  "changesAttr": CHANGES_ATTR_NAME      // optional, default: "changes"
  "updatedIf": [                        // optional, column list
    "column_1",
    "column_2",
    ...
  ]
}
```

The __idAttr__ parameter is a name of an attribute of each record, that will be used as it's ID.  
The __return__ parameter can be used to tell the act which records to include in the final result set. Possible values are __new__, __updated__, __deleted__ and __unchanged__, you can provide more than one separated by comma.  
The __addStatus__ parameter sets if the act should add a __status__ attribute to each of the resulting records.  
If true, it's value will be one of __NEW__, __UPDATED__, __DELETED__ or __UNCHANGED__, depending on the value of __return__ parameter.  
The __addChanges__ parameter tells the act to include a list of columns that contained changes. This list will be added to a new __changes__ column.  
The __changesAttr__ parameter overrides the default __changes__ column name, where the changes will be stored.  
The __updatedIf__ parameter can contain an array of column names. If set, the record will be recognized as __UPDATED__ if and only if there was a change in one of those columns. If __addChanges__ is set to __true__, the __changes__ array will contain the column names that had changes and are also present in the __updatedIf__ array.
