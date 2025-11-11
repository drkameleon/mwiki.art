<h1 align="center">mwiki.art</h1>
<p align="center">
  <b>MediaWiki API wrapper for Arturo</b>
  <br><br>
  <img src="https://img.shields.io/github/license/drkameleon/mwiki.art?style=for-the-badge">
  <img src="https://img.shields.io/badge/language-Arturo-orange.svg?style=for-the-badge">
</p>

---

<!--ts-->

* [What does this package do?](#what-does-this-package-do)
* [How do I use it?](#how-do-i-use-it)
* [Type Reference](#type-reference)
   * [MW](#-mw)
   * [mwPage](#-mwpage)
   * [mwUser](#-mwuser)
   * [mwCategory](#-mwcategory)
* [License](#license)

<!--te-->

---

## What does this package do?

This package provides a complete MediaWiki API wrapper for Arturo, enabling seamless interaction with any MediaWiki-powered wiki (Wikipedia, Wikia, etc.). It handles authentication, page retrieval and editing, search, category browsing, and more - with automatic cookie management under the hood.

## How do I use it?

Simply `import` it and start interacting with your favorite wiki:

```red
import 'mwiki!

; Connect to a MediaWiki instance
wiki: to :MW ["https://rosettacode.org/w/api.php"]!

; Retrieve a page
page: wiki\page "Fibonacci sequence"
print page\content

; Search for pages
results: wiki\search.limit:5 "palindrome"
print.lines results

; Get category members
cat: wiki\category "Programming Tasks"
print [cat\name "has" cat\members "members"]

; Login and edit (requires credentials)
using wiki [
    if \login "username" "password" ->
        \editPage "Test Page" "Hello, wiki!" "Created test page"
]
```

## Type reference

### 🔹 MW

The main MediaWiki API client

#### Constructor

<pre>
<b>to :MW</b> [<ins>apiUrl</ins> <i>:string</i>]
</pre>

#### Fields

- `\apiUrl` - the MediaWiki API endpoint
- `\cookies` - session cookies (managed automatically)
- `\loggedIn` - authentication status

#### Methods

##### `login`

Authenticate with MediaWiki API.

<pre>
<b>login</b> <ins>username</ins> <i>:string</i> <ins>password</ins> <i>:string</i>
</pre>

###### Returns
- *:logical* - `true` if authentication successful, `false` otherwise

##### `page`

Retrieve page content by title.

<pre>
<b>page</b> <ins>title</ins> <i>:string</i>
</pre>

###### Returns
- *:mwPage* - page object containing title and content
- *:null* - page not found or request failure

##### `editPage`

Edit or create a wiki page.

<pre>
<b>editPage</b> <ins>title</ins> <i>:string</i> <ins>content</ins> <i>:string</i> <ins>summary</ins> <i>:string</i>
</pre>

###### Returns
- *:logical* - `true` if edit successful, `false` otherwise

##### `category`

Get all members of given category.

<pre>
<b>category</b> <ins>name</ins> <i>:string</i>
</pre>

###### Returns
- *:mwCategory* - category object containing name, size, and member list
- *:null* - request failure

##### `search`

Search wiki pages using given query.

<pre>
<b>search</b> <ins>query</ins> <i>:string</i>
</pre>

###### Attributes

| Option | Type | Description |
|----|----|----|
| limit | :integer | Limit search results (default: 10) |

###### Returns
- *:block* - array of page titles matching the search query

##### `user`

Get current user information.

<pre>
<b>user</b>
</pre>

###### Returns
- *:mwUser* - user object with information, groups, rights, and edit count
- *:null* - request failure

##### `recent`

Get recent wiki changes.

<pre>
<b>recent</b> <ins>limit</ins> <i>:integer :null</i>
</pre>

###### Returns
- *:block* - array of recent changes (default limit: 10)

### 🔹 mwPage

Represents a wiki page with its content

#### Constructor

<pre>
<b>to :mwPage</b> [<ins>title</ins> <i>:string</i>, <ins>content</ins> <i>:string</i>]
</pre>

#### Fields

- `\title` - page title
- `\content` - page wikitext content

### 🔹 mwUser

Represents a MediaWiki user

#### Constructor

<pre>
<b>to :mwUser</b> [<ins>details</ins> <i>:dictionary</i>]
</pre>

#### Fields

- `\details` - user information dictionary

### 🔹 mwCategory

Represents a wiki category with its members

#### Constructor

<pre>
<b>to :mwCategory</b> [<ins>name</ins> <i>:string</i>, <ins>members</ins> <i>:integer</i>]
</pre>

#### Fields

- `\name` - category name
- `\members` - number of members

> [!TIP]
> The wrapper automatically handles session cookies and CSRF tokens, so you don't need to worry about authentication state management! 😉

<hr/>

## License

MIT License

Copyright (c) 2025 Yanis Zafirópulos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
