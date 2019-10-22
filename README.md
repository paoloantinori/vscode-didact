# vscode-didact README  

The *vscode-didact* extension prototype does a few things. Mainly it shows what's possible through a combination of a simple Markdown file, the VS Code Webview, and calling through to easily accessible commands.

## VSCode-Didact In Action

What follows is a simple example with three actions. One scaffolds a project based on a structure defined in JSON. One opens a file created when the folder structure was created. And one triggers a command in a different extension if it's installed.

## Tutorial in Action

A simple tutorial is defined in [this MarkDown file](./example/tutorial2.md)

![Three Step Didact Tutorial Example](./images/didact-sample-tutorial-22-OCT-2019.gif)

# Implementation Notes

## CSS Styling

Currently we are using the CSS template suggested by the W3C, as provided [here at the Quackit.com site](https://www.quackit.com/css/css_template.cfm). We may be able to reuse some of the PatternFly approach, but that will require additional research.

## Link formatting

The Didact webview is listening for link events and responds if a link starts with `didact:`. All Didact links have the following qualities:

* Starts with `didact:`
* Then works in pairs
  * `commandId:your.vscode.command.id`
  * (optional) `projectFilePath:my/file/path` (assumes it's in the user's workspace, so has the workspace root prepended)
  * (optional) `srcFilePath:my/src/file/path` (assumes it's in the extension source, so prepends the extension `__dirname`)
  * Note: projectFilePath and srcFilePath should be mutually exclusive

## Project JSON Structure

The Project JSON file structure is simply a collection of named folders and files, as follows:

```{
    "folders": [
    {
       "name":"simpleGroovyProject",
       "folders": [
         {
             "name":"src",
             "files": [
                 {
                     "name":"simple.groovy",
                     "content":"from('timer:groovy?period=1s')\n\t.routeId('groovy')\n\t.setBody()\n\t.simple('Hello Camel K from ${routeId}')\n\t.to('log:info?showAll=false')\n"
                 }
             ]
           }
     ]
    }
 ]
}
```

# Next steps

1. Create a way to register a Didact tutorial.
2. Create a way to get a list of registered tutorials.
3. Find the best way to ensure that files (project.json, commands referencing files in a project scaffolded by a project.json) are accessible across extensions (i.e. if I register a tutorial in Camel K, the Didact extension should be ok with finding all the available commands and any files)
4. Provide a better CSS that perhaps mimicks what is being done in the Integreatly Walkthroughs project. 
5. Look into finding ways to chain commands together so that you can do things like create a project and open a file all in one go.
6. Look at the Eclipse Cheat sheet approach to see if we can glean anything - http://help.eclipse.org/kepler/index.jsp?topic=%2Forg.eclipse.platform.doc.isv%2Freference%2Fextension-points%2FcheatSheetContentFileSpec.html 
7. Also look at the Integr8ly Walkthroughs to see if we can glean anything - https://github.com/integr8ly/tutorial-web-app-walkthroughs/tree/master/walkthroughs


**Enjoy!**