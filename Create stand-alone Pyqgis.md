#Sources: from https://github.com/mlaloux/My-Python-GIS_StackExchange-answers/blob/master/Python%20Script%20examples%20for%20geoprocessing%20shapefiles%20without%20using%20arcpy.md
There are 4 main ways to create a stand-alone Python code using QGIS environment and variables:
1. via commands in the Python console (ok)
2. via Python scripts in Processing or with the ScritRunner plugin of Gary Sherman (is this Python scripts inside QGIS?)
3. via development of custom plugins to the QGis application (this is Python plugins of QGIS)
4. outside QGIS (in the Python shell or creating an applications with PyQt4 and not Tkinter (why import Tkinter twice ?)

Is you are interested in (4), you can use PyQGIS as any other Python module. But Python does not know where to find PyQGIS. For that, you need to add the PyQGIS folder to the PYTHONPATH
You don't need here PyQt4, Tkinter or qgis.gui:

    from qgis.core import *
    QgsApplication.setPrefixPath("yourpath", True)
    QgsApplication.initQgis()
    # or your solution
    # read a shapefile 
    layer = QgsVectorLayer('your.shp', 'your', 'ogr')
    layer.isValid()
    True
    # loop through layer 
    for elem in layer.getFeatures():
        geom= elem.geometry()
        attr =elem.attributes()
        (processing)

     # interaction with other Python module: Shapely, for example
     from shapely.geometry import shape
     from json import loads
     for elem in layer.getFeatures():
           shapely_geometry = shape(loads(elem.geometry().exportToGeoJSON()))
           
You can create an application. You need here PyQt4 (and not Tkinter) and qgis.gui. So, for that, you must learn PyQt4 , as you have to learn Tkinter (or wxPython), for example. This is another problem: the solution given by gsherman is a problem of PyQt4, not of PyQGIS (look at PyQt4 tutorial, for example).
