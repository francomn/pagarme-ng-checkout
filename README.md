# [pagarme-ng-checkout](https://github.com/pagarme/pagarme-ng-checkout)
Angular service to provide pagar.me checkout functionality to your Angularjs application.

**[Demo here](http://pagarme.github.io/pagarme-ng-checkout/)**


## Instructions

Import both pagar.me checkout.js and pagarme-ng-checkout.js

```html
<script src="https://assets.pagar.me/checkout/checkout.js"></script>
<script src="lib/pg-ng-checkout.js"></script>
```

Import into your application and on the config stage set your pagar.me encryption key (test or live)

```javascript
angular.module('my-awesome-ecommerce', ['pg-ng-checkout'])
.config(function($pgCheckoutProvider){

  $pgCheckoutProvider.setEncryptKey('ek_live_mRVAfBPidrKieIX53fGPlLfchMMk3A');

});
```


Inject the service `$pgCheckout` anywhere you want.
To open the checkout modal just call the `open` method of the injected service.

```javascript
angular.module('my-awesome-ecommerce', [])
.directive('checkoutButton', function($pgCheckout){

  return{
  
    link: function($scope, $element){
    
      var params = {"amount":"100000"};
    
      //open checkout on button click
      $element.on('click', function(){
      
        $pgCheckout.open(params);
      
      });
    
    }
  
  }

})
```

## Callbacks

Pass a success function callback when opening the checkout instance.
The provided callback is called when the user has successfully finished his purchase via checkout.

```javascript

var params = {"amount":"100000"};

$pgCheckout.open(params, function(){

  //purchase done code here
  alert('The purchase is done! :D');

});
```

## Checkout data attributes
You may pass any attribute that you would pass via html data-attributes on the conventional importation method (via script tag) on the open method params.

```javascript
var params = {"customerData":false, "amount":"100000", "createToken": "false"};
$pgCheckout.open(params);
```

## Retrieving `card_hash` or transaction `token`

You can access all variables that you would be able to get trough post vars on your backend trough success callback parameter.

```javascript
var params = {"customerData":false, "amount":"100", "createToken": "true"};
$pgCheckout.open(params, callback);

function callback(data){

   var token = data.token;

}
```

And that's it! :D

[Rafael Violato](http://rviolato.com) @ [pagar.me](http://pagar.me)

## Support
If you have any problem or suggestion please open an issue [here](https://github.com/pagarme/pagarme-ng-checkout/issues).

## License

Check [here](LICENSE).
