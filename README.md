# FreeDoc — Scale down your HTML load


## Why FreeDoc

Have you ever tried to access a specific title or an attribute in a complex HTML tree?
Have you tried to keep your mark up inline and well formatted?
Have you maintained code like that?
What about maintaining readability?
Beyond that, what about writing comments in HTML?
If you have done all of this, have you ever been visited by a feeling that you are almost making
double the work for something that should be easier and lighter to read and write?

FreeDoc removes the burden of extensive dealing with HTML tags, with no change of skills required.
It attempts to mirror the advantages that Markdown and YAML have achieved, but applied to HTML itself

Look at the bottom of this page for a comparison between an HTML and FreeDoc document representing the same content.


## FreeDoc

Free document is easy to use and requires almost no additional learning or other skills.
You know HTML — it is enough to start using FreeDoc.
The format follows the HTML logic as close as possible, ridding you of the necessity of putting those closing tags

FreeDoc does not interpret the tags that you are providing in the mark–up.
Whether you are using React components with capital letters, Angular components with custom tags
and custom attributes, they are all transparent to FreeDoc

Python and YAML are good examples of languages where formatting gives meaning to the contents.
*Talk more about difficulty of maintaining formatting, and why it is easy in the case of YAML*

## Syntax

### Formatting

Think of FreeDoc as of HTML with the `<` and `>` removed, and without the need of closing tags.
The closing of tags happens automatically based on your indentation.
If you are familiar with Python, you know the life style

```
  div class="menu" style="width: 100%"
    a class="menu-button" (click)="logIn()"
      span
        Log In
    a class="menu-button" (click)="logOut()"
      span
        Log Out
```

By providing indentation in HTML, you have already given most of information that is needed to determine the nesting levels

### Void elements

Some HTML tags are "void", in that they do not require a closing tag, such as `br`, `img` or `input`.
FreeDoc by itself does not interpret these elements and will not attempt to make any guess whether these or any other tags are void.
Simply put a slash `/` at the end of the tag name to indicate that it should be void.
The following line
```
  input/ id="username" name="username" type="text"
```
translates into
```html
  <input id="username" name="username" type="text"/>
```

### Inline nesting

Although normally you would avoid doing this, sometimes you really want to fit the contents of a tag on the same line as the tag itself, *e.g.*
```html
  <span>Cart</span>
```
While in most cases it does decrease readability, in special rare cases it does make sence.
You can achieve that using `|` symbol
```
  span | Cart
```
You can even do this,
```
  a class="menu-button" | span | Cart
```
to be compared with
```html
  <a class="menu-button"><span>Cart</span></a>
```

What if you want an empty `<p></p>` tag?
You cannot do
```
  div class="container"
    p                           # this won't work
  div class="footer"
    ...
    ...
```
because in that case `p`, being the last element of last line of the "paragraph" will be considered text, not a tag.
The principle is simple — if an elements has contents, it's a tag, if it's empty — it's text. All you have to do is to put a vertical bar (`|`) at the end:
```
  div class="container | p |
```

If you happen to have to cram multiple items onto a single line, to the point that you will have sibling–tags on the same line, you can use the semicolon (`;`) as an "effective" closing tag,
to inform FreeDoc that the following tag is the sibling of the *previous* tag.
Think of the semicolon `;` as of the "closing bracket" for the vertical bar "|":
```
  a class="sign-up" | span class="material-icons" | account_circle; span | Sign Up
```
You can stack semicolons to go up a few levels,
```
  a class="sign-up" | span | Sign Up;;  a class="try-free" | span | Try for Free
```
if you really have to do this on the same line.
Still, compare this to
```html
  <a class="sign up"><span>Sign Up</span></a><a class="try-free"><span>Try for Free</span></a>
```

### Line continuation

### Script and verbatim tags



* Comments

* Escaped symbols

  + `|;#\`


## Tools

### Transpiler

```shell
$ freedoc --output-folder=dist/Messenger toolbar.free
```

or

```shell
$ freedoc --input-folder=src/app --output-folder=dist/Messenger
```

### HTML to FreeDoc converter


## A meaningful comparison between FreeDoc and HTML

Compare a real example,
```html
  <div>
    <div class="Polaris-Card">
      <ul class="Polaris-OptionList">
        <li>
          <p class="Polaris-OptionList__Title">Inventory Location</p>
          <ul class="Polaris-OptionList__Options" id="PolarisOptionList2-0">
            <li class="Polaris-OptionList-Option" tabindex="-1"><button id="0" type="button" class="Polaris-OptionList-Option__SingleSelectOption">Byward Market</button></li>
            <li class="Polaris-OptionList-Option" tabindex="-1"><button id="1" type="button" class="Polaris-OptionList-Option__SingleSelectOption">Centretown</button></li>
            <li class="Polaris-OptionList-Option" tabindex="-1"><button id="2" type="button" class="Polaris-OptionList-Option__SingleSelectOption">Hintonburg</button></li>
            <li class="Polaris-OptionList-Option" tabindex="-1"><button id="3" type="button" class="Polaris-OptionList-Option__SingleSelectOption">Westboro</button></li>
            <li class="Polaris-OptionList-Option" tabindex="-1"><button id="4" type="button" class="Polaris-OptionList-Option__SingleSelectOption">Downtown</button></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
```
to its FreeDoc counterpart
```
  div
    div class="Polaris-Card"
      ul class="Polaris-OptionList"
        li
          p class="Polaris-OptionList__Title" | Inventory Location
          ul class="Polaris-OptionList__Options" id="PolarisOptionList2-0"
            li class="Polaris-OptionList-Option" tabindex="-1" | button id="0" type="button" class="Polaris-OptionList-Option__SingleSelectOption" | Byward Market
            li class="Polaris-OptionList-Option" tabindex="-1" | button id="1" type="button" class="Polaris-OptionList-Option__SingleSelectOption" | Centretown
            li class="Polaris-OptionList-Option" tabindex="-1" | button id="2" type="button" class="Polaris-OptionList-Option__SingleSelectOption" | Hintonburg
            li class="Polaris-OptionList-Option" tabindex="-1" | button id="3" type="button" class="Polaris-OptionList-Option__SingleSelectOption" | Westboro
            li class="Polaris-OptionList-Option" tabindex="-1" | button id="4" type="button" class="Polaris-OptionList-Option__SingleSelectOption" | Downtown
```
