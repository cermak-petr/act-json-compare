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
  "return": WHICH_RECORDS_TO_RETURN,    // default: "new, updated"
  "addStatus": ADD_TEXT_STATUS          // default: false
}
```

The __idAttr__ parameter is a name of an attribute of each record, that will be used as it's ID.
The __return__ parameter can be used to tell the act which records to include in the final result set.
Possible values are __new__, __updated__, __deleted__ and __unchanged__, you can provide more than one separated by comma.
The __addStatus__ parameter sets if the act should add a __status__ attribute to each of the resulting records.
If true, it's value will be one of __NEW__, __UPDATED__, __DELETED__ or __UNCHANGED__, depending on the value of __return__ parameter.
