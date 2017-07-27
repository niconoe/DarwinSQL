# DarwinSQL
Like DarwinCore Archive, but using SQLite

## Rationale

The [Darwin Core Archive](https://en.wikipedia.org/wiki/Darwin_Core_Archive) format is widely for biodiversity
informatics (within the [GBIF](http://www.gbif.org) community for example), and has largely shown its effectiveness
as an exchange format.

Due to its nature (basically, a bunch of CSV files zipped together) it is however a poor candidate for data use and
analysis: many users get data in Darwin Core Archive, but then immediately extract data from the Archive and transfer it
to some custom/non-standard format that's easier to manipulate, such as a spreadsheet or a relational database.

## DarwinSQL: the concept

The aim of DarwinSQL is to propose an alternative, standardized file format that can be used for exchanging data,
but also for simple data use and analysis.

There are two main milestones to this project:

   - Defining a new file format with the following characteristics:
        - Can hold the same content (data and metadata) as Darwin Core Archives
        - Keeps the perks of DwC-A: simple, contained in a single file, ...
        - Based on [SQLite](https://www.sqlite.org/):
            - improved performance
            - queryable with SQL 
            - directly compatible with the huge SQLite ecosystem (admin tools, GUI, converters, ...)
        - Stable, with the goal to ultimately become an official standard
        
   - Providing a basic implementation of this format:
        - A command-line tool to automatically convert (no questions asked): Darwin Core Archive -> DarwinSQL
        - (Possibly) a small webapp to perform this conversion
        - (Possibly) a DarwinSQL -> Darwin Core Archive converter
        - (Possibly) some examples
        - ...

## The DarwinSQL format

**Work in progress, subject to change at any time, comments are welcome!**

- DarwinSQL files are SQLite3 databases
- They use the *.dwsql* file extension
- It contains a table for each data/csv file in the source DwC-A (core and extensions). Rows/columns match the content 
of the source DwC-A. All fields are of TEXT type. Those tables *may* contains more fields for interpreted values. Those
fields are named: '<initialfieldname>_interpreted'
- It contains an `info` table describing the content of the DarwinSQL in a standardized format, similar to the 
`Metafile` of a Darwin Core Archives.
- It contains a `files` table that hold the raw content of each file of the Archive, except the data (CSV) files. 2 fields:
`path` (relative path of the file in the originating Darwin Core Archive) and `content` (BLOB)
  