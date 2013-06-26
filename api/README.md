# General API

## Rules:
All rules defined here are set *without exceptions*. That means there is not a single
scenario where these rules will be broken. Any time this isn't true, the results are
undefined and unsupported.

* Requests to the backend are always made via HTTP.
* Parameters passed to the backend are always passed via POST.
* Results from the backend are always returned via JSON.
* Issue fields are not defined outside of a schema.

This means:
* Results will never be (sanely) cached. This is correct.
* Javascript (the target frontend language) will always have great support.
* Other languages (such as Python, PHP, Perl, Ruby, Go...) will also have good support.
* Backends and frontends do not need to care about issue fields.

## Goals:
* Issue systems can be defined by a schema. No patches required.
* Write as little HTML as possible. Perfect world: less than 100 LOC of HTML.
* Absolutely _ZERO_ HTML in the backend.

## URIs:
A URI endpoint is defined as a directory that contains methods that can be invoked. By
way of example, an implementation that might be installed on a certain host in the root
directory might have scripts in a directory like this:

	http://bugs.example.com/api/

And the API for creating a new issue might be located here:

	http://bugs.example.com/api/create

These API endpoints can either exist as individual files that actually exist, or as
symlinks to a central program (or several such programs), or as a 404 catch-all that can
process requests to files in that directory that don't exist. That is of course
implementation-defined.

### Endpoints:
Nearly all API endpoints accept parameters. (All currently-defined endpoints do.) Any
parameters that are optional are marked as such. There are certain standard parameters
that are defined the same way for all endpoints where they are used:

* id
	* Refers to an issue ID.
* ids
	* Refers to a list or range (or combination thereof) of issue IDs.
* summary
	* Refers to a human-readable text summary of the changes being made.
* authtoken
	* Refers to a authentication identifier. This will be returned by the login endpoint.

Anywhere that these parameters are used as named, they will not be re-defined in each API
endpoint. 

#### login
Parameters:
* username
* password

Returns
* authtoken

In the future, this API will be extended to include a parameter named "hmac". This will be
a value salted with both the username and a salt value returned by "startlogin".

#### logout
Parameters:
* authtoken

Invalidates a certain authtoken.

#### startlogin
Parameters:
* username

Returns:
* salt

This endpoint is used to generate a string used for salting a user's password. See `login`.


#### create
Creates a new issue. Adds metadata "submitted by" the user identified by "authtoken".

Parameters:
* id
* summary
* description
* tags

#### update
Updates an existing issue. Adds metadata "updated by" the user identified by "authtoken".

Parameters:
* id
* summary
* [fields/attributes]

#### setstatus
* id
* summary
* state

#### attach
* id
* summary
* file
	* I honestly have no idea how this works outside of PHP, so this is subject to change.

