clAjax
=======

Simple JavaScript library for AJAX processing

##Download/Install clAjax

You can [download released versions of clAjax](https://sourceforge.net/projects/clajax) from SourceForge.

For Node.js developers, Knockout is also available from [npm](https://npmjs.org/) - just run `npm install clajax`.

##How to use

Deferred loading JavaScript/CSS
```javascript
new clajax()
	.setSuccess(function(){			
		new clajax().load('../css/bootstrap.min.css');
		new clajax().load('../js/utils.js'); 						
	})
	.load('../js/bootstrap-native.js');
```
alternatively
```javascript
new clajax({
	success: function(){			
		new clajax().load('../css/bootstrap.min.css');
		new clajax().load('../js/utils.js'); 						
		}
	})
	.load('../js/bootstrap-native.js');
```

Async request
- Method GET
```javascript
new clajax()
	.setUrl('../resource.html')
	.setTarget(document.getElementById('target_div'))
	.request('GET');
```
alternatively
```javascript
new clajax({
	target:document.getElementById('target_div'),
	url:'../resource.html'
	})
	.request('GET');
```
