# clAjax

Simple JavaScript library for AJAX processing

## Download / Install clAjax

You can [download released versions of clAjax](https://sourceforge.net/projects/clajax) from SourceForge.

For Node.js developers, clAjax is also available from [npm](https://npmjs.org/) - just run `npm install clajax`.

## Examples
You can find into [/examples](https://github.com/surban1974/clajax/tree/master/examples) folder, or as demo:
 - [long polling](http://classhidra-surban1974.rhcloud.com/pooling)
 - [rest](http://classhidra-surban1974.rhcloud.com/restful)

## How to use
```javascript
	<!--  clAjax -->
	<script src='../js/clAjax.js'></script> 
```

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
	.setSuccess(function(http_request, instance){			
		processingSuccess(http_request,instance); 						
	})
	.setReady(function(http_request, instance){			
		processingReady(http_request,instance); 						
	})
	.setFail(function(http_request, instance){			
		processingFail(http_request,instance); 						
	})
	.setFinish(function(http_request, instance){			
		processingFinish(http_request,instance); 						
	})
	.setError(function(http_request, e, eToString, instance){			
		processingError(http_request, e, eToString,instance); 						
	})
	.setTimeout(function(http_request,instance){			
		processingTimeout(http_request,instance); 						
	})
	.request('GET');
```
alternatively
```javascript
new clajax({
	target:document.getElementById('target_div'),
	url:'../resource.html',
	success: function(http_request, instance){			
			processingSuccess(http_request,instance); 						
		},
	ready: function(http_request, instance){			
			processingReady(http_request,instance); 						
		},
	fail: function(http_request, instance){			
			processingFail(http_request,instance); 						
		},
	finish: function(http_request, instance){			
			processingFinish(http_request,instance); 						
		},
	error: function(http_request, e, eToString, instance){			
		processingError(http_request, e, eToString,instance); 						
		},
	timeout: function(http_request,instance){			
		processingTimeout(http_request,instance); 						
		}	
	})
	.request('GET');
```
- Method GET for different response's state and status
```javascript
var clAjax = 
	new clajax({
		acceptableReadyState:	[
			{
			readyState:3,
			acceptableStatus:[
				{
					status:	200,
					success: function(http_request,instance){ 			
						console.log(3200);
					}
			 	}													 	]
			},
			{
			readyState: 4,
			acceptableStatus:[
			 	{
			 		status:	200,
			 		success: function(http_request,instance){ 	
						console.log(4200);
					}
			 	},
			 	{
			 		status:	0,
			 		success: function(http_request,instance){ 			
						console.log(4000);
					}
			 	}	
				 	]
			}		
		],
		timeout: function(http_request,instance){
			console.log('timeout');
		},
		target:document.getElementById('target_div'),
		url:'../resource.html'
	})
	.request('GET');

```
- Extend object with user's variables/properties:
```javascript
var clAjax = 
	new clajax({
		extention:{
			response_length:0,
			interrupted:false,
			chunkcounter:0,
			setResponseLength: function(_response_length){
				this.response_length=_response_length;
				return this;
			},							
			setInterrupted: function(_interrupted){
				this.interrupted=_interrupted;
				return this;
			}
		},
		url:'../rest.html'
	})
	.instance()
	.request('GET');
	
...
clAjax
	.setResponseLength(0)
	.setInterrupted(false)
	.clone()
	.setUrl('longPolling?asyncInterrupt=false&tmp='+new Date().getTime())
	.request('GET');
```
- Methods POST / PUT / DELETE
```javascript
	new clajax({
		target:document.getElementById('rest_canvas'),
		url:'../rest.html',
		json: {
			'item':{
				'id':document.getElementById('item.id').value,
				'name':document.getElementById('item.name').value,
				'surname':document.getElementById('item.surname').value,
				'age':document.getElementById('item.age').value
			}
		},
		acceptableStatus: 	[{status:-1}] //any status
	}).request('POST');
...	
	new clajax({
		target:document.getElementById('rest_canvas'),
		url:'../rest.html',
		json: {
			'item':{
				'name':document.getElementById('item.name').value,
				'surname':document.getElementById('item.surname').value,
				'age':document.getElementById('item.age').value
			}
		},
		acceptableStatus: 	[{status:-1}] //any status
	}).request('PUT');
...
	new clajax({
		target:document.getElementById('rest_canvas'),
		url:'../rest.html?id='+document.getElementById('item.id').value,
		acceptableStatus: 	[{status:-1}] //any status
	}).request('DELETE');
```
