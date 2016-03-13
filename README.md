# Track by

## Overview

Track by allows Angular to speed up our `ng-repeat`s massively - let's take a look how.

## Objectives

- Describe "track by" clause
- Write an ng-repeat that utilises "track by"

## What is track by?

Track by allows us to tell Angular what to identify unique items in our arrays, so Angular can tell when to remove it from the DOM correctly.

If we were to have an `ng-repeat` repeating items of news, Angular will display all of the news items on the page.

Later on, if we were to refresh the data (refresh the news), Angular will have to rebuild every DOM node in the repeat, even if two of the articles are the same.

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

Angular would then delete the original two DOM nodes, and then render three DOM nodes in its place - this is because it doesn't know what makes each news article unique.

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