# Style Calculations

After fetching the file the browser starts with the Style calculations.

## HTML parsing algorithm

### Conversion

The browser reads raw ```Bytes``` and converts them into ```Characters```


### Tokenizing

The browser converts the string of characters into distinct tokens. Each token has a special meaning

```StartTag:html StartTag:head .... EndTag:head EndTag:html```

### Lexing

The browser converts tokens into nodes.

```html``` ```head```

### Building the DOM tree

Once the tokens are converted into nodes the browser builds the DOM with the parent child relationship.

## DOM is Not Enough

If you want to know what the page looks like a DOM is not enough, its CSS of course.

Even without a stylesheet the browser has a default one which will make headers larger than others etc.

## Parse CSS

The method to parse CSS is very similar.

1. Bytes become Characters
2. Characters become Tokens
3. Tokens become Nodes
4. Linked into a tree structure CSS Object Model (CSSOM)

## The Render Tree

Will only have objects on it that can displayed. If for example display: none is a property. It will not be on the Render Tree.