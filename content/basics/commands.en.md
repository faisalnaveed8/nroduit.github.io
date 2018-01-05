---
title: Weasis Commands
weight: 50
---

The commands listed below can be applied at start-up or in a telnet session. All the commands starting by "dcmview2d:" allow to drive Weasis and are not adapted to be used at start-up.

{{% notice info %}}
This page matches to Weasis 2.5.1 or higher. The syntax of usage comes from <a target="_blank" href="http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html">POSIX</a>.
{{% /notice %}}

For getting the list of commands, after starting Weasis, open a local telnet session of the OSGI Console and type `lb` for getting the list of bundles and their state or type `help` for getting all the available commands:

``` text
telnet localhost 17179

Trying 127.0.0.1...

Connected to localhost.localdomain.

Escape character is '^]'.

____________________________

Welcome to Apache Felix Gogo

g! 
```

{{% notice tip %}}
**Modifying the default port number**: This value can be changed in the <a target="_blank" href="https://github.com/nroduit/weasis-pacs-connector#configuration-of-weasis-pacs-connector">configuration of the launcher</a> (by overriding the property or with a new jnlp template)
{{% /notice %}}

### List of Weasis commands

#### dcmview2d:layout

``` text
g! dcmview2d:layout
Select a split-screen layout
Usage: dcmview2d:layout ( -n NUMBER | -i ID )
  -n --number=NUMBER  select the best matching number of views
  -i --id=ID          select the layout from its identifier
  -? --help           show help
```

#### dcmview2d:mouseLeftAction

``` text
g! dcmview2d:mouseLeftAction
Change the mouse left action
Usage: dcmview2d:mouseLeftAction COMMAND
COMMAND is (sequence|winLevel|zoom|pan|rotation|crosshair|measure|draw|contextMenu|none)
  -? --help       show help
```

#### dcmview2d:move

``` text
g! dcmview2d:move
Pan the selected image
Usage: dcmview2d:move -- X Y
X and Y are Integer. It is mandatory to have '--' (end of options) for negative values
  -? --help       show help
```

#### dcmview2d:reset

``` text
g! dcmview2d:reset

Reset image display
Usage: dcmview2d:reset (-a | COMMAND...)
COMMAND is (winLevel|zoom|pan|rotation)
  -a --all        reset to original display
  -? --help       show help
```

#### dcmview2d:scroll

``` text
g! dcmview2d:scroll
Scroll into the images of the selected series
Usage: dcmview2d:scroll ( -s NUMBER | -i NUMBER | -d NUMBER)
  -s --set=NUMBER       set a new value from 1 to series size
  -i --increase=NUMBER  increase of some amount
  -d --decrease=NUMBER  decrease of some amount
  -? --help             show help
```

#### dcmview2d:synch

``` text
g! dcmview2d:synch
Set a synchronization mode
Usage: dcmview2d:synch VALUE
VALUE is (None|Stack|Tile)
  -? --help       show help
```

#### dcmview2d:wl

``` text
g! dcmview2d:wl
Change the window/level values of the selected image (increase or decrease into a normalized range of 4096)
Usage: dcmview2d:wl -- WIN LEVEL
WIN and LEVEL are Integer. It is mandatory to have '--' (end of options) for negative values
  -? --help       show help
```

#### dcmview2d:zoom

``` text
g! dcmview2d:zoom
Change the zoom value of the selected image
Usage: dcmview2d:zoom (set VALUE | increase NUMBER | decrease NUMBER)
  -s --set=VALUE        [decimal value]  set a new value from 0.0 to 12.0 (zoom magnitude, 0.0 => default, -200.0 => best fit, -100.0 => real size)
  -i --increase=NUMBER  increase of some amount
  -d --decrease=NUMBER  decrease of some amount
  -? --help             show help
```

#### dicom:get

``` text
g! dicom:get
Load DICOM files remotely or locally
Usage: dicom:get ([-l PATH]... [-r URI]... [-p] [-i DATA]... [-w URI]...)
PATH is either a directory(recursive) or a file
  -l --local=PATH   open DICOMs from local disk
  -r --remote=URI   open DICOMs from an URI
  -p --portable     open DICOMs from configured directories at the same level of the executable
  -i --iwado=DATA   open DICOMs from an XML manifest (GZIP-Base64)
  -w --wado=URI     open DICOMs from an XML manifest
  -? --help         show help
```

#### dicom:close

``` text
g! dicom:close
Close DICOM files
Usage: dicom:close  (-a | ([-y UID]... [-s UID]...))
  -a --all           close all the patients
  -y --study=UID     close a study, UID is Study Instance UID
  -s --series=UID    close a series, UID is Series Instance UID
  -? --help          show help
```

#### image:get

``` text
g! image:get
Load images remotely or locally
Usage: image:get ([-f file]... [-u url]...)
  -f --file=FILE     open an image from a file
  -u --url=URL       open an image from an URL
  -? --help          show help
```

#### image close

``` text
g! image:close
Close images
Usage: dicom:close (-a | ([-g UID]... [-s UID]...))
  -a --all         close all series
  -g --group=UID   close a group from its UID
  -s --series=UID   close an series/image from its UID
  -? --help        show help
```

#### weasis:info

``` text
g! weasis:info
Show information about Weasis
Usage: weasis:info (-v | -a)
  -v --version    show version
  -a --all        show weasis specifications
  -? --help       show help
```

#### weasis:ui

``` text
g! weasis:ui
Manage user interface
Usage: weasis:ui (-q | -v)
  -q --quit     shutdown Weasis
  -v --visible  set window on top
  -? --help     show help
```

#### acquire:patient

``` text
g! acquire:patient
Load Patient Context from the first argument
Usage: acquire:patient (-x | -i | -s | -u) arg
arg is an XML text in UTF8 or an url with the option '--url'
  -x --xml         open Patient Context from an XML data containing all DICOM Tags
  -i --inbound     open Patient Context from an XML data containing all DICOM Tags, decoding syntax is [Base64/GZip]
  -s --iurlsafe    open Patient Context from an XML data containing all DICOM Tags, decoding syntax is [Base64_URL_SAFE/GZip]
  -u --url         open Patient Context from an URL (XML file containing all DICOM TAGs)
  -? --help        show help
```

{{% notice note %}}
For identifying the commands at start-up, the symbol "$" must be added before the command (not required in the OSGI console). See examples below.
{{% /notice %}}


### Weasis Portable distribution

There are two ways to open local images with the portable distribution.

1. Load images automatically from a configured directory

    Set images into a “dicom” or “images” directory at the same level of the binary launcher (c.f. weasis-win32.exe). The default directories can be changed in weasis/conf/config.properties, see the properties starting by "weasis.portable." in [Weasis Weasis Preferences](../customize/preferences).
{{% notice tip %}}
Launch Weasis by double clicking on the executable file or in command-line (c.f. on Linux: ./weasis-linux.sh '$dicom:get --portable')
{{% /notice %}}


2. Launch arguments
    - Linux and Mac: commands must be in between quotes

        ``` text
        ./viewer-linux.sh '$dicom:get -l /home/Images/'


        Multiple commands:
        ./viewer-linux.sh '$dicom:get -l "/DICOM/Overlay"' '$weasis:ui --visible'


        Local directories (recursive) or files:
        ./viewer-linux.sh '$dicom:get -l "/DICOM/Overlay" -l "/DICOM/test/file.dcm"'

        Open non DICOM images (Local and URL):
        ./viewer-linux.sh '$image:get -f "/home/Images/test.png" -u https://dcm4che.atlassian.net/wiki/download/attachments/3670024/weasis-mpr.png'
        ```

    - Windows commands

        ``` text
        viewer-win32.exe $dicom:get -l "E:\\DICOM\\Overlay" -l "E:\\DICOM\\Shutter"
         
        viewer-win32.exe $dicom:get -l "E:/DICOM/Overlay" -l "E:/DICOM/Shutter"
        ```

{{% notice warning %}}
**Special characters**:
The command interpreter has changed from weasis 2.6.0. Command containing special characters like '&' must be within quotes or double quotes. Example: 
dicom:get -w **"url"**
<br><br>
It also depends of the command line system. For instance in the Eclipse launcher parameters, ‘&’ wihtin URLs needs to be escaped with backslash.
{{% /notice %}}