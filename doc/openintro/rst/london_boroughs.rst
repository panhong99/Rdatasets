=============== ===============
london_boroughs R Documentation
=============== ===============

London Borough Boundaries
-------------------------

Description
~~~~~~~~~~~

This dataset contains the coordinates of the boundaries of all 32
boroughs of the Greater London area.

Usage
~~~~~

::

   london_boroughs

Format
~~~~~~

A data frame with 45341 observations on the following 3 variables.

borough
   Name of the borough.

x
   The "easting" component of the coordinate, see details.

y
   The "northing" component of the coordinate, see details.

Details
~~~~~~~

Map data was made available through the Ordnance Survey Open Data
initiative. The data use the `National
Grid <https://en.wikipedia.org/wiki/Ordnance_Survey_National_Grid>`__
coordinate system, based upon eastings (``x``) and northings (``y``)
instead of longitude and latitude.

The ``name`` variable covers all 32 boroughs in Greater London:
``Barking & Dagenham``, ``Barnet``, ``Bexley``, ``Brent``, ``Bromley``,
``Camden``, ``Croydon``, ``Ealing``, ``Enfield``, ``Greenwich``,
``Hackney``, ``Hammersmith & Fulham``, ``Haringey``, ``Harrow``,
``Havering``, ``Hillingdon``, ``Hounslow``, ``Islington``,
``Kensington & Chelsea``, ``Kingston``, ``Lambeth``, ``Lewisham``,
``Merton``, ``Newham``, ``Redbridge``, ``Richmond``, ``Southwark``,
``Sutton``, ``Tower Hamlets``, ``Waltham Forest``, ``Wandsworth``,
``Westminster``

Source
~~~~~~

https://data.london.gov.uk/dataset/ordnance-survey-code-point

Contains Ordinance Survey data released under the `Open Government
License, OGL
v2 <http://www.nationalarchives.gov.uk/doc/open-government-licence/version/2/>`__.

See Also
~~~~~~~~

london_murders

Examples
~~~~~~~~

::


   library(dplyr)
   library(ggplot2)

   # Calculate number of murders by borough
   london_murders_counts <- london_murders %>%
     group_by(borough) %>%
     add_tally()

   london_murders_counts

   ## Not run: 
   # Add number of murders to geographic boundary data
   london_boroughs_murders <- inner_join(london_boroughs, london_murders_counts, by = "borough")

   # Map murders
   ggplot(london_boroughs_murders) +
     geom_polygon(aes(x = x, y = y, group = borough, fill = n), colour = "white") +
       scale_fill_distiller(direction = 1) +
     labs(x = "Easting", y = "Northing", fill = "Number of murders")

   ## End(Not run)
