# Let’s take some &lt;m&gt;easures

The proposed inline `<m>` element represents a measurement of a physical attribute such as length, area, volume, mass, speed, temperature, etc.

``` html
<m unit="mi" value="20">twenty miles</m>
```

The purpose of the Web is to render information for us in a human-readable format. Making information also machine-readable will make it easily __convertible__ and thus - even more accessible for everyone.

"I hope we will use the Net to cross barriers and connect cultures." [Sir Tim Berners-Lee](http://edition.cnn.com/2005/TECH/internet/08/30/tim.berners.lee/index.html)


## Usefulness

Making measurements easier to convert on-page (automatically or on demand) through an extension or a built-in browser feature can eliminate interruptions of our browsing experience to convert units:

- for objects with physical dimensions like consumer products, tech hardware, furniture, etc.
- for recipes that contain cooking measurements such as cups/ounces/liters/grams
- on weather forecasts that display temperatures in °F or °C
- of the specifications of vehicles like dimensions, torque, acceleration, weight, fuel efficiency
- in drawing, CAD, and 3D modelling web applications that require physical dimension upon starting/exporting a project


But browsers aren’t the only consumer of content out there. We also have screen readers, search bots (such as Bing and Google), computational engines (like WolframAlpha), and personal assistants (Alexa, Cortana, Google Assistant, Siri) that can extract information and digest it for its users. Exposing more information to these bots and engines can only broaden their datasets of the real-world physical objects and thus be more useful to their users.


## What about Microformats?

A [measure microformat has been discussed in the past](https://microformats.org/wiki/measure-brainstorming) but the proposals either include a multitude of elements and attributes or severely limits the text content inside each element. Furthermore, the fact that a microformat did not gain popularity can not be an indicator of whether a similar HTML element would be successful. Microformats are heavier to write, include more attributes to configure (classes and other attributes) and are bound to use a longer-named tag than `<m>`.
The drawbacks of using the microformat proposal linked above are:
- it includes prices and currencies inside the specification, which are volatile units that change their relation to one another hundreds of times per day
- will require using non-semantic inline elements with a longer name, which is less readable than a dedicated `<m>` tag
- data is inside classes instead of specific attributes, targeting the unit or value as a hook is therefore more difficult and more error-prone
- the proposal requires the use of more than one element and more than two attributes to mark up the data
- the web author is strongly encouraged to use SI (metric) units instead of just using the units of his/her choice


## Why have `value` and `unit` attributes?

Currently no simple program can parse and understand physical measurements inside a casually phrased text because not all measurements consist of a simple number and a unit next to it.

The spirit of the Web isn't about forcing web authors to write in a specific machine-readable format with certain units (e.g. "the car's power is 84 kilowatts"), rather it encourages authors to phrase their text content as they will with the _option_ to mark it up for hooks, semantics, or machine readability.

Here are some examples where hard-to-machine-parse measurements can be marked up and become machine-readable without constraints to the text that web authors use:
- `<m unit="m" value="10">10 m</m>` - ambiguous abbreviations
- `<m unit="oz" value="2">two ounces</m>` - number words are sometimes used instead of digits
- `<m unit="kg" value="4">4 kilos</m>` - shortened or slang words for units
- `<m unit="gal" value="0.5">half a gallon</m>` - multiple words
- `<m unit="lb" value="0.95">weights just under a pound</m>` - being imprecise in the text
- `<m unit="l" value="96">quatre-vingt seize litres</m>` - units and values in a different language
- `<m unit="in" value="71">5′ 11″</m>` - feet & inches often use quotes, primes, apostrophes, carets or similar symbols - `′'‘’` & `″"“”`

No regular expression or program can be written to translate and understand all the above measurements just from the textual information, but as demonstrated, all of them can be marked up so that they can be understood unambiguously by machines and people.

Healthy reminder that the existing `<a>`, `<abbr>`, and `<time>` also expect information for one thing provided in two formats - user-facing text content inside the tag plus an attribute value.

The `value` attribute can accept any positive or negative number, using a dot for a decimal separator.

The attribute `unit` will expect a case-sensitive string that should unambiguously define different units across the metric, imperial, and US customary unit systems.


<details>
    <summary>Which standard to use?</summary>

Here is an example list of accepted `unit` abbreviations that can be easily extended in the future:

| Type of measurement | Metric | Imperial & US Customary |
| --------------- | ---------------- | ----------- |
| Length          | <abbr title="centimeter">cm</abbr>, <abbr title="meter">m</abbr>, <abbr title="kilometer">km</abbr>        | <abbr title="inch">in</abbr>, <abbr title="foot">ft</abbr>, <abbr title="yard">yd</abbr>, <abbr title="mile">mi</abbr> |
| Area            | <abbr title="square centimeter">cm2</abbr>, <abbr title="square meter">m2</abbr>, <abbr title="square kilometer">km2</abbr>, <abbr title="hectare">ha</abbr> | <abbr title="square inch">sqin</abbr>, <abbr title="square foot">sqft</abbr>, <abbr title="square mile">sqmi</abbr>, <abbr title="acre">acre</abbr> |
| Volume          | <abbr title="cubic centimeter">cm3</abbr>, <abbr title="cubic meter">m3</abbr>, <abbr title="liter">l</abbr>       | <abbr title="cubic inch">cuin</abbr>, <abbr title="cubic foot">cuft</abbr>, <abbr title="UK gallon">UKgal</abbr> <abbr title="USgallon">USgal</abbr> |
| Mass            | <abbr title="milligram">mg</abbr>, <abbr title="gram">g</abbr>, <abbr title="kilogram">kg</abbr>, <abbr title="tonne">t</abbr>        | <abbr title="grain">gr</abbr>, <abbr title="ounce">oz</abbr>, <abbr title="pound">lb</abbr>, <abbr title="stone">st</abbr> |
| Density         | <abbr title="kilogram per cubic meter">kg/m3</abbr> | <abbr title="pound per cubic foot">lb/ft3</abbr> |
| Torque          | <abbr title="newton meter">Nm</abbr> | <abbr title="pound-foot">lb.ft</abbr> |
| Speed           | <abbr title="kilometer per hour">km/h</abbr>, <abbr title="meter per second">m/s</abbr> | <abbr title="mile per hour">mph</abbr>, <abbr title="foot per second">ft/s</abbr> |
| Fuel efficiency | <abbr title="liters per 100 km">L/100km</abbr> | <abbr title="miles per gallon">mpg</abbr> |
| Temperature     | <abbr title="degree Celsius">C</abbr> | <abbr title="degree Fahrenheit">F</abbr> |


The options I found for a standard reference to be used for the `unit` attribute basically look like that:
- The major international standards that list measurement units and propose abbreviations for them are [ISO/IEC 80000](https://www.iso.org/standard/30669.html) - behind a paywall and focused on Metric units
- [IEEE Std 260.1](https://ieeexplore.ieee.org/document/1337729) that defines "Standard Letter Symbols for Units of Measurement (SI Customary Inch-Pound Units, and Certain Other Units)" but is behind a paywall
- The [UCUM's case-sensitive units](https://ucum.org/ucum.html) which include all units listed in ISO 1000, ISO 2955-1983, ANSI X3.50-1986, HL7 and ENV 12435, and is designed primarily for machine-to-machine communication, many unit codes are not very user-friendly
- [Wikipedia's own "unit-codes"](https://en.wikipedia.org/wiki/Template:Convert/list_of_units) that are designed to be unambiguous and easy-to-use for conversion purposes, they include the most popular units and are made to be easy for human use. Licensed by [Creative Commons Attributions ShareAlike 3.0](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License), which is [compatible](https://wiki.creativecommons.org/wiki/Wiki/cc_license_compatibility) with the "Creative Commons Attribution 4.0 International" license of [WHATWG's HTML repository](https://github.com/whatwg/html/blob/master/LICENSE).

</details>


## User Perspective
"The essential property of the World Wide Web is its universality." [Sir Tim Berners-Lee](https://www.researchgate.net/publication/225070375_The_Semantic_Web_A_New_Form_of_Web_Content_That_is_Meaningful_to_Computers_Will_Unleash_a_Revolution_of_New_Possibilities)

If implemented, it will enable the creation of standardized site scripts, user scripts, browser extensions, and browser features that will easily convert measurements between metric, imperial, and US customary units without the need for users to resort to unit converters.

Current browser extensions that convert between units are typically either convertor popups, or selection/whole-page parsers, neither of which is both accurate and fast-to-use.

Browsers already offer us translations of a whole web page (Chrome and Safari), this is a type of a localized personalization of the content for the user, based on his declared language preferences. We don't need a great stretch of the imagination to envision a "translator" that localizes units for us, working in a similar manner.

Being able to quickly convert measurements without interrupting the user flow will save both time and bandwidth for all who this feature.

The demand for unit conversion is apparently quite strong - search queries for unit conversion are so popular that Google [added a unit converter UI calculator](https://news.softpedia.com/news/Google-Builds-a-Unit-Converter-in-the-Search-Page-281183.shtml) to their search results more than 8 years ago, but in fact the search engine has been [answering conversion queries for at least 16 years](https://arxiv.org/abs/physics/0411198) - around the time Google became a public company (and before Gmail and Google Translate even existed).


## Conversion

Converting units is a task typically delegated to users, who usually interrupt their reading journey by opening another tool, popup, or search engine to convert units. This is clearly inefficient; however, the currently available alternatives are often not ideal or possible.

With `<m>`, web authors will have one more measurement declaration method to pick from:

| HTML                                   | Conversion effort by | Converted unit availability     |
|----------------------------------------|----------------------|---------------------------------|
| `61 miles`                             | users                | manually from 3rd party tool    |
| `61 miles (100 km) `                   | author               | always visible                  |
| `{{convert\|61\|mi\|km\|abbr=on}}` <br>resulting in `61 miles (100 km)` | MediaWiki back end | always visible |
| `<m unit="mi" value="61">61 miles</m>` | JS on the front end  | available inline on-demand or automatically |

As demonstrated by this table, to avoid the human effort either the 3rd or 4th method should be used for conversion. A new standardized HTML element would be a solution that is always available and back-end agnostic.

Additionally, when using the `<m>` element the developer can announce whether the measurement is suitable for conversion with the optional attribute `convert`:
```
convert="never|auto|eager"
```

A `never` option would be suitable for measurements with de-facto standard units such as nanometers for CPU designs and inches for screen diagonals or car tires. Probably no person will ever need to know that a 5nm CPU is 0.00000019685 inches.

The `auto` option is the default value and is the same as omitting the attribute. It will be up to the script/browser/user to decide whether to convert these automatically or on-demand.

The `eager` option is for units that will be more understandable if converted to the users' preferred ones. It signals that the value is appropriate for automatic conversion if a user preference/consent has been provided.

For this conversion system to work in a user-friendly way it also needs browser/OS unit option (metric, UK imperial, US imperial, etc) that users can set for their preferred units. This preference can be placed in one of several places:
- in the [Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl) JS object
- in the [Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) user agent interface which already provides read-only access [to the user's browser languages](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/languages)
- any other place that offers access to user preferences in the web platform
- a media feature similar to [prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) and [prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) that are accessible through both CSS and JavaScript

Just a few years ago the [IndieUI: User Context](https://www.w3.org/TR/indie-ui-context/) W3C document proposed the ability for a "set of preferences that users can choose to expose to web applications", the listed examples include assistive tech used, preferred typography style, and even a desired subtitle background color. No mention of a preferred "unit language" though.


## A richer, more useful HTML
The more recent structuring block-level HTML elements such as `<main>`, `<article>`, `<aside>`, `<header>`, `<footer>`, `<nav>`, and `<hgroup>` have brought significant benefits for developers, but a huge part of the web is still a collection of blocks of plain text.

The web needs also more inline-level semantics, currently a limited number of such elements are available to authors to mark up their content. The most recent HTML usage data I could find shows a [depressingly poor and generic usage of inline elements](https://www.advancedwebranking.com/html/#inline-text-semantics).

The proposed `<m>` element will not only bring the aforementioned benefits. Due to its attributes having an expected and clear structure they will become a set of hooks for CSS and JS that will be used by developers in many creative ways we cannot even envision.

A [&lt;dfn&gt; element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dfn) might serve to identify the physical entity measured if placed inside the same `<p>` or `<section>` as the `<m>` element. Alternatively, an [existing ARIA role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques#relationship_attributes) might be used such as "labeledby" or "describedby".


## Can `<m>` become widespread?
Widely used inline marked data might seem hard to achieve in our vast web but is actually possible as demonstrated by the success of [Schema.org](https://schema.org/docs/schemas.html).

The unit problem has been "solved" by the Wikimedia Foundation by listing units in multiple formats - the length of the Great Wall of China is listed as "21,196 km (13,171 mi)" which is written in their back end as `{{convert|21196|km|mi|abbr=on}}`. This convert tag is reportedly used on over a million pages on Wikipedia. Wikimedia Foundation can theoretically update their code to output the same content but wrap the unit in a `<m>` tag.

Stores, wikis, CMSs and other sites that use templates/views might also be able to retroactively update lots of its content.
