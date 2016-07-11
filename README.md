# Track by

## Overview

Track by allows Angular to speed up our `ng-repeat`s massively - let's take a look how.

## Objectives

- Describe "track by" clause
- Write an ng-repeat that utilises "track by"

## Performance

Now that we've started to build our Angular applications, we can start to think about scaling them. As we start to display more data and allow complex user interactions with that data, our application can become slow, much like if we build a one-way street and try and drive 5,000 cars in both directions. There are a few neat tricks we can use to improve performance.  Each performance enhancement we use in Angular is like adding an extra road, allowing things to become much quicker.

## What is track by?

Track by allows us to identify JavaScript objects in an `ng-repeat` list so that Angular won't `$destroy` or re-create DOM nodes unnecessarily.

For example, if we were to have an `ng-repeat` repeating the news, Angular will display all of the news items on the page.

Later on, if we were to refresh the data (refresh the news), Angular will have to rebuild every DOM node in the repeat, even if two of the articles are the same. Any change in the array will result in a rebuild of the DOM - Angular has no way of telling what items in the new array are the same in the last array.

To prevent this, we can use `track by` in our `ng-repeat`s. This tells Angular what to use to identify the news article.

If our data structure looks like this:

```js
var newsItems = [{
	id: 2342339,
	title: 'Apple customer goes to the top for iPhone battery answer',
	timestamp: 1457697486000
}, {
	id: 2342320,
	title: 'Android N brings split-screen multitasking apps',
	timestamp: 1457609266000
}];
```

Here we've got two items of news. Angular will then display these on the page. If we were then to refresh the news, and a new item of news comes in:

```js
var newsItems = [{
	id: 2342342,
	title: 'Computer wins series against Go master',
	timestamp: 1457773283000
}, {
	id: 2342339,
	title: 'Apple customer goes to the top for iPhone battery answer',
	timestamp: 1457697486000
}, {
	id: 2342320,
	title: 'Android N brings split-screen multitasking apps',
	timestamp: 1457609266000
}];
```

Angular would then delete the original two DOM nodes, and then render three DOM nodes in its place - this is because it doesn't know what makes each news article uniques (it can't tell what has changed, so assumes it all has).

## Using track by

As you can see, all of our news articles have unique IDs associated with these. Let's let Angular know about these!

This:

```
<ul class="news">
	<li ng-repeat="item in ctrl.news">
		{{ item.title }}
	</li>
</ul>
```

Will turn into this:

```
<ul class="news">
	<li ng-repeat="item in ctrl.news track by item.id">
		{{ item.title }}
	</li>
</ul>
```

Letting Angular know to track by the `id` property on the news articles.

If we go back to when we update the data - instead of removing two DOM nodes and creating three, Angular just creates one new DOM node at the top of the list - awesome!

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/angular-track-by-readme'>Angular Track By </a> on Learn.co and start learning to code for free.</p>
