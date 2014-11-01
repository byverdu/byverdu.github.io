---
permalink: how-to-do-a-tooltip-only-using-css
layout: post
title: How to do a tooltip only using CSS
---

After working in a project I have been using a lot the CSS pseudo-elements `:after` and `:before` and as well doing triangles with CSS borders. Then something crossed my head, let's do a CSS pop up.

After finished my bootcamp programming there is one thing that I have realized, that I got an acceptable understanding in CSS.

<!-- more -->

#### <i class="fa fa-html5"></i> The HTML file

{% highlight scss %}
<nav id="container">
 <ul class="nav_bar">
  <li id="settings"> <i class="fa fa-cogs"></i>    </li>
  <li id="home">     <i class="fa fa-home"></i>    </li>
  <li id="about">    <i class="fa fa-user"></i>    </li>
  <li id="archive">  <i class="fa fa-archive"></i> </li>
 </ul>
</nav>
{% endhighlight %} 


#### <i class="fa fa-css3"></i> The SCSS file

First we set this couple of mixins that will be useful to avoid rewritting the again and again

{% highlight scss %}
// Mixins and variables for all tooltips examples

@mixin set_arrow_tooltip{
 visibility: hidden;
 transition:visibility 0s ease-in 0.5s;
 content: '';
 color: transparent;
 position: absolute;
}

@mixin set_bubble_tooltip{
 visibility: hidden;
 transition:visibility 0s ease-in 0.5s;
 position: absolute;
 box-shadow: 0px 0px 3px;
 padding: 7px;
 border-radius: 11px;
}

@mixin show_tooltip{
 
 &:hover::before,
 &:hover::after {
	visibility: visible;
 }
}

{% endhighlight %} 


#### <i class="fa fa-css3"></i> SCSS example styling container



{% highlight scss %}

#container{
  
 position:relative;
 width: 350px;
 margin: 0 auto;

 .nav_bar{
   list-style: none;
	 display: flex;

	 li{
		margin-left: 40px;
      
    i{
      font-size: 34px;
      color: #ac4142
		}
	 }
	}
}

{% endhighlight %} 




#### <i class="fa fa-css3"></i> SCSS example for top tooltip

This first example is for the house icon

{% highlight scss %}

#home{
	
	&::before{
		
	@include set_arrow_tooltip();
		border-top: 10px solid rgba(25,25,25,0.3);
		border-right: 20px solid transparent;
		border-left: 20px solid transparent;
		top: -16px;
		margin-left: -4px;
	}

	&::after{

		@include set_bubble_tooltip();
		content: "Home";
		top: -60px;
		left: 62px;
		background-color: rgba(172,65,66,0.3);
	}
	
 @include show_tooltip();
}

{% endhighlight %} 


#### <i class="fa fa-css3"></i> SCSS example for bottom tooltip

This second example is for the user icon

{% highlight scss %}

#about{

  &::before{
	
		@include set_arrow_tooltip();
		border-bottom: 10px solid rgba(25,25,25,0.3);
		border-right: 20px solid transparent;
		border-left: 20px solid transparent;
		top: 42px;
    margin-left: -7px;
  }

  &::after{

	  @include set_bubble_tooltip();
	  content: "About";
	  top:  53px;
	  left: 130px;
	  background-color: rgba(172,65,66,0.3);
  }

  @include show_tooltip();
}

{% endhighlight %} 




### Live demo

> All my measures are hard coded so probably you will need to fix them.

<nav id="pop_up_demo">
 <ul class="nav_bar">
  <li id="settings"> <i class="fa fa-cogs"></i>    </li>
  <li id="home">     <i class="fa fa-home"></i>    </li>
	<li id="about">    <i class="fa fa-user"></i>    </li>
	<li id="archive">  <i class="fa fa-archive"></i> </li>
 </ul>
</nav>

