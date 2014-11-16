---
permalink: e2e-tests-with-protractor-and-mocha
layout: post
title: e2e tests with protractor and mocha.
---

I have just started testing for the last 4 months and I really see the point about it. Now, writing code without testing it before feels like if I am doing it wrong. The only problem is that get used to test takes time (at least for me).

During the bootcamp that I have been attending, all the tests used to be in ruby using `RSpec` and `Capybara`. That was really pleasant if you compare it with javascript. Like I want to work with javascript I need to get used it, so.

<!-- more -->

I am trying to test as much I can in Javascript, my framework of choice is `Mocha` using the `Chai` library. Recently I had to do a test for a silly game based in AngularJS. 

For the Unit tests I am using `Karma`, in this case all the process was smooth and reasonable. The problem was when I tried to start with the e2e tests, every single code snippet that I found wasn't working for me. With some lucky I started to see my tests green.

### <i class="fa fa-code"></i> protractor-config.js

{% highlight javascript %}
exports.config = {

	framework:       'mocha',
	baseUrl: 'http://localhost:3000',

	specs: ['test/e2e/*.js'],
	capabilities: {
    'browserName': 'chrome'
  }           

}
{% endhighlight %}  

### <i class="fa fa-code"></i> homePageSpec.js

The only way that I have been able to pass the tests is by selecting an element using protractor's syntax, apply a protractor's function to the selected element and finally chain the `then()` function. The assertion is done inside the `then()` function using the parameter passed.


{% highlight javascript %}
var chai   = require('chai');
var expect = chai.expect;

describe('wordsApp', function() {
  
  beforeEach(function(){ browser.get('/') });

  describe('On the Home page', function() {
    it('should have a title in the browser tab', function() {
    
      browser.getTitle().then(function(text) { 
        expect(text).to.eq('wordGame');
      })
    });

    it('should have a welcome title', function() {
      
      element(by.css('h3')).getText().then(function(text){

        expect(text).to.eq('Welcome to wordGame');
      })
    });

    it('should display the English keyWord', function() {
      
      element(by.binding('keyWord')).isPresent().then(function(elem){

        expect(elem).to.be.true  
      });  

    });

    it('should display the English keyPhrase', function() {

      element(by.binding('keyPhrase')).isPresent().then(function(elem){

        expect(elem).to.be.true
      })
    });

    it('should display the possible answers', function() {
      
      element.all(by.repeater('spanish in spanishWords')).count().then(function(count){

        expect(count).to.eq(3);
      });
    });
  });
});
{% endhighlight %} 


{% highlight html %} 

<!DOCTYPE html>
<html ng-app="wordsApp">

<head>
  <meta charset="utf8">
  <title>wordGame</title>
</head>

<body>
  <div ng-controller="WordsCtrl">
		<h3>Welcome to wordGame</h3>
		<section>
		 <h5 ng-bind="keyWord"></h5>
		 <p ng-bind="keyPhrase"></p>
		 <ol>
		 	<li ng-repeat="spanish in spanishWords">
		 		{% raw %} {{spanish}} {% endraw %}
		 	</li>
		 </ol>
		</section>
	</div>
</body>
</html>

{% endhighlight %} 

You can take a look to the whole repo [here](https://github.com/byverdu/BussuAngularTest)

Please let me know if there is mistakes and another way!!!!







