# Code Style

## The #define Gaurd
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
First include Qt headers. After include Qt headers, include my header files.
```
// In pna_scene.h:
#ifndef PNA_SCENE_H
#define PNA_SCENE_H

// First include Qt headers 
#include <QFile>
#include <QThread>
...

// After include Qt headers, include my header files
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

## Names
### File Names
Filenames for `.cpp` and `.h` should be all lowercase and can include underscires(_).
```
pna_core.cpp
pna_core.h
```
Filenames for Qml Objects
```
PnaAboutDialog.qml
```

### Common Variable Names
Variable names in class, struct, global, local must be lowercase with underscore
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
Class names should always start with Pna
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
 
## Functions
### Function Declaration
If the fucntion is not inside the class must be start with `pna_`.
```
// In a class:
QString funcName(QString varName, int varName2, int defaultArgument = 1);

// Without class:
// For example see pna_utils.h
int pna_rawRead(PnaRawBuffer *raw_buf, char *dest);

```

### Function Definition
```
QString PnaScene::setBid(qreal bid)
{
  ...
}
```

### Inlinde Functions
Only used for functions with one line code.
```
QString lastcommand() const { return m_lastcommand; }
```

## Qml
Order 
### Signals
```
signal updateClicked()
```

## Conditionals
```
if (condition)
{
   //codes go here
}
else if (condition)
{
    //codes go here
}
else
{
    //codes go here
}
```

## Loops and Switch Statements
```
for (int i=0 ; i<10 ; i++)
{
    //codes go here
}

while (condition)
{
    //codes go here
}

switch (condition)
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
while (condition);
 ```
 
 ## Comments
 ### Variable Comments
 Comment on variables when defining them
 ```
 // In pna_scene.h
 QString m_calfopen;//file name for read calibration data
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
