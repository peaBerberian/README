# Features of the HTML Pages

## Overview

The HTML pages generated by README should work with or without JavaScript
(library users reading documentation pages are full of geeks after all ;)). Yet
they have many supplementary features when JavaScript is enabled.

## Search

Search in README is achieved without involving a third-party thanks to the
[elastic lunr](http://elasticlunr.com/) library.

The idea is that an index is generated when your documentation is built, and
that index is fetched the first time you search on the generated HTML page.
Elastic lunr then searches through that index to provide matches that are then
display in the page.

Doing the search locally has the advantage of not having to rely on third
parties for your search. It also allows to have a much faster search experience
than if a server was requested for each search input.

Note however that elastic lunr is quite old and that some more recent local
search implementations exist that we're looking at today with the goal of
improving search accuracy.

## Soft navigation

Links to other documentation pages, as long as they concern the same category
(e.g. you're switching between links of the `API` category), are pre-loaded as
soon as they are hovered. Because documentation pages are very small in size,
doing this has the advantage of leading to an almost instantaneous page change
(as the request has often already ended before the link is actually clicked on).

The idea of pre-loading pages to then quasi-instantaneously update the page's
content on navigation through JavaScript is a recurrent trick called "soft
navigation".

Doing this also has the advantage of keeping the state of your page as is, even
when navigating between links. For example, page groups will remain opened even
when going to another documentation page.

## Responsiveness

This feature doesn't depend on JavaScript, but it should still be noted that
README HTML pages have two layouts depending on the available width.

Once small enough, several changes are made when compared to the full-width
layout:

- A "hamburger button" appears, toggling the display of a list of both the pages
  in the current category as well as the categories themselves. External links
  are also shown in that list.

- The header now only contains this hamburger button, your logo (if enabled),
  search (if enabled) and your project's version (if enabled).

- The table of contents (usually on the right side of the screen) is not visible
  anymore.

This was done to allow a smoother experience when reading your documentation in
a case where not a lot of horizontal space is available.