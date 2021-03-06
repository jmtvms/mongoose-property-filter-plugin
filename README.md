# mongoose-property-filter-plugin
[![npm](https://img.shields.io/npm/v/mongoose-property-filter-plugin.svg?style=flat-square)](https://www.npmjs.com/package/mongoose-property-filter-plugin)
[![Travis](https://img.shields.io/travis/jmtvms/mongoose-property-filter-plugin.svg?style=flat-square)](https://travis-ci.org/jmtvms/mongoose-property-filter-plugin)
[![npm](https://img.shields.io/npm/dt/mongoose-property-filter-plugin.svg?style=flat-square)](https://www.npmjs.com/package/mongoose-property-filter-plugin)  
Mongoose plugin to easly remove properties from the schema without removing any data.

## How to use it
To use this module just add the reference to you javascript file.

```javascript
const mongoosePropertyFilter = require('mongoose-property-filter');
```

Then just add the plugin on the shcema app.

```javascript
const clientSchema = new Schema({
    name: {
        type: String,
        required: [true, 'Client name is mandatory']
    }
});

clientSchema.plugin(mongoosePropertyFilter);
```

## Configuring

You can configure the toJSON and toObject methods output properties filter from your schema using regex ``` /(_|deleted|created|updated).*/ ```, a whitespace separed string ``` "_id __v createdAt updatedAt deleted deletedAt deletedBy" ``` or even an array of strings ``` ["_id", "__v", "createdAt", "updatedAt", "deleted", "deletedAt, "deletedBy"] ```.

### Options available and their default values

|    Property   |            Type           |             Default             |                                                                         Description                                                                        |
|:-------------:|:-------------------------:|:-------------------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------:|
| **hide**          | Regexp, String, [String] | /(_\|deleted\|created\|updated).\*/ | Fields to be removed from the schema. |
| **showVirtuals**  |            Bool           |               false              | Force virtual fields to be shown.      
| **showGetters**  |            Bool           |               false              | Force getters fields to be shown.                                                                                                                       |
| **versionKey**    |            Bool           |              false              | Show the version key from the schema.                                                                                                                      |
| **_id**           |            Bool           |              false              | Show the _id field from the schema.                                                                                                                        |
| **allLevels**     |            Bool           |              true               | All nestes schemas are filtered too.                                                                                                                        |
| **applyToJSON**   |            Bool           |               true              | Should the filters be applied on the toJSON method from the schema.                                                                                        |
| **applyToObject** |            Bool           |              false              | Should the filters be applied on the toObject method from the schema.                                                                                      |
### Using the options on your schema



```javascript
const clientSchema = new Schema({
    name: {
        type: String,
        required: [true, 'Client name is mandatory']
    },
    myCustomField: {
        type: String,
    }
});

// With this options the JSON version of this schema will be { "name" : "Wally" }
const opt = { "hide" : "myCustomField" };
clientSchema.plugin(mongoosePropertyFilter, opt);
```
