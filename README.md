# Coding Style

##### Table of Contents
**[The #define Guard](#guard)**  
**[Include](#include)**  
**[Name](#name)**  
**[Function](#function)**  
**[Conditional](#conditional)**  
**[Loop and Switch Statement](#loop-and-switch-statement)**  
**[Comment](#comment)**  
**[Qml](#qml)**  
<a name="headers"/>

## Guard
All header files should have #define guards to prevent multiple inclusion. The format of the symbol name should be FILE_NAME_H.
Example for class PnaScene
```
#ifndef PNA_SCENE_H
#define PNA_SCENE_H
...
#endif // PNA_SCENE_H
```

## Include
All `include` must be in header files and only the header for that class include to the .cpp file.
First include Qt headers after that, include my header files.
```
// In pna_scene.h:
#ifndef PNA_SCENE_H
#define PNA_SCENE_H

// First include Qt headers 
#include <QFile>
#include <QThread>
...

// Include project header files
#include "pna_plotter.h"
#include "pna_command.h"
...

class PnaScene
{
  ...
}

#endif // PNA_SCENE_H

// In pna_scene.cpp:
#include "pna_scene.h"

PnaScene::PnaScene()
{
  ...
}
...
```

## Name
### File Names
Filenames for `.cpp` and `.h` should be all lowercase and start with project name (pna). Word should be seprated with underscores(_) in the filenames.
```
pna_core.cpp
pna_core.h
```
Filenames for Qml Objects start with project name(Pna)
```
PnaAboutDialog.qml
```

### Common Variable Names
Variable names in struct, global, local must be lowercase with underscore
```
QString variable_name; // loswercase with underscore.
```

### Property Member Names in PnaScene Class
Start with `m_`, and the variable name must be in lowercase
```
class PnaScene 
{
  ...
private:
  QString m_labelunit; // start with 'm_', and variable name must be in lowsercase
}
```

### Class Names
Class names should always start with project name(Pna) and should be camel case.
```
class PnaScene
{
    ...
}
```

### Struct Names
```
typedef struct PnaRawBuffer
{
    volatile int write_index;//write index for interface
    volatile int read_index;//read index for calibration
    bool buffer_full;//check if buffer is almost full
    char *buffer;
}PnaRawBuffer;
```

### The .qrc File Names
Must be lowercase for example:
```
gallery.qrc
fonts.qrc
images.qrc
```
 
## Function
### Function Declaration
Functions should start with a lower letter and have a capital letter for each new word after that.
If the fucntion is not inside the class must be start with project name(Pna).
For better understanding refer to following examples:
```
// In a class:
QString funcName(QString var_name, int var_name2, int default_argument = 1);

// Without class:
// For example see pna_utils.h
int pna_rawRead(PnaRawBuffer *raw_buf, char *dest);

```

### Function Definition
```
void PnaCommand::configBoard(bool debug_mode, int interface_mode)
{
  ...
}
```

### Inlinde Functions
Only used for functions with one line code.
```
QString lastcommand() const { return m_lastcommand; }
```

## Conditional
```
if( condition )
{
   //codes go here
}
else if( test_variable==true )
{
    //codes go here
}
else
{
    //codes go here
}
```

## Loop and Switch Statement
```
for( int i=0 ; i<10 ; i++ )
{
    //codes go here
}

while( condition )
{
    //codes go here
}

switch( condition )
{
    case 1:
      //codes go here
      break;
    case 2:
      ...
    default:
      //codes go here
      break;
}

do
{
    //codes go here
}
while( condition );
 ```
 
## Comment
### Variable Comments
Comment on variables when defining them.
Inline comment should not touch `;` at the end of line.
```
// In pna_scene.h
QString m_calfopen; //file name for read calibration data
```

### Function Comments
Comment on functions when definition them. That means comment inside the `.cpp` files.
```
// In pna_utils.cpp
/*
* @id: id board. First board id is 0.
* @return: Value of config board based on key
*          and id. If not found return
*          QJsonValue(null).
*/
QJsonValue pna_getBoardValue(int id, QString key)
{
  ...
}
```

## Qml
### Signals
```
signal rxfSamplingChanged(real oldValue)
```

### The Component ID
```
Rectangle
{
    id: rect_container
}
```

### Property Name
```
property color color_border_disabled: "#a0a0a0"//lowercase with underscore
```

### Function
```
function updateLables(maximumValue)
{
    ...
}
```

### Example .qml File
```
import QtQuick 2.0

Rectangle
{
    property string text_label: ""
    property string text_unit:  ""
    
    property color color_border_enabled:  "#a0a0a0a"
    property color color_border_disabled: "#a0a0a0a"
    
    signal changeValueDial(real value)
    
    id: container
    width: 300
    height: 300
    
    Rectangle
    {
        id: rect_canvas
        ...
    }
    ...
    
    function enabled(valueTextInput)
    {
        ...
    }
    
}
```
