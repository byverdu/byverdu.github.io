---
permalink: e2e-tests-with-protractor-and-mocha
layout: post
title: e2e tests with protractor and mocha.
---

I have just started testing for the last 4 months and I really see the point about it. Now, writing code without testing it before feels like that I am doing it wrong. The only problem is that get used to test takes time (at least for me).

During the bootcamp that I attended, the tests were written in ruby using `RSpec` and `Capybara`. That was really pleasant if you compare it with javascript. Like I want to work with javascript I need to get used it, so.

<!-- more -->

I am trying to test as much I can in Javascript, my framework of choice is `Mocha` using the `Chai` library. Recently I had to do a test for a silly game based in AngularJS. 

For the Unit tests I am using `Karma`, in this case all the process was smooth and reasonable. <del>The problem was when I tried to start with the e2e tests, every single code snippet that I found wasn't working for me. With some lucky I started to see my tests green.</del>

The tests still green but after some digging I found the `chai-as-promised` plugin for the chai library. This plugin brings the javascript promises to chai.

`npm install -g chai-as-promised`

`npm install --save-dev chai-as-promised`

[chaiAsPromised Github repo](https://github.com/domenic/chai-as-promised)

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

<del>The only way that I have been able to pass the tests is by selecting an element using protractor's syntax, apply a protractor's function to the selected element and finally chain the `then()` function. The assertion is done inside the `then()` function using the parameter passed.</del>

Now we need to add some extra syntaxes like `.eventually`. 


{% highlight javascript %}
var chai     = require('chai');
var promised = require('chai-as-promised');
chai.use(promised) 
var expect   = chai.expect;

describe('wordsApp', function() {
  
  beforeEach(function(){ browser.get('/') });

  describe('On the Home page', function() {
    it('should have a title in the browser tab', function() {
    
      expect(browser.getTitle()).to.eventually.eq('wordGame');
    });

    it('should have a welcome title', function() {

      var header = element(by.css('h3'));
      expect(header.getText()).to.eventually.eq('Welcome to wordGame');
    });

    it('should display the English keyWord', function() {
      
      var keyWord = element(by.binding('keyWord'));
      expect(keyWord.isPresent()).to.eventually.be.true  
    });

    it('should display the English keyPhrase', function() {
      
      var keyPhrase = element(by.binding('keyPhrase'));
      expect(keyPhrase.isPresent()).to.eventually.be.true; 
    });

    it('should display the possible answers', function() {
      var spanish = element.all(by.repeater('spanish in spanishWords'));
      expect(spanish.count()).to.eventually.eq(3);
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







