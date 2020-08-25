# docker-composer

Docker Composer, a visual editor for Docker Compose.

The main aim of this project is to provide a visual alternative to edit and visualize Docker Compose stacks. The tool was developed as a prototype/POC for a master's degree in software engineering dissertation at FEUP (Faculdade de Engenharia da Universidade do Porto). At the current stage the project is purely **experimental**.

The technologies used are [mxGraph](https://github.com/jgraph/mxgraph) for the graph-based visual map and [React](https://github.com/facebook/react) and [Bootstrap](https://github.com/twbs/bootstrap) for the remainder of the UI. It is distributed as an [Electron](https://github.com/electron/electron) app.

At the moment, only version 3 of Docker Compose is supported.

## Contents

* List of [Features](features) 
* For information on how to get started refer to [Quick start](#quick-start).
* For a detailed user manual refer to [How to use](#how-to-use).

## Features

* Visualize and edit Docker Compose stacks as a visual map of artifacts.
* Static validations and feedback.
* Integration with Docker Hub.
* Execute Docker Compose CLI commands through the UI.
* Visual feedback for running stacks.
* Easily integrates with existing projects.

## Quick start

The tool is available as an Electron app for Windows, Linux and Mac.

Download the executable for the target platform from the available releases and start the app.

Make sure you have Docker and Docker Compose installed in the host to fully use the tool.

### Development

To run the app in a development environment, do the following:

1. Clone repository or download the source code
2. Run `npm install` in the root folder.
3. Run `npm run electron-dev` in the root folder.

## How to use

This section contains an in-depth user manual.

### UI layout

The UI is split into five main panels: the **toolbar**, **image palette**, **properties editor**, **graph editor**, and **terminal**.

<p align="center">
  <img src="https://github.com/Kubix20/docker-composer/wiki/images/layout.png"/>
</p>
<p align="center">
  <b>Fig. 1:</b> Layout
</p>

The **toolbar** (located at the top of the screen) includes to the left an area dedicated to controlling status LED which lights up different colors according to the state of the running stack and a set of buttons to control the stack (such as starting and stopping) and on the right buttons for file management. Lastly, in the settings menu, you can set the working directory and adjust some output preferences when exporting files.

<p align="center">
  <img width="800" height="32" src="https://github.com/Kubix20/docker-composer/wiki/images/toolbar.png"/>
</p>
<p align="center">
  <b>Fig. 2:</b> Toolbar
</p>

The toolbar LED color code is shown bellow:

| State    |  Color                       |  Description                                       |
| -------- | :--------------------------: | -------------------------------------------------- |
| Off      |  ![images/led_off.png](images/led_off.png)     |  None of the services are running.                 |
| Starting |  ![images/led_starting.png](images/led_starting.png)|  The services are being (re)started or (re)created |
| Running  |  ![images/led_running.png](images/led_running.png) |  All the services in the stack are running         |
| Warning  |  ![images/led_warning.png](images/led_warning.png) |  At least one service in the stack is not running  |
<p align="center">
  <b>Table 1:</b> Toolbar LED color code
</p>

The **image palette** allows you to search for images hosted in Docker Hub and easily add new services by clicking and dragging the target image and dropping it in the graph editor area. You can also access the image page hosted on Docker Hub by clicking on the info icon near the image.

<p align="center">
  <img width="170" height="405" src="https://github.com/Kubix20/docker-composer/wiki/images/imagePalette.png"/>
</p>
<p align="center">
  <b>Fig. 3:</b> Image palette
</p>

The **graph editor** is split between the toolbar at the top, and the graph area itself. The toolbar allows you to perform actions such as adjusting the zoom level and clearing the graph editor. The graph area displays an interactive visual map of the stack containing the various artifacts that comprise the stack and their relationships.

<p align="center">
  <img width="500" height="416" src="https://github.com/Kubix20/docker-composer/wiki/images/graphEditor.png"/>
</p>
<p align="center">
  <b>Fig. 4:</b> Graph editor
</p>

The **properties editor** is useful to access and edit the various properties of currently selected object (artifact or connection) in the graph editor. It also provides quick access to some helpful links such as the Docker Compose docs and image information on Docker Hub.

<p align="center">
  <img width="170" height="322" src="https://github.com/Kubix20/docker-composer/wiki/images/propsEditor.png"/>
</p>
<p align="center">
  <b>Fig. 5:</b> Properties editor
</p>

The **terminal** (initially collapsed) displays the output produced by the services (containers) once created and started. It contains a “General” tab with the combined output of all services and additional logs (identical to the output of executing `docker compose up`) and individual tabs for the output of services that comprise the stack.

<p align="center">
  <img width="800" height="122" src="https://github.com/Kubix20/docker-composer/wiki/images/terminal.png"/>
</p>
<p align="center">
  <b>Fig. 6:</b> Terminal
</p>

### Managing files

You can save a stack (preserving the current layout) at any time by clicking on the Save button. This will create a hidden directory in the currently set working directory with an XML file or override the file if it already exists. You can load a stack from a previously saved project by clicking on the Open button and opening the directory where it was previously saved.

Alternatively, it is possible to import existing docker-compose YAML file by clicking on the Import button and opening the file. Similarly, it is also possible to export the stack as a docker compose YAML file and save it in a directory of your choice.

Whenever a stack is loaded, the working directory is automatically set to the path of the directory containing the selected stack.

### Visual notation

The graph area displays the visual map for the stack. This map is made up of visual representations for Docker Compose artifacts and their relationships (connections).

The artifacts correspond to those declared in the root level of the YAML:

* Services
* Volumes (Named)
* Networks
* Configs
* Secrets

<p align="center">
  <img width="300" height="244" src="https://github.com/Kubix20/docker-composer/wiki/images/service.png"/>
  <img width="200" height="154" src="https://github.com/Kubix20/docker-composer/wiki/images/artifacts.png"/>
</p>
<p align="center">
  <b>Fig. 7:</b> Artifacts
</p>

Relationships are represented as connections between artifacts:

| Connection                       | Representation          
| -------------------------------- |:--------------------------------: |
| Depends on between services      | ![images/depends_on.png](images/depends_on.png)        |
| Links between services           | ![images/links.png](images/links.png)             |
| Volume connection with service   | ![images/volumeConnection.png](images/volumeConnection.png)  |
| Network connection with service  | ![images/networkConnection.png](images/networkConnection.png) |
| Config connection with service   | ![images/configConnection.png](images/configConnection.png)  |
| Secret connection with service   | ![images/secretConnection.png](images/secretConnection.png)  |
<p align="center">
  <b>Table 2:</b> Connection types
</p>

For more information about each artifact and their properties, refer to the official [Docker Compose docs](https://docs.docker.com/compose/compose-file/).

### Graph editor actions

Viewing area:

* Pan the view by holding right click with the mouse and dragging.
* Adjust zoom level in the toolbar or through keyboard shortcuts.
* Multiple selections by dragging left click with the mouse to select an area.

Objects (artifacts and connections):

* Add new artifacts through the context menu opened by right clicking in an empty space of the graph area.
* Position an artifact by holding left click and dragging to the desired location.
* Add a connection by dragging left click from the anchor on the source artifact to the corresponding target. 
* Reposition a connection by selecting it and dragging its anchor points.
* Edit the properties of an object through the properties editor or directly in the node if applicable.
* Hover over an artifact to preview the output in YAML.
* Clear the editor by clicking the clear button on the toolbar.

### Keyboard shortcuts

Ctrl+plus(+) or Ctrl+ScrollWheelUp - Zoom in

Ctrl+minus(-) or Ctrl+ScrollWheelDown - Zoom out

Ctrl+Z - Undo

Ctrl+Y - Redo

Del - Delete selected artifact(s)

## Creating a stack

In a typical workflow, you create a stack by following a similar rationale to that of writing a textual docker-compose.yml. Start by adding the artifacts that will make up the stack (usually, begin by adding the services either by selecting an image from the image palette or through the context menu). Then connect the artifacts as desired. Finally, edit the properties of each object accordingly. Once the stack is ready to deploy, you can run it locally (i.e. not Swarm) by clicking on the 'Start' button.
