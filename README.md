# virtualmicroscope
PNWU Virtual Microscope

The PNWU Virtual Microscope is a web-based program for displaying multifocal-plane, whole-slide-scanned microscope slides ("virtual slides") using an image-tile architecture similar to that used by the Google Maps API.  A version of this program can be seen at http://viewer.pnwu.edu.  The Virtual Microscope consists of two modules:  the SlideBox, which displayes the list of available slides and allows the user to choose which slide to display, and the Viewer (the "Microscope") which displays the chosen slide. 

Currently (December, 2020) the principal components of the Viewer (which can be found in the program consist of one HTML file (Microscoope.htm), one CSS file (jrscpStyleMain.css), nine javascript files (jrscpGlobal.js, jrscpProg.js, jrscpSldView.js, jrscpMove.js, jrscpFZ.js, jrscpMenu.js, jrscpTouchMain.js, jrscpTouchMenu.js, jrscpChgSet.js), and four PHP files (jrSQL_GetSldList.php, jrSQL_GetSldBasic.php, jrSQL_GetSldInfo.php, jrSQL_GetZYX.php); there also are ancilliary files (jpg, png, wav).  The principal components of the viewer need to be located within the same folder (directory) on the server; on GitHub, they are located in the directory named "UserFiles".  The PHP files need to be located in a directory named "SQLphp" that is at the same level on the server as 'UserFiles' (i.e., the are addressed by Ajax calls to "../SQLphp/'filename.php'").  The ancillary files (which also have been copied to GitHub) must be located in a directory named "images" that is at the same level on the server as 'UserFiles' (i.e., they are accessed by calls to "../images/'filename.jpg'").

Besides a database of microscope-image tiles, the program also relies on a SQL database containing metadata relative to each microscope slide.  It is anticipated that additional javascript and PHP files will need to be created when additions to the Virtual Microscope (such as tools for measuring/annotating the slides) are created.
Questions or comments regarding the PNWU Virtual Microscope can be emailed to:  Microscope@PNWU.edu.

Among the known bugs, there is a particularly aggravating bug that I would greatly appreciate help in eliminating.

For touchscreen devices, touching the part of the screen containing the image of the slide (a "div" with id="sldBndBox") results in a touchEvent whose target is the visible slideView plane (which is a child of "sldBndBox"), rather than sldBndBox, even though useCapture == true and the eventListener is attached to the parent (sldBndBox.addEventListener(); the eventListener is NOT attached to the child!).

I think that fact that the touchEvent is attached to the child of sldBndBox is the cause of another bug: when changing magnification or focus by pinching/spreading your fingers on the computer screen, the program frequently (usually) hangs after changing zoom-level or focal plane two or more times.  Lifting fingers off the screen unblocks the hang and allows the program to proceed with displaying the slide (including using pinch/spread to change zoom/focus). I'm guessing that the error is because the slideView plane to which the touchEvent belongs was destroyed when the number of view-plane was restricted.  If I only could figure out how to get the touchEvent to "belong" to sldBndBox (which is never destroyed) ... 
  
There are many aspects of the project that still need to be developed, and we would be delighted to have collaborators.  Among the sub-projects that we hope to address in the next few months (Spring & Summer 2020) are:
  (1) cleaning-up & debugging touchEvents on the part of the window (sldBndBox) that displays the slideView planes.
  (2) rewriting the Change Setting code ... the current code handling the user changing default settings is very 'clunky' and needs to be cleaned-up.
  (3) adding a scale-bar, tools for measuring & annotating elements within the specimen (annotations will require that we develop a login system so that the user can log-in to get and/or save annotations), and for exporting the URL that includes command-line arguments.

If you are interested in helping with this project, please email Jim Rhodes using the contact information listed in "About" => "About PNWU Microscope" in the microscope viewer:  http://viewer.pnwu.edu. 
