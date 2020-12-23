# Let’s take some &lt;m&gt;easures

The proposed inline `<m>` element represents a measurement of a physical-world property such as dimension, mass, speed, temperature, etc.

``` html
<m unit="mi" value="60">sixty miles</m>
```

The purpose of the Web is to render information for us in a human-readable format. Making information also machine-readable will make it easily convertible and thus - even more accessible.

"I hope we will use the Net to cross barriers and connect cultures." [Sir Tim Berners-Lee](http://edition.cnn.com/2005/TECH/internet/08/30/tim.berners.lee/index.html)

## Why mark up measurements?

Making measurements easier to convert on-page (automatically or on demand) through an extension or a built-in browser feature will has the potential to eliminate pauses in our browsing experience to do conversions:

- for objects with physical dimensions in inches or centimeters, such as consumer products, tech hardware, or furniture
- for recipes that contain cooking measurements in units like cups/ounces/liters/grams
- on weather forecasts that assume a default temperature unit - °F or °C
- of the specifications of a new car model such as dimensions, torque, acceleration, weight, dimensions, boot volume, fuel efficiency
- in drawing, CAD, and photo editing web applications that pick a wrong default length unit for you


But browsers aren’t the only consumer of content out there. We also have screen readers, search bots (such as Bing and Google), computational engines (like WolframAlpha), and personal assistants (Alexa, Cortana, Google Assistant, Siri) that can extract information and digest it for its users. Exposing more information to these bots and engines can only broaden their datasets of the real-world physical objects and thus be more useful to their users.



## Why have `value` and `unit` attributes?

A [measure microformat has been discussed in the past](http://microformats.org/wiki/measure-brainstorming) but the proposals either include a multitude of elements and attributes or severely limits the text content inside each element. Furthermore, the fact that a microformat did not gain popularity can not be an indicator of wether a similar HTML element would be successful. Microformats are heavier to write, include more attributes to configure (classes and other attributes) and are bound to use a longer-named tag than `<m>`.

If we are to preserve the freedom of a web author to phrase one's content freely, then the only two options to convert these are to:
- paste the information into a search engine like so "{input unit} in {desired unit}" but even then, the engine might not understand the context/language/abbreviation
- provide information in a simple machine-readable format

The latter option is of course superior, but no simple program can parse and understand physical measurements inside a given text, especially measurements that don't consist of a simple number and a unit.

Here are just some cases where a hard-to-machine-parse textual measurement can be marked up:
- `<m unit="m" value="10">10 m</m>` - ambiguous abbreviations
- `<m unit="oz" value="2">two ounces</m>` - number words are sometimes used instead of digits
- `<m unit="kg" value="4">4 kilos</m>` - shortened or slang words for the unit
- `<m unit="gal" value="0.5">half a gallon</m>` - multiple words
- `<m unit="lb" value="0.95">weights just under a pound</m>` - being imprecise in the text
- `<m unit="l" value="96">quatre-vingt seize litres</m>` - units and values in a different language
- `<m unit="in" value="71">5′ 11″</m>` - for feet & inches, people often use quotes, primes, apostrophes, carets or similar symbols - `′'‘’` & `″"“”`

Healthy reminder that there already are HTML tags that expect information for one thing in two formats - user-facing text content inside the tag plus an attribute value. These are `<time>`, `<a>`, and `<abbr>`.

The `value` attribute can accept any positive or negative number, using a dot for a decimal separator.

The attribute `unit` will expect a case-sensitive string that should unambiguously define different units across the Metric, Imperial, and US customary unit systems.


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
- The major international standards that list measurement units and propose abbreviations for them are [ISO/IEC 80000](https://www.iso.org/standard/30669.html) - behind a paywall and only defines with Metric units
- [IEEE Std 260.1](https://ieeexplore.ieee.org/document/1337729) that defines "Standard Letter Symbols for Units of Measurement (SI Customary Inch-Pound Units, and Certain Other Units)" but is behind a paywall
- The [UCUM's case-sensitive units](https://ucum.org/ucum.html) which include all units listed in ISO 1000, ISO 2955-1983, ANSI X3.50-1986, HL7 and ENV 12435, and is designed primarily for machine-to-machine communitaction, but many codes are not very user-friendly
- [Wikipedia's own "unit-codes"](https://en.wikipedia.org/wiki/Template:Convert/list_of_units) that are designed to be unambiguous and easy-to-use for conversion purposes, they include the most popular units and are made to be easy for human use. Licensed by [Creative Commons Attributions ShareAlike 3.0](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License), which is [compatible](https://wiki.creativecommons.org/wiki/Wiki/cc_license_compatibility) with the "Creative Commons Attribution 4.0 International" license of [WHATWG's HTML repository](https://github.com/whatwg/html/blob/master/LICENSE).

</details>

## User Perspective
"The essential property of the World Wide Web is its universality." [Sir Tim Berners-Lee](https://www.researchgate.net/publication/225070375_The_Semantic_Web_A_New_Form_of_Web_Content_That_is_Meaningful_to_Computers_Will_Unleash_a_Revolution_of_New_Possibilities)

If implemented, it will enable browser extensions (or browsers themselves) to easily convert measurements between metric and imperial units without the need for users to resort to unit converters.

Current browser extensions that convert between units are typically either convertor popups, or selection/whole-page parsers, neither of which is both accurate and fast-to-use.

Browsers already offer us translations of a whole web page (Chrome and Safari), this is a type of a localized personalization of the content for the user, based on his declared language preferences.
We don't need a great stretch of the imagination to envision a "translator" that localizes units for us, working in a similar manner.
Being able to quickly convert measurements without interrupting the user flow will save both time and bandwidth for all who this feature.

The demand for unit conversion is apprently quite strong - search queries for unit conversion are so popular that Google [added a unit converter UI calculator](https://news.softpedia.com/news/Google-Builds-a-Unit-Converter-in-the-Search-Page-281183.shtml) to their search results more than 8 years ago, but in fact the search engine has been [answering conversion queries for at least 16 years](https://arxiv.org/abs/physics/0411198) - around the time Google became a public company (and before Gmail and Google Translate even existed).


## Conversion

The current state of unit leaves a web author can:
- write "61 miles" and leave every single user to try and convert it by himself/herself
- write "61 miles (100 km)" but spend additional time to figure out the conversion

A third option - writing "&lt;m unit='mi' value='61' &gt;61 miles&lt;/m&gt;" will leave the conversion to the software and is more efficient time-wise (can save many human-hours of wasted effort).

Additionally, the developer can announce whether the measurement is suitable for conversion with the optional attribute `convert`:
```
convert="never|auto|eager"
```

A `never` option would be suitable for measurements with established/settled units such as nanometers for CPU designs. 5nm is okay, 0.00000019685 inches isn't user-friendly even for people accustomed imperial unit. Another unit that is a de-facto international standard is the inch when used for screen diagonals and car tires.

The `auto` option is the default value and is the same as omitting the attribute. It will be up to the browser/user to decide whether to convert these.

The `eager` option is for values that will be certainly more understandable if converted to the users' preference. It signals that the value is appropriate for automatic conversion if a user preference/consent has been provided. An example would be a weather forecast website which would automatically display temperatures in a user's preferred unit (imagine building a weather website without the need to add options in the interface for °F/°C units).

For this conversion system to work in a user-friendly way it also needs browser/OS unit option (metric, UK imperial, US imperial, etc) that users can set for their preferred units. This preference can be placed in one of several places:
- in the [Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl) JS object
- in the [Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) user agent interface which already provides read-only access [to the user's browser languages](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/languages)
- any other place that offers access to user perferences in the web platform
- a media future similar to [prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) and [prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) that are accessible through both CSS and JavaScript

Just a few years ago the [IndieUI: User Context](https://www.w3.org/TR/indie-ui-context/) W3C document proposed the ability for a "set of preferences that users can choose to expose to web applications", the listed examples include assistive tech used, preferred typography style, subtitle language, and even a desired subtitle background color. Adding a "unit language" preference here would be a nice fit that helps accessibility.



## A richer, more useful HTML
The more recent structuring block-level HTML elements such as `<main>`, `<article>`, `<aside>`, `<header>`, `<footer>`, `<nav>`, and `<hgroup>` have brought significant benefits for developers, but lots of content on the web is still a collection of blocks of plain text.

The web also needs more inline-level semantics, currently a limited number of such elements are available to authors to mark up significant parts of their content. The most recent HTML usage data I could find shows a [depressingly poor and generic usage of inline elements](https://www.advancedwebranking.com/html/#inline-text-semantics).

The proposed `<m>` element will not only bring the aforementioned benefits. Due to its attributes having an expected and clear structure they will become a set of hooks for CSS and JS that will be used by developers in many creative ways we cannot even envision.

A [&lt;dfn&gt; element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dfn) might serve to identify the physical entity measured if placed inside the same `<p>` or `<section>` as the `<m>` element.


## Can `<m>` become widespread?
Widely used inline marked data might seem hard to achieve in our vast web but is actually possible as demonstrated by the success of [Schema.org](https://schema.org/docs/schemas.html).

The unit problem has been "solved" by Wikimedia Foundation by listing units in multiple formats - the length of the Great Wall of China is listed as "21,196 km (13,171 mi)" which is written in their back end as `{{convert|21196|km|mi|abbr=on}}`. This convert tag is reportedly used on over a million pages on Wikipedia. They can theoretically update their code to output the same content but wrap at least one of the units in a `<m>` tag. Stores, wikis, and other sites that use templates/views might also be able to retroactively update lots of its content.
