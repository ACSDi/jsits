General API
===========

Rules:
------
* Requests to the backend are always made via HTTP. No exceptions.
* Parameters passed to the backend are always passed via POST. No exceptions.
* Results from the backend are always returned via JSON. No exceptions.

This means:
* Results will never be (sanely) cached. This is correct.
* Javascript (the target frontend language) will always have great support.
* Other languages (such as Python, PHP, Perl, Ruby, Go...) will also have good support.

Goals:
-----------------
* Write as little HTML as possible. Perfect world: less than 100 LOC of HTML.
* Absolutely _ZERO_ HTML in the backend.

URIs:
----------------
A URI endpoint is defined as a directory that contains methods that can be invoked. By
way of example, an implementation that might be installed on a certain host in the root
directory might have scripts in a directory like this:

	http://bugs.example.com/api/

And the API for creating a new issue might be located here:

	http://bugs.example.com/api/create

