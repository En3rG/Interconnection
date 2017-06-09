# Grid Interconnection Outline

See <a href="https://en3rg.github.io/Grid-Interconnection-Outline/index">example</a> output.  These are all generated by the program.

# Overview

This is a python project that models interconnections of a given system.  Components are represented in XML files which are then integrated together to generate the entire model of the system.  The program outputs HTML and javascript files that will render the connections between each components.

# Objective

The objective was to have a way of representing a complex system, that could have thousands of connections, in a clean and simplified way. Displaying a system with large amount of connections in a two dimensional plane can be very ugly.  It could almost look like a spider web, where it is almost impossible to trace each connections.  Displaying each components in a grid like format could minimize the overlapping connections.  The major problem in this scenario, is having the ability to know where to strategically place each of the components in the grid, to minimize overlaying connections.  Some scenarios, depending on the number of connections/number of components, are impossible to have no overlapping connections.  This is an NP complete problem, similar to 1-planar graph.  Fortunately, when tracing a problem on a system, you dont need to know the entire connections of a system.  Tracing the specific pin(s) along with all its dependencies/controls/etc should be sufficient in troubleshooting the problem at hand.

# Functionalities

* GUI

The GUI is written using PyQt5.  It allows the user to update multiple options, such as the CSS properties, logging options, multiprocessing options, and how the output is to be generated.  It also shows the user what components/adapters are available to be traced in the model.

* Generating XMLs

The program reads the existing XMLs and generate missing XMLs when necessary.  The XML is really a representation of say an engineering drawing.  Where it has a drawing number, nomenclature, revision date, and etc.  When generating missing XMLs, the program assumes that the naming convention on the pins are the same on both sides.  For example, cable1 with connector X has pins a,b and c which connects to cable2 with connector Y.  An assumption is made, that Cable2 connector Y will also have pins a, b and c as well. Thus if the data only contains an XML for cable1, the program will generate cable2 XML, which will be almost a mirror representation found in cable1.  This is to help speed up the process of generating the XML data.  Users still need to input additional data into the XML to better represent the model, such as descriptions or other internal components found within that component.  Mostly base on the engineering drawing of the component and any of its supporting documents.

* Output

The connection to be traced can be a single pin, a single component (with multiple pins), or multiple components.  Each component can be selected, which will then illustrate its internal connections.  The output is displayed in a grid layout, to improve readability.  Each component, can only have connections on its top, left, bottom, and/or right.

* Tracking components

When an output/model is generated, the user can track what data were used to generate the model.  Under additional info, the user can see what drawing revision were used to generate the model.

# Imrovements

* Test more scenarios
* Add Tree view (I had this option on my previous version but stripped it off with this one)
* Improve GUI, maybe use qml instead of widgets
* Improve output.  This was mostly done as a concept.  There are definitely better ways to represent the output than using just regular HTML and jsplumb.  I am sure there is a javascript library out there than can be used to better display the output.
