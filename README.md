Introduction
------------

alertmap is (currently) a script for generating a map of probable earthquake early warning alert times, 
roughly based off of "Probabilistic Warning Times for Earthquake Ground Shaking in the San Francisco Bay Area", Allen, R.M., Seismological Research Letters Vol. 77, Number 3 pp. 371-376.

This code uses a local ShakeMap installation and assumes that the ShakeMap root path is "/home/shake/ShakeMap".


Installation and Dependencies
-----------------------------

This package depends on:
 * numpy, the fundamental package for scientific computing with Python. <a href="http://www.numpy.org/">http://www.numpy.org/</a>  
 * matplotlib, a Python 2D plotting library which produces publication quality figures. <a href="<a href="http://matplotlib.org/index.html">http://matplotlib.org/index.html</a>
 * scipy, a Python library which provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization. <a href="<a href="http://www.scipy.org/scipylib/index.html">http://www.scipy.org/scipylib/index.html</a>
 * obspy, a Python library for dealing with seismology data.
 * neicio, a Python library for reading/writing various spatial data formats (including ShakeMap grid.xml). 

The best way to install numpy,matplotlib,and scipy is to use one of the Python distributions described here:

<a href="http://www.scipy.org/install.html">http://www.scipy.org/install.html</a>

Anaconda and Enthought distributions have been successfully tested with smtools.

To install obspy:

pip install obspy

To install neicio:

pip install git+git://github.com/usgs/neicio.git

To install alertmap:

pip install git+git://github.com/mhearne-usgs/alertmap.git

Uninstalling and Updating
-------------------------

To uninstall:

pip uninstall alertmap

To update:

pip install -U git+git://github.com/mhearne-usgs/alertmap.git

Command line usage
------------------

<pre>
usage: getstrong.py [-h] [-c] [-i INPUTFOLDER] [-d] [-r RADIUS] [-e EVENTID]
                    [-y TIME LAT LON] [-w TIMEWINDOW] [-f FOLDER] [-u USER]
                    [-p PASSWORD] [-n] [-o]
                    {knet,geonet,turkey}

        Download and process strong motion data from different sources
        (NZ GeoNet, JP K-NET, Turkey) into peak ground motion values,
        and output in an XML format suitable for inclusion in
        ShakeMap.
        
        Generic (non-ShakeMap) Usage:
        To configure the system for further use (you will be prompted for 
        KNET username/password, and ShakeMap home):
        getstrong.py -c
        To process data from a local folder (rather than downloading from a remote source):
        getstrong.py -i INPUTFOLDER -f OUTPUTFOLDER
        To process data from a local folder and print peak ground motions to the screen:
        getstrong.py -i INPUTFOLDER -d

        To retrieve data from K-NET with a user-supplied K-NET username/password:
        getstrong.py knet -f ~/tmp/knet -y 2014-05-04T20:18:24 34.862 139.312 -u fred -p SECRETPASSWD

        To retrieve data from GeoNet:
        getstrong.py geonet -f ~/tmp/knet -y 2014-01-20T02:52:44 40.660 175.814

        To retrieve data from Turkey:
        getstrong.py turkey -f ~/tmp/knet -y 2003-05-01T00:27:06 38.970 40.450

        ###############################################################
        For Shakemap Users:
        To download K-NET data for an event into it's input folder, while retaining the raw data:
        
        getstrong.py knet -e EVENTID
        
        To download K-NET data for an event into it's input folder, while deleting the raw data:
        
        getstrong.py knet -e EVENTID -n
        

positional arguments:
  {knet,geonet,turkey}  Specify strong motion data source.

optional arguments:
  -h, --help            show this help message and exit
  -c, -config           Create config file for future use
  -i INPUTFOLDER, -inputfolder INPUTFOLDER
                        process files from an input folder.
  -d, -debug            print peak ground motions to the screen for debugging.
  -r RADIUS, -radius RADIUS
                        Specify distance window for search (km).
  -e EVENTID, -event EVENTID
                        Specify event ID (will search ShakeMap data directory.
  -y TIME LAT LON, -hypocenter TIME LAT LON
                        Specify UTC time, lat and lon. (time format YYYY-MM-
                        DDTHH:MM:SS)
  -w TIMEWINDOW, -window TIMEWINDOW
                        Specify time window for search (seconds) (default:
                        60).
  -f FOLDER, -folder FOLDER
                        Specify output station folder destination (defaults to
                        event input folder or current working directory)
  -u USER, -user USER   Specify K-NET user (defaults to value in config)
  -p PASSWORD, -password PASSWORD
                        Specify K-NET password (defaults to value in config)
  -n, -nuke             Do NOT retain extracted raw data files
  -o, -plot             Make QA plots
</pre>

<pre>
usage: smcheck.py [-h] eventID dataFile

Compare station data against a modeled ShakeMap.
        

positional arguments:
  eventID     Specify event ID (will search ShakeMap data directory.
  dataFile    Specify name of data file in event input folder to compare
              against ShakeMap grid.

optional arguments:
  -h, --help  show this help message and exit
</pre>
