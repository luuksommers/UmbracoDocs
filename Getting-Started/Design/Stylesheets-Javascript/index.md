---
meta.Title: "Working with stylesheets and JavaScript in Umbraco"
meta.Description: "Information on working with stylesheets and JavaScript in Umbraco, including bundling & minification"
versionFrom: 7.0.0
---

# Working with stylesheets and JavaScript

## Stylesheets in the Backoffice

You can create and edit stylesheets in the Stylesheets folder in the Settings section of the Backoffice.

![Creating a new stylesheet](images/1-creating-stylesheet.png)

In the Create menu, there are several options available:

* Stylesheet file (for use in templates/views)
* Rich Text Editor stylesheet file (for use in [Rich Text Editor](../../Backoffice/Property-Editors/Built-in-Property-Editors/Rich-Text-Editor/))
* Folder (for keeping stylesheets organized)

:::note
It is currently not possible to use any CSS preprocessor (such as SASS) in the backoffice.
:::

After creating a new stylesheet, you would work with it as you would with templates or javascript files - using the built-in backoffice text editor.
When you're working with stylesheets, you also have access to the Rich Text Editor, which allows you to create CSS styles and get a real-time preview.

![Stylesheet RTE](images/2-rte-editor.png)

The rules you create in the Rich Text Editor section will carry over to the Code tab.

![Stylesheet RTE tab](images/3-rte-editor-p2.png)
![Stylesheet Code tab](images/3-rte-editor-p3.png)

To reference your newly included stylesheet in a template file, navigate to Templates, pick the template you like (css files are usually referenced in the layout or home templates) and link to it with the `link` tag.

![Linking CSS in template](images/4-link-css.png)

By default, the stylesheets will be saved in the `css` folder in the solution.
To reference them you can use either of the methods used in the above screenshot.

```html
<link rel="stylesheet" href='@Url.Content("~/css/mystylesheet.css")'>
```
or
```html
<link rel="stylesheet" href="/css/mystylesheet.css">
```

With the stylesheet referenced, you will be able to style the template file with the rules and classes defined in the stylesheet.

Your stylesheets can be used in Rich Text Editors (datatype) as well - please see the [Rich Text Editor](../../Backoffice/Property-Editors/Built-in-Property-Editors/Rich-Text-Editor/RTE-Styles/) documentation for more information.

:::note
If your RTE is styled differently on the frontend of the site, the backoffice styling might be getting overwritten by other stylesheets you have included.
:::

## JavaScript files in the Backoffice

To create and edit JavaScript files in the Backoffice, head on over to the Scripts folder in the Settings section of the Backoffice.

![Creating a new JavaScript](images/8-create-js.png)

From here you can add a new JavaScript file, or a new folder.

Add a new JavaScript file and write your code:

![Sample JS script](images/9-myscript.png)

Then, navigate to the template where you would like to include your JS file.
```html
<script src="/scripts/myScript.js"></script>
```

![Reference the script in template](images/10-reference-script.png)

By default all JavaScript files will be stored in the `scripts` folder in the solution.

:::tip
If you are working locally, you can create CSS and JS files outside of the Backoffice - long as they are placed in appropiate folders (`css` and `scripts`), they will show up in the Backoffice.
:::

## Bundling & Minification for JavaScript and CSS

You can use whichever tool you are comfortable with for bundling & minification, though it is worth noting that Umbraco ships with the ClientDependency Framework which offers runtime bundling & minification.

You can bundle and minify as follows in a view template file.

```csharp
@using ClientDependency.Core.Mvc
@using ClientDependency.Core
@{
    Html.RequiresJs("~/scripts/Script1.js", 1);
    Html.RequiresJs("~/scripts/Script2.js", 2);

    Html.RequiresCss("~/css/style.css");
}
<html>
<head>
    @Html.RenderCssHere()
    @Html.RenderJsHere()
</head>
```

Full details of the ClientDependency Framework can be found here: [https://github.com/Shandem/ClientDependency](https://github.com/Shandem/ClientDependency)
