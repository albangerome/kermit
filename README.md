Kermit
======

Introduction:
-------------

If you have some experience with web analytics implementation there will be 2 types of tracking requirements. First you will need to track page views, second you will need to track interactions with page elmements. Kermit is a group of Javascript functions that will help you with the 2nd type of tracking requirements, i.e. page element interactions.

Whenever a visitor interacts with a page element a multitude of Javascript events will fire. So what do I mean by _page element interactions_ exactly? I mean clicks on buttons, drop-down selections, text fields. 3 Javascript events are of particular interest but only one Javascript event will be relevant. We will have 3 categories of page elements based on the followin Javascript events

* click
* change
* blur

For example the only Javascript event that will matter for a button is a _click_ event. All other Javascript events have little to no value for us except the click event when the page element is a button. In the case of a drop-down however the _click_ event will be incorrect as it would fire twice, once when you open the drop-down and a second time when you actually select an option. When dealing with drop-downs you will want the _change_ Javascript event. This leaves the text fields and here the only event of interest is the _blur_ event. More on this below.

Marking up the page elements:
-----------------------------

The first thing consists of adding a custom HTML attribute to the page elements you need to track. The HTML standards recommend using attributes starting with _data-_. I have picked _data-analytics-interaction-description_, Fellows of the Royal Academy of Poetry there's a contact link somewhere on the page. You can change the name of HTML attribute in the config section. More on this later.

Now the value of the _data-analytics-interaction-description_ HTML attribute will be passed to your web analytics tool. Please make sure you pass a unique value as it will help you do a proper breakdown of all in the interactions tracked across your website.

Automatically handle the rest:
------------------------------

Now kermit will scan through the document for tags containing the _data-analytics-interaction-description_ HTML attribute. It will find the tag name and if necessary the _type_ and _href_ attributes. For example an _input_ tag with _type="radio" and an _input_ with _type="text"_ will be in 2 different categories (click, change, blur). Therefore the tag name is not enough. Then kermit will determine the category automatically and attach the appropriate event listener to the element. kermit provides a cross-browser event listener.

For links that will result in loading a completely new page there could be a racing condition where the new page is trying to load and the analytics tracking request is trying to fire. Which one will happen first can be random so kermit applies a 500 milliseconds delay to the new page loading to leave enough time for the tracking request to be sent out. This delay does not apply to any other interaction and this ensures more accurate analytics data. The delay duration can also be edited in the config section.

Configuring kermit:
-------------------

I have already mentioned 2 settings above which you can edit in the config section

* The name of the HTML element attribute that will contain the description of the interaction for your web analytics reports
* The delay after which a new page will display after the visitor clicked on a link

There is also another item which I have mentioned briefly, the list of elements and the relevant HTML attribute which will be used to determine which category of the interaction belongs to:

_click_ category
* input[button]
* input[submit]
* input[checkbox]
* button
* a[href]
* area[href]

_change_ category
* select[]
* input[radio]

_blur_ category
* input[text]
* input[color]
* input[date]
* input[datetime]
* input[datetime-local]
* input[email]
* input[month]
* input[number]
* input[range]
* input[search]
* input[tel]
* input[time]
* input[url]
* input[week]
* textarea

How to use the demo files:
--------------------------

Copy all 3 files and open your browser with the Javascript console opened. Start interacting with the page elements.

Alban Gérôme
22 August 2016

Follow me on Twitter: @albangerome