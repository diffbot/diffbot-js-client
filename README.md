# Diffbot API JavaScript client

## Preface

This API uses the JSONP protocol to support cross domain communication.

## Installation

Include the following JavaScript file just before the closing </head> tag of your HTML document, this assumes your HTML document resides in the same folder.

```
   <script type="text/javascript" src="diffbot.js"></script>
```

## Configuration

To access the API, you first need to create an instance of the Diffbot class.

```JavaScript
 var client = new DiffBot("your token");
```
Replacing your token with your developer token.

The library takes care of passing your API token with all API calls for the lifetime of the object.

## Usage

### Article API

Assume that we have our `client` configured. Now we can call the get function on the article to retrieve the data we need.
The url parameter must be an absolute url of the page you are retreiving data for.

```JavaScript
	 client.article.get({
            url: "http://www.xconomy.com/san-francisco/2012/07/25/diffbot-is-using-computer-vision-to-reinvent-the-semantic-web/"
        }, function onSuccess(response) {
			// output the summary
			document.getElementById("content").write(response.summary);
        }, function onError(response) {
			  switch(response.errorCode) {
				case "401":
					break;
				case "404": 
					break;
				case "500":
					break;
			  }
		});
});
```

The first parameter accepts an object with properties as specified in the DiffBot API documentation which can be found here:
http://diffbot.com/products/automatic/article/

The second parameter is a callback function which is called if your lookup to the API is successful. The callback function is passed a single parameter containing a JSON object with all of the information returned from the DiffBot API.

The third parameter is a callback function which is called should an error occur during your lookup. 
For example if the page you have request cannot be found, the example above demonstrates how you can differentiate between the error types using the errorCode property returned from 
the API

For detailed documentation of the arguments for the request, and the JSON data returned as part of the response see the DiffBot article documentation.
http://diffbot.com/products/automatic/article/


### Analyze API

Calling the Analyze API is the same as calling the article API, just calling a different function within the client.

```JavaScript
	 client.analyze.get({
            url: "http://www.xconomy.com/san-francisco/2012/07/25/diffbot-is-using-computer-vision-to-reinvent-the-semantic-web/"
        }, function onSuccess(response) {
			// output the summary
			document.getElementById("content").write(response.summary);
        }, function onError(response) {
			  switch(response.errorCode) {
				case "401":
					break;
				case "404": 
					break;
				case "500":
					break;
			  }
		});
});
```

The first parameter accepts an object with properties as specified in the DiffBot API documentation which can be found here:
http://diffbot.com/products/automatic/classifier/

The second parameter is a callback function which is called if your lookup to the API is successful. The callback function is passed a single parameter containing a JSON object with all of the information returned from the DiffBot API.

The third parameter is a callback function which is called should an error occur during your lookup. 
For example if the page you have request cannot be found, the example above demonstrates how you can differentiate between the error types using the errorCode property returned from 
the API

For detailed documentation of the arguments for the request, and the JSON data returned as part of the response see the DiffBot article documentation.
http://diffbot.com/products/automatic/classifier/


### Error handling

Each function has a onError parameter which can be utilised to handle errors returned from the DiffBot API.

The callback function passes a single argument which is an object returned by the service.

Here's an example of an error object returned to the callback function :

```
	{ error: "Not authorized API token.", errorCode: 401 }
```

-Initial commit by Craig Cooke-
