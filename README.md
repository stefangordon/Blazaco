# Patched Blazaco

I built this after writing my own ShareX (image / code / link) API in Blazor, just seeing what all it's capable of, and was looking for a way to style the code page. Found the BlazorBits but noticed it wasn't on Nuget anymore and was outdated, so decided to build an updated version. Any feedback would greatly be appreciated.

# Blazaco dependencies
* Visual Studio 16.1.0 Preview 3
* .NET Core 3.0.100-preview5-011568

# Demo
<a href="https://kyle-undefined.github.io/Blazaco/"><img src="https://forthebadge.com/images/badges/check-it-out.svg" /></a>

# Installation
  * Add the [NuGet](https://www.nuget.org/packages/Blazaco/) package to your Blazor Client project
```
dotnet add package Blazaco

// or

Install-Package Blazaco
```

# Usage
* Add the following to your root `_ViewImports.cshtml` file, or any file you want to use the Monaco Editor
```csharp
@using Blazaco
@using Blazaco.Editor
@using Blazaco.Editor.Options // Only needed if you want to change defaults
```

* Add the `MonacoEditor` Component anywhere in your file
```html
<MonacoEditor class="editor-class" ref="_editor" Model="@_editorModel" />
```

* Add your `MonacoEditor` and `EditorModel` fields to your `@functions`
```csharp
private EditorModel _editorModel { get; set; }
private MonacoEditor _editor;
```

* Configure Blazaco settings in your `OnInit` or `OnInitAsync`
```csharp
_editorModel = new EditorModel(); // Uses defaults

// or

var options = new EditorOptions()
{
    Value = "// Your Code Here!",
    Language = "csharp",
    Theme = "vs-dark"
};

_editorModel = new EditorModel(options);

// or

var options = new EditorOptions()
{
	Value = "// Your Code Here!",
	Language = "csharp",
	Theme = "vs-dark",
	Minimap = new MinimapOptions()
	{
		Enabled = false
	}
};

_editorModel = new EditorModel(options);

// or

_editorModel = new EditorModel(new EditorOptions()
{
	Value = "// Your Code Here!",
	Language = "csharp",
	Theme = "vs-dark",
	Minimap = new MinimapOptions()
	{
		Enabled = false
	}
});
```
_Note: You can configure the Constructor Options based on [these](https://microsoft.github.io/monaco-editor/api/interfaces/monaco.editor.ieditorconstructionoptions.html) options_

* Add the `monaco-editor` [folder](https://github.com/Kyle-Undefined/Blazaco/tree/master/samples/BlazacoTestApp/wwwroot/monaco-editor) and link the Javascript and CSS files in your `index.html` file
```html
<head>
    <link rel="stylesheet" data-name="vs/editor/editor.main" href="monaco-editor/min/vs/editor/editor.main.css">
</head>
<body>
    <app></app>
    ...
    <script>var require = { paths: { 'vs': 'monaco-editor/min/vs' } };</script>
    <script src="monaco-editor/min/vs/loader.js"></script>
    <script src="monaco-editor/min/vs/editor/editor.main.nls.js"></script>
    <script src="monaco-editor/min/vs/editor/editor.main.js"></script>
    <script type="blazor-boot">
    </script>
	...
</body>
```

# Interop
Currently I've only created a handful of Methods for Interop, as that's all I really need for my purposes. Current plans are to expand the Interop to allow more integration of the [Monaco Editor API](https://microsoft.github.io/monaco-editor/api/index.html) and make it more fleshed out.

* `InitializeEditor`
  * Internal Method to Initialize the Monaco Editor with default or set settings
* `GetValue`
  * Gets the Value from the Monaco Editor
* `SetValue`
  * Sets the Value for the Monaco Editor to display
* `SetTheme`
  * Sets the Theme for the Monaco Editor
* `Layout`
  * Instructs the editor to remeasure its container. This method should be called when the container of the editor gets resized

# Change log
  * History and changes can be located in the [CHANGELOG.md](https://github.com/Kyle-Undefined/Blazaco/blob/master/CHANGELOG.md)

# Copyright
Copyright (c) 2019 Kyle Undefined under the MIT License.

# Note
This is just a patched Version of https://github.com/Kyle-Undefined/Blazaco with all Merge Request merged and maybe other improvements. Enjoy!