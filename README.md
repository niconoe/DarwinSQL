# DarwinSQL
DarwinCore Archives expressed as SQLite

## Rationale

The [Darwin Core Archive](https://en.wikipedia.org/wiki/Darwin_Core_Archive) format is widely used in the 
biodiversity informatics field (with [GBIF](http://www.gbif.org) for example), and has largely shown its effectiveness 
as an exchange format.    

Due to its nature (basically, a bunch of CSV files zipped together) it is however inefficient in terms of data use and 
analysis. Most people who consume Darwin Core will therefore immediately extract data from the Archive and transfer it 
to some format easier to manipulate, such as a relational database.

## DarwinSQL: the concept

There are two main goals to this project:

   - Defining a new file format with the following characteristics:
        - Can hold the same data as Darwin Core Archives
        - Keeps the perks of DwC-A: simple, contained in a single file, ...
        - Based on [SQLite](https://www.sqlite.org/) for improved performance, being directly queryable with SQL, being 
        directly compatible with the huge SQLite ecosystem (admin tools, GUI, converters, ...)
        - Stable, with the goal to ultimately become an official standard
        
   - Providing a basic implementation of this format:
        - A command-line tool to automatically convert (no questions asked): Darwin Core Archive -> DarwinSQL
        - (Possibly) a small webapp to perform this conversion
        - (Possibly) a DarwinSQL -> Darwin Core Archive converter
        - ...
        
Comments, contributions, patches, ... are more than welcome!