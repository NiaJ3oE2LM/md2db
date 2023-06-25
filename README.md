# The idea

**md2db** is a tool for formatting markdown-typed information into an SQL database. Input markdown files are structured using headers, text emphasis, and file location according to *user-defined structural rules*. The output database contains one line per item and the number of columns depends on the *structural rules* that are enforced.

All the software is expecting is plain text (in markdown format). No formulas, No images. See section Ouverture for future expansion.

## Example applications

The necessity for developing  **md2db** was born from two simple tasks: annual expenses tracking and English vocabulary expansion.

Many smartphone-based applications provide good frameworks for addressing such problems. **md2db** tries to address similar problems with a more *linux-based* approach. Hopefully this will empower the end-user with remarkable robustness and freedom. 

### Annual expenses tracking
A simple way to track personal annual expenses on a daily basis is to write one markdown log per day. Such file shall be named after the date of creation, and be written according to the following *structural rules*:
+ all expenses of the day are written in this daily markdown file
+ 1-st level headers (\#) contain the amount of the expenses. Such amount can be written with mathematical operations (+ \*/-)
+ the body corresponding to each 1-st level header contains a description of the expense item
+ emphasis text is not used in this context
+ daily logs can be grouped in sub-folders associated the weeks of the year. The name of the sub-folder identifies directly the week. 

Given a root folder location, converting all daily log files with **md2db** will result in a database structure in the following way
+ one line per each expense, corresponding to 1-st level headers.
+ column `date`. Extracted from the corresponding name of the log file
+ column `week`. Extracted from the relative location of the log file with respect to the given root folder.
+ column `amount`. Extracted from the content of the 1-st level header after computation of simple mathematical expressions
+ column `description`. Extracted from the body corresponding to the 1-st level header

Once the database has been created, the user can import its content in her/his data analysis tool of choice, and perform further analysis.

### Vocabulary expansion
When learning 

# Code base

pseudocode 

## Python implementation

todo

## Rust implementation

todo

# Ouverture

images in text body

gui gtk
