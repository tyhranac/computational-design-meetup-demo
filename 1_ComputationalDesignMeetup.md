# Intro to Web Development

### Agenda

1. Setup our development environment
   - Get tools we need to create websites/web apps

2. Review foundational web development tech and concepts
   - The languages and programming patterns used to create websites/web apps

3. Build!
   - Create a building viewer website

<img src="image.png" alt="Building in Scene Layer" width="800"/>

### 1: Setup our development environment

- Install [VS Code](https://code.visualstudio.com/Download)
  - Available in Application Workspace or via the download link if you have admin privileges
  - If permissions allow, add _Prettier_ and _HTML Boilerplate_ plugins
  - This is the text editor we'll use to write code; it also integrates with other software we'll be using

- Create a free [GitHub](https://github.com/) account
  - Github allows us to save our code in the cloud and also turn it into a publicly accessible website!

- Install [GitHub Desktop](https://desktop.github.com/download/)
  - Available in Application Workspace or via the download link if you have admin privileges
  - We'll use this to save and track changes in our code as it gets more complicated

- Install a web browser - we should all be set here :)
  - As a web developer, your browser is now one of your most important tools in addition to being a search engine/website viewer

### 2: Web Development basics

- Generative AI has gotten pretty good at developing websites, so we'll focus less on the specifics of code syntax and more on the general concepts needed to work with AI effectively

- Website/web app functionality can be broken down into _frontend_ and _backend_ functionality
  - The _frontend_ is what we see and interact with a user
    - The content layout, interactivity (buttons, dropdowns, etc.), and styling
    - _Frontend_ stuff happens on our machine, in whichever web browser we're using
    - The _frontend_ is written in HTML, CSS, and JavaScript

  - The _backend_ is largerly hidden from us when we're using a website/web app, but handles the behind the scenes logic
    - Managing user accounts, querying databases, performing complex analysis
    - _Backend_ stuff happens on a server in some data center
    - The _fackend_ can be written in many different programming languages; some common ones are Java, C#, Python, Go

- Our favorite web app as an example:

<img src="image-1.png" alt="Vantagepoint Home Page" width="800"/>

- We'll be focused on writing _frontend_ code, developing ways for users to interact with out building models via the web!

### 3: Build!

- We'll start with a "Hello world" web page using the most basic HTML and then add in some more advanced styling and functionality using CSS and JavaScript to display a building model in a 3D web map

- Resources:
    - [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
    - [Structuring Content with HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content)
    - [Styling Content with CSS](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics)
    - [Adding Functionality with JavaScript](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting)

- Final code:
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="description" content="" />

    <title>Building Viewer</title>

    <!-- Load Calcite components from CDN -->
    <script
      type="module"
      src="https://js.arcgis.com/calcite-components/3.3.3/calcite.esm.js"
    ></script>

    <!-- Load the ArcGIS Maps SDK for JavaScript -->
    <script src="https://js.arcgis.com/4.34/"></script>

    <!-- Load Map components from CDN-->
    <script
      type="module"
      src="https://js.arcgis.com/4.34/map-components/"
    ></script>

    <style>
      html,
      body {
        margin: 0;
        height: 100%;
      }
    </style>
  </head>
  <body>
    <arcgis-scene item-id="f477c289e93347aba6a0c052bfe0e0a4">
      <arcgis-zoom slot="top-left"></arcgis-zoom>
      <arcgis-navigation-toggle slot="top-left"></arcgis-navigation-toggle>
      <arcgis-compass slot="top-left"> </arcgis-compass>
      <arcgis-building-explorer slot="top-right"></arcgis-building-explorer>
    </arcgis-scene>
    <script type="module">
      const viewElement = document.querySelector("arcgis-scene");
      await viewElement.viewOnReady();

      viewElement.map.allLayers.forEach((layer) => {
        if (layer.title === "Esri Building E Demo") {
          // Explore building components in the layer using the BuildingExplorer
          const buildingExplorer = document.querySelector(
            "arcgis-building-explorer",
          );
          buildingExplorer.layers = [layer];
        }
      });
    </script>
  </body>
</html>
```
