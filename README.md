# Mongoose schema to JSON schema and back

## Motivation

This library represents a practical approach to convert the schemas used in a Mongoose model so that they can conveyed to hypermedia clients that interact with the web service.

## Usage

### Adding hypermedia controls in the Mongoose model

A Mongoose model should be augmented so that the schema options contains a JSON tranformation function:

```javascript
var mongoose = require('mongoose');

var schema = new mongoose.Schema({
	
}, {
	toJSON: {
		transform: function (doc, ret, options) {
			ret._links = {
				describedBy: {
					href: '/meta/models/example'
				}
			};
		}
	}
});

var model = mongoose.model('Example', schema);
```

Now, every time the model is converted to JSON, the representation will convey to the client the link that describes the schema of the document. The representation uses the [HAL](http://stateless.co/hal_specification.html) convention but other san be used as well.
