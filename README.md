jQuery.upload
======================

A simple ajax file upload plugin
====

jQuery upload is jQuery plug-in to upload files by the Ajax style original written by [nkzawa](http://nkzawa.tumblr.com/). It is possible to upload files simply and easily in the same way as jQuery.post and the jQuery.get.

The latest version contains improvements by [Mr Rogers](https://github.com/rcode5/).

### Usage
 
Simply call upload method from the jQuery object, that containing input elements (type attribute is "file"). URL at the uploading destination, the callback method when completing it, and the data type of response are specified by arguments. To execute uploading simultaneously with file selection, use change event of the input element.

	$('input[type=file]').change(function() {
		$(this).upload('/action/to/upload', function(res) {
			alert('File uploaded');
		}, 'json');
	});
	
### Server-side

It is possible to access data as usual POST on the server side program. When the responses other than html and xml are returned, set "text/html" as Content-Type of header so that the download dialog of a browser would not be displayed.

Following is a PHP example.

	$filename = basename($_FILES['yourkey']['name']);
	if (move_uploaded_file($_FILES['yourkey']['tmp_name'], '/path/to/save/' . $filename)) {
		$data = array('filename' => $filename);
	} else {
		$data = array('error' => 'Failed to save');
	}

header('Content-type: text/html');
echo json_encode($data);

### Ducumentation

upload(url, [data], [callback], [type])

The file is uploaded asynchronously by posting data to the iframe generated in the same page. The callback function called when uploading is completed can be specified, and the data of the form specified by the fourth argument is received. The second argument is the parameter to be send at the same time.

All the fields are sent when the specified element has two or more fields in the descendant element.

When "data" is unnecessary, the method can be called by the following form.

	upload(url, callback, type)
url

Type: String
URL at uploading destination

data

Type: Map, String
Optional: Object, String or Array of Object that have pairs of key and value. The return value of serialize() and serializeArray() can be passed directly.

	{'key': 'value'}
	
	[{name:'key', value:'value'}]
	
	'key=value&...'
	
callback

Type: Function
Optional: Function called when uploading is completed. The response data is received by the argument.

	function(data) {
		// data could be xmlDoc, jsonObj, html, text.
	}
	
type

Type: String
Optional: Data format received by argument of callback function. "xml", "html", "script", "json", and "text" can be specified.

###Release Notes

1.0.3 April 6, 2013
use JSON.parse instead of window.eval and output pure JSON by rcode5

1.0.2 May 29, 2010

Compatible with jQuery 1.4.2.

1.0.1 April 22, 2010

Bug fix. When the element including radio buttons and checkboxes is selected, check is reset in IE6 and IE7.

1.0.0

Initial Release.	 

### Contribute

* feel free to fork this project and add/modify.  submit a pull request if you make exciting improvements.
