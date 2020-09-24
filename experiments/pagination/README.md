# Use of Paging for large sets

This experiment demonstrates why pagination might provide a better experience, and allows hands-on, immediate feedback
on pagination fields.

## Problem

At some point, the optimal query has been created, using all the performance enhancements, but still produces a lot of hits
and takes a long time to complete. Such a delay can be a bad experience for the user. 

## What the Experiment Does Not Teach You

This experiment tries to show the power of Pagination and the user of Querybuilder properties.

It does not try to teach how to:
 * create a beautiful web page
 * script perfect JS/JQuery usage
 * how to optimize a search for best performance

## Setup

Tools to Install:
* Maven (3.6.3 or more recent)

_NOTE_: An author instance running on port 4502 is required for this experiment.

We'll begin by building and installing the package included in this project.

1. Clone this Git repo to a local location
1. Using a console, go to the `aem-project` folder located in the project root (created from the AEM Project Archetype).
1. Build and install the package to your localhost's author instance by running `mvn -PautoInstallSinglePackage clean install`
1. Ensure that executes successfully.
1. To verify the installation, open the Pager page: http://localhost:4502/content/searchtester/us/en/experiments/pager.html

## Pager 

On the [page](http://localhost:4502/content/searchtester/us/en/experiments/pager.html) you will see 4 fields which
you may recognize as
[Querybuilder](http://localhost:4502/libs/cq/search/content/querydebug.html?_charset_=UTF-8&query=p.limit%3D-1%0D%0Apath%3D%2Fcontent%0D%0Ap.offset%3D0%0D%0Ap.guessTotal)
fields:

* limit: Page Size
* guessTotal: Whether to finish the full query to determine the total size (see the [Guess Total experiment](https://github.com/adobe/aem-search-experiments/tree/master/experiments/large-result-sets) for more information)
* offset: Where, in the result list, to start extracting hits to return 
* path: The base path where the search will begin

These fields will be updated, after clicking _Load Page_, if required in order to be ready for the next load.

You will see 2 button:

* Load Page: Use the fields' values to start a search of cq:Page items.
* Reset Fields: Reset all the values to their default values

You will see 2 textarea fields.

* Results: The list of all the hits already returned, the most recent hits appended to the bottom. Scrolling to the bottom of the list will trigger the next load (i.e. infinite scroll).
* Details: The details of the most recently executed search call including time duration, URL and the response.

## Test #1: 

1. Open the Pages page: http://localhost:4502/content/searchtester/us/en/experiments/pager.html
1. Examine the fields (note the _Path_ is pointing to the pager location, to limit the number of hits)
1. Click _Load Page_ button
1. Examine the text area fields
1. Note the _Details_, especially the Duration, how the URL matches the field values and the response metadata
1. Click the _Load Page_ again. See the _Result_ list grow, and see the _Details_ information refresh

## Test #2:

1. Open the Pages page: http://localhost:4502/content/searchtester/us/en/experiments/pager.html
1. Click the _Clear Fields_ button
1. Change the Path value to **"/content"**
1. Click _Load Page_
1. In _Details_, notice the Duration value
1. Change the _guessTotal_ value to **"true"**
1. Click _Load Page_
1. In _Details_, notice the Duration value is substantially larger (relatively) because the backend finished the search in order to find the exact total

## Test #3:

1. Open the Pages page: http://localhost:4502/content/searchtester/us/en/experiments/pager.html
1. It is up to you.
1. Change the _Limit_ to see different page sizes.  Notice what happens to the _Offset_ field
1. Change the _guessTotal_ values to "true", "false", -1, 0, 1 and 10000 and check the _Details_ of that search
1. Open your browser's network tab and see the network traffic when the call is executed


## Conclusion

To provide a better experience for the user, consider paging long results, instead of loading them all at once.
A practice of using pagination by default for UI based searches might be beneficial.  Require authors & developers to
prove pagination is not required, instead of wondering if it should be.

Examples of times when paging should be considered:

* the query has been optimized, but still takes a while
* when the item the user is most likely interested in will be near the "top" of the returned hit list
* when the search hits may grow over time, or will be substantially larger in a Production environment (i.e. testing on Dev & Stage might have small results, but Production could be much larger)
* when migrating large sets of data, perhaps from a legacy database, and testing shows search queries are taking much longer