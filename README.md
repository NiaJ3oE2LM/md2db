# The idea

**md2db** is a command-line tool for formatting markdown-typed information into an SQL database. Input markdown files are structured using headers, text emphasis, and file location according to *user-defined structural rules*. The output database contains one line per item and the number of columns depends on the *structural rules* that are enforced.

All the software is expecting, is plain text (in markdown format). No formulas, No images. See section Ouverture for further developments.

## Use-cases examples 

The necessity for developing  **md2db** was born from two simple tasks: annual expenses tracking and English vocabulary expansion.

Many smartphone-based applications provide good frameworks for addressing such problems. **md2db** tries to address similar problems with a more *linux-based* approach. Hopefully this will empower the end-user with remarkable robustness and freedom. 

This workflow exploits a smartphone as a text editor (markdown) and storing device. The generated markdown files are later copied to a different machine in order to perform the conversion and eventually continue the analysis of the information.

### Annual expenses tracking
A simple way to track personal annual expenses on a daily basis is to write one markdown log per day. Such file shall be named after the date of creation, and be written according to the following *structural rules*:
+ all expenses of the day are written in this daily markdown file
+ 1-st level headers (\#) contain the amount of the expenses. Such amount can be written with mathematical operations (+ \*/-)
+ the body corresponding to each 1-st level header contains a description of the expense item
+ emphasis text is not used in this context
+ daily logs can be grouped in sub-folders associated the weeks of the year. The name of the sub-folder identifies directly the week. 

Given a root folder location, converting all daily log files with **md2db** will result in a database with the following structure:
+ one line per each expense, corresponding to 1-st level headers.
+ column `date`. Extracted from the corresponding name of the log file
+ column `week`. Extracted from the relative location of the log file with respect to the given root folder.
+ column `amount`. Extracted from the content of the 1-st level header after computation of simple mathematical expressions
+ column `description`. Extracted from the body corresponding to the 1-st level header

Once the database has been created, the user can import its content in a tool of choice, and perform further analysis.

### Vocabulary expansion
When learning a foreign language it's essential to build a strong dictionary. To do so, one could read books and systematically write down unknown words. Such tedious task can be performed in separate steps in order to preserve the pleasure of reading a story.

A possible solution to such problem is to write unknown words in a markdown file with the following *structural rules*:
+ 1-st level headers are used to identify the source book. For example, one could write the title of the book and the corresponding chapter. This is useful when reading multiple books simultaneously.
+ 2-nd level headers are used to write the unknown word or idiom
+ the body corresponding to 2-nd level headers is used to write the definition of the unknown word.
+ text emphasis could be used to add extra information such as the *context of use* (formal, informal), examples, synonyms, ... If this is required, the user-defined *structural rule* should specify a 1-1 relation between the different text emphasis formats (italic, bold,  text-type, ...) and the corresponding meaning.
+ file location is not exploited in this context but could be used to group words by source (book) or topic.

Converting multiple such markdown files with **md2db** will result in a database with the following structure:
+ one line per unknown word corresponding to 2-nd level headers
+ column `word/idiom`. Extracted from the content of 2-nd level headers
+ column `definition`. Extracted from the body corresponding to 2-nd level headers short of extra text formatting (italic, bold, text-type, ...)
+ column `source`.  Extracted from the corresponding 1-st level header
+ column `extra`. Extracted from emphasized text (italic, bold, text-type, ...) according to user-defined rules. This column could eventually be split in different columns if needed

Once the database has been created the user can import its contents in a flash-card creation software.

# Code base

## Pseudo-code 

TOML settings file should contain:
1. definition of the *structural rules*. Define the map between each *standard* element of markdown format and the corresponding column in the resulting database. Header levels (1,2,3,...), text emphasis (italic, bold, text-type, ...). No lists / table / images are expected. 
2. root folder and file location. Define the mapping between sub-folder structure and columns of the resulting database. This could be enforced by specifying some kind of *recursion* level (R). For example, R=1 means that files are grouped by sub-folders and results in 1 column with the name of the sub-folder. 

Code conversion tasks:
1. todo

## Python implementation
dependencies: Python-Markdown

todo

## Rust implementation
dependencies:  crate markdown

todo

# Ouverture

dealing with images in text body

dealing with extra fields identified by text emphasis
