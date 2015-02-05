Mongoose i18n Schema Plugin
===========================

Surprisingly there is not a proper plugin for this.
I found a couple gists that do this:

- [as a plugin](https://gist.github.com/viczam/3306456d3c63e2c21f1d)
- [extending Schema class](https://gist.github.com/hetsch/3925111)

I didn’t see anything in the npm repo, so...

Usage
-----

Install:

```bash
npm i --save mongoose mongoose-i18n
```

Create your schema:

```coffee-script
mongoose = require 'mongoose'
i18nPlugin = require 'mongoose-i18n'

TranslatableSchema = new Schema
    value : { type: String, i18n: true, required: true }

TranslatableSchema.plugin(i18n, { languages: ['en_US', 'es_ES', 'fr_FR'], defaultLanguage: 'en_US' })

Translatable = mongoose.model('Translatable', TranslatableSchema)

```
Set/Get the value of translatable property

```coffee-script
translatableObject = new Translatable()

# ... set the value in default language  ... #

translatableObject.value.i18n = "Hello"

# ... set the value in specific language  ... #

translatableObject.value.es_ES = "Hola"

# ... get the value in default language  ... #

value = translatableObject.value.i18n;

# ... get the value in specific language  ... #

value = translatableObject.value.es_ES;
```

Convert object to translated Object/Json 
```coffee-script

translatableObject.toObjectTranslated(translation: 'es_ES')

translatableObject.toJSONTranslated(translation: 'es_ES')
```
you will get 

	{
		"value": "Hola"
	}

when the original is
	
	{
		"value": { 
			"en_US" : "Hello",
			"es_ES" : "Hola" 
		}
	}