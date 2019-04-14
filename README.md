# md-tooltips

A simple Python markdown extension which will give you tooltips of definitions from a glossary. Works with `mkdocs` with `mkdocs-material`.

## How to use

Install from `pip`

```bash
$ pip install md-tooltips
```

Add to your `mkdocs.yml` under the `markdown_extensions` field.

```yaml
markdown_extensions:
     - mdtooltips
```

Create a file named `glossary.md` in the top level of the `docs` directory.

```bash
$ touch docs/glossary.md
```

Format each word as a subheader using double `##`.

```md
## Word

Here is the definition of a word

## Block

A block is a data structure...
```

In any of your markdown files in the `docs` directory, use the `@()` syntax to create a tooltip.

```md
An important term you should be familiar with is @(block).
```

Add css.

```css
/* Tool-tips */
*,
*:before,
*:after {
	-webkit-box-sizing: border-box;
	-moz-box-sizing:    border-box;
	box-sizing:         border-box;
}

/* Add this attribute to the element that needs a tooltip */
[data-tooltip] {
	position: relative;
	/* z-index: 2; */
	cursor: pointer;
	text-decoration: underline dotted;
}

/* Hide the tooltip content by default */
[data-tooltip]:before,
[data-tooltip]:after {
  visibility: hidden;
	-ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=0)";
	filter: progid:DXImageTransform.Microsoft.Alpha(Opacity=0);
	opacity: 0;
	pointer-events: none;
}

/* Position tooltip above the element */
[data-tooltip]:before {
	position: absolute;
  z-index: 2;
	top: 115%;
	left: 50%;
	margin-bottom: 5px;
	margin-left: -80px;
	padding: 7px;
	width: 160px;
	-webkit-border-radius: 3px;
	-moz-border-radius:    3px;
	border-radius:         3px;
	background-color: #000;
	background-color: hsla(0, 0%, 20%, 0.9);
	color: #fff;
	content: attr(data-tooltip);
	text-align: center;
	font-size: 14px;
	line-height: 1.2;
}

/* Triangle hack to make tooltip look like a speech bubble */
[data-tooltip]:after {
	position: absolute;
  z-index: 2;  
	top: 115%;
	left: 50%;
	margin-left: -5px;
	margin-top: -5px;
	width: 0;
	border-bottom: 5px solid #000;
	border-bottom: 5px solid hsla(0, 0%, 20%, 0.9);
	border-right: 5px solid transparent;
	border-left: 5px solid transparent;
	content: " ";
	font-size: 0;
	line-height: 0;
}

/* Show tooltip content on hover */
[data-tooltip]:hover:before,
[data-tooltip]:hover:after {
	visibility: visible;
	-ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=100)";
	filter: progid:DXImageTransform.Microsoft.Alpha(Opacity=100);
	opacity: 1;
}
```

It should work! If it does not please open an issue, as I hacked this together in a few hours for a project I work on and did not do any testing on other environments.

## License

Public domain.