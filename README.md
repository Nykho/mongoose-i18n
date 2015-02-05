Mongoose i18n Schema Plugin
===========================

Forked from [justin-lau/mongoose-i18n](https://github.com/justin-lau/mongoose-i18n)

Usage
-----

Install:

```bash
npm i --save mongoose varavut/mongoose-i18n
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