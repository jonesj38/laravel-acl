# Blog Post 2 - Kodeine/Laravel-ACL - by jonesj38

[![Laravel](https://img.shields.io/badge/Laravel-~5.0-orange.svg?style=flat-square)](http://laravel.com)
[![Source](http://img.shields.io/badge/source-kodeine/laravel--acl-blue.svg?style=flat-square)](https://github.com/kodeine/laravel-acl/)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](https://tldrlegal.com/license/mit-license)

Laravel ACL adds role based permissions to built in Auth System of Laravel 5. ACL middleware protects routes and crud controller methods.

# Blog Post 2 [Artifact 1] Pull Request to Kodeine/Laravel-ACL for Beginner Tutorial - by jonesj38

For the first artifact of my second blog post I decided to issue a pull request to Kodeine to see if he/she would accept the noob/beginner tutorial that I
wrote for my initial blog post. The tutorial aimed to provide more in-depth and easy to digest instructions for installing and using Kodeine/Laravel-ACL lightweight
permissions, including a workaround for the blade directives provided with Kodeine/Laravel-ACL which for some reason don't seem to work properly "out of the box".
I issued the pull request on April 4, 2016 and as of April 11, 2016 I have not received a response from Kodeine.

![Image of Tutorial Pull Rquest]
(https://github.com/jonesj38/laravel-acl/blob/blogs/tutorialPR.png?raw=true)


# Blog Post 2 [Artifact 2] Trick/Tip When Using Kodeine/Laravel-ACL Blade Directives

For the second artifact of my second blog post I initially wanted to fix the blade directive issues, but I was unable to figure out the problem before my second
blog post is due. Instead, I want share an interesting trick/tip involving Kodeine/Laravel-ACL blade directives that I actually incorporated into the group 
project I worked on this semester. I discovered that wrapping only the initial part of a link in a permission, e.g.

```html
<td class="table-success" id="success-measures"> @role('bplead')<a data-pk="{{ $action->id }}" href="#" class="editable editable-click editable-disabled">@endrole {{ $action->success }}</a></td>
```

The natural tendency is to wrap the entire link inside of a permission like so:

```html
<td class="table-success" id="success-measures"> @role('bplead')<a data-pk="{{ $action->id }}" href="#" class="editable editable-click editable-disabled"> {{ $action->success }}</a></td>@endrole
```

and although this allows us to view and edit the text when logged in as a bplead, in this case we are logged in as user Vicky:

![Image 1 of artifact 2]
(https://github.com/jonesj38/laravel-acl/blob/blogs/tutorialPR.png?raw=true)


This hides the text behind the bplead permission and renders it invisible to non-bplead users:

![Image 2 of artifact 2]
(https://github.com/jonesj38/laravel-acl/blob/blogs/tutorialPR.png?raw=true)

you can give a link a permission while at the same time allowing the text and the html to stay visible to non-permitted users and 
continue to work properly, e.g.:

```html
<td class="table-success" id="success-measures"> @role('bplead')<a data-pk="{{ $action->id }}" href="#" class="editable editable-click editable-disabled">@endrole {{ $action->success }}</a></td>
```

and if you look at the following images, when we're logged in as Vicky, which is our business plan lead, it allows us to see and edit the success measure.


![Image 3 of artifact 2]
(https://github.com/jonesj38/laravel-acl/blob/blogs/tutorialPR.png?raw=true)


When we're logged out and simply viewing the business plan as a read-only user the success measure is no longer editable but it is still
visible and this is what we want.

![Image 4 of artifact 2]
(https://github.com/jonesj38/laravel-acl/blob/blogs/tutorialPR.png?raw=true)


The reason why this works has to do with the way Kodeine/Laravel-ACL blade directives work; they add a permission(s) to the code around which
they are wrapped after the html has been compiled. In other words, the code within the blade directives is still part of the rest of the page and 
acts accordingly, but when permissions are added, it will act on that specific part of the code after it has been compiled. This can be useful 
when trying to add functionality to some bit of code, like the link example above, while simultaneous allowing it to stay visible to non-permitted users.

This is just one example of the powerful malleability that Kodeine/Laravel-ACL blade directives have.

Cheers!
and happy coding
jonesj38