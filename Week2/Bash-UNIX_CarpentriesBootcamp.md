---
title: "Working With Files and Directories"
teaching: 30
exercises: 20
questions:
- "How can I create, copy, and delete files and directories?"
- "How can I edit files?"
objectives:
- "Create a directory hierarchy that matches a given diagram."
- "Create files in that hierarchy using an editor or by copying and renaming existing files."
- "Delete, copy and move specified files and/or directories."
keypoints:
- "`cp [old] [new]` copies a file."
- "`mkdir [path]` creates a new directory."
- "`mv [old] [new]` moves (renames) a file or directory."
- "`rm [path]` removes (deletes) a file."
- "`*` matches zero or more characters in a filename, so `*.txt` matches all files ending in `.txt`."
- "`?` matches any single character in a filename, so `?.txt` matches `a.txt` but not `any.txt`."
- "Use of the Control key may be described in many ways, including `Ctrl-X`, `Control-X`, and `^X`."
- "The shell does not have a trash bin: once something is deleted, it's really gone."
- "Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, but is normally used to indicate the type of data in the file."
- "Depending on the type of work you do, you may need a more powerful text editor than Nano."
---
## Creating directories
We now know how to explore files and directories,
but how do we create them in the first place?

### Step one: see where we are and what we already have
Let's go back to our `MarineGenomics` directory on the Desktop
and use `ls -F` to see what it contains:

~~~
$ pwd
~~~
{: .language-bash}

~~~
/home/margeno/MarineGenomics
~~~
{: .output}

~~~
$ ls -F
~~~
{: .language-bash}

~~~
Desktop/  Documents/  Downloads/  MarineGenomics/  Music/  Pictures/  Public/  Templates/  Videos/
~~~
{: .output}

### Create a directory

Let's create a new directory called `thesis` using the command `mkdir thesis`
(which has no output):

~~~
$ mkdir thesis
~~~
{: .language-bash}

As you might guess from its name,
`mkdir` means 'make directory'.
Since `thesis` is a relative path
(i.e., does not have a leading slash, like `/what/ever/thesis`),
the new directory is created in the current working directory:

~~~
$ ls -F
~~~
{: .language-bash}

~~~
Desktop/  Documents/  Downloads/  MarineGenomics/  Music/  Pictures/  Public/  Templates/  Videos/ thesis/
~~~
{: .output}

Since we've just created the `thesis` directory, there's nothing in it yet:

~~~
$ ls -F thesis
~~~
{: .language-bash}

Note that `mkdir` is not limited to creating single directories one at a time. The `-p` option allows `mkdir` to create a directory with any number of nested subdirectories in a single operation: 

~~~
$ mkdir -p thesis/chapter_1/section_1/subsection_1
~~~
{: .language-bash}

The `-R` option to the `ls` command will list all nested subdirectories within a directory.  Let's use `ls -FR` to recursively list the new directory hierarchy we just created beneath the `thesis` directory:

~~~
$ ls -FR thesis
chapter_1/

thesis/chapter_1:
section_1/

thesis/chapter_1/section_1:
subsection_1/

thesis/chapter_1/section_1/subsection_1:
~~~
{: .language-bash}

> ## Two ways of doing the same thing
> Using the shell to create a directory is no different than using a file explorer.
> If you open the current directory using your operating system's graphical file explorer,
> the `thesis` directory will appear there too.
> While the shell and the file explorer are two different ways of interacting with the files,
> the files and directories themselves are the same.
{: .callout}

> ## Good names for files and directories
>
> Complicated names of files and directories can make your life painful
> when working on the command line. Here we provide a few useful
> tips for the names of your files.
>
> 1. Don't use spaces.
>
>    Spaces can make a name more meaningful,
>    but since spaces are used to separate arguments on the command line
>    it is better to avoid them in names of files and directories.
>    You can use `-` or `_` instead (e.g. `north-pacific-gyre/` rather than `north pacific gyre/`).
>
> 2. Don't begin the name with `-` (dash).
>
>    Commands treat names starting with `-` as options.
>
> 3. Stick with letters, numbers, `.` (period or 'full stop'), `-` (dash) and `_` (underscore).
>
>    Many other characters have special meanings on the command line.
>    We will learn about some of these during this lesson.
>    There are special characters that can cause your command to not work as
>    expected and can even result in data loss.
>
> If you need to refer to names of files or directories that have spaces
> or other special characters, you should surround the name in quotes (`""`).
{: .callout}

### Create a text file
Let's change our working directory to `thesis` using `cd`,
then run a text editor called Nano to create a file called `draft.txt`:

~~~
$ cd thesis
$ nano draft.txt
~~~
{: .language-bash}

> ## Which Editor?
>
> When we say, '`nano` is a text editor' we really do mean 'text': it can
> only work with plain character data, not tables, images, or any other
> human-friendly media. We use it in examples because it is one of the
> least complex text editors. However, because of this trait, it may
> not be powerful enough or flexible enough for the work you need to do
> after this workshop. On Unix systems (such as Linux and macOS),
> many programmers use [Emacs](http://www.gnu.org/software/emacs/) or
> [Vim](http://www.vim.org/) (both of which require more time to learn),
> or a graphical editor such as
> [Gedit](http://projects.gnome.org/gedit/). On Windows, you may wish to
> use [Notepad++](http://notepad-plus-plus.org/).  Windows also has a built-in
> editor called `notepad` that can be run from the command line in the same
> way as `nano` for the purposes of this lesson.
>
> No matter what editor you use, you will need to know where it searches
> for and saves files. If you start it from the shell, it will (probably)
> use your current working directory as its default location. If you use
> your computer's start menu, it may want to save files in your desktop or
> documents directory instead. You can change this by navigating to
> another directory the first time you 'Save As...'
{: .callout}

Let's type in a few lines of text.
Once we're happy with our text, we can press <kbd>Ctrl</kbd>+<kbd>O</kbd>
(press the <kbd>Ctrl</kbd> or <kbd>Control</kbd> key and, while
holding it down, press the <kbd>O</kbd> key) to write our data to disk
(we'll be asked what file we want to save this to:
press <kbd>Return</kbd> to accept the suggested default of `draft.txt`).

<div style="width:80%; margin: auto;"><img alt="screenshot of nano text editor in action" src="../fig/nano-screenshot.png"></div>

Once our file is saved, we can use <kbd>Ctrl</kbd>+<kbd>X</kbd> to quit the editor and
return to the shell.

> ## Control, Ctrl, or ^ Key
>
> The Control key is also called the 'Ctrl' key. There are various ways
> in which using the Control key may be described. For example, you may
> see an instruction to press the <kbd>Control</kbd> key and, while holding it down,
> press the <kbd>X</kbd> key, described as any of:
>
> * `Control-X`
> * `Control+X`
> * `Ctrl-X`
> * `Ctrl+X`
> * `^X`
> * `C-x`
>
> In nano, along the bottom of the screen you'll see `^G Get Help ^O WriteOut`.
> This means that you can use `Control-G` to get help and `Control-O` to save your
> file.
{: .callout}

`nano` doesn't leave any output on the screen after it exits,
but `ls` now shows that we have created a file called `draft.txt`:

~~~
$ ls
~~~
{: .language-bash}

~~~
draft.txt
~~~
{: .output}

> ## Creating Files a Different Way
>
> We have seen how to create text files using the `nano` editor.
> Now, try the following command:
>
> ~~~
> $ touch my_file.txt
> ~~~
> {: .language-bash}
>
> 1.  What did the `touch` command do?
>     When you look at your current directory using the GUI file explorer,
>     does the file show up?
>
> 2.  Use `ls -l` to inspect the files.  How large is `my_file.txt`?
>
> 3.  When might you want to create a file this way?
>
> > ## Solution
> > 1.  The `touch` command generates a new file called `my_file.txt` in
> >     your current directory.  You
> >     can observe this newly generated file by typing `ls` at the
> >     command line prompt.  `my_file.txt` can also be viewed in your
> >     GUI file explorer.
> >
> > 2.  When you inspect the file with `ls -l`, note that the size of
> >     `my_file.txt` is 0 bytes.  In other words, it contains no data.
> >     If you open `my_file.txt` using your text editor it is blank.
> >
> > 3.  Some programs do not generate output files themselves, but
> >     instead require that empty files have already been generated.
> >     When the program is run, it searches for an existing file to
> >     populate with its output.  The touch command allows you to
> >     efficiently generate a blank text file to be used by such
> >     programs.
> {: .solution}
{: .challenge}

> ## What's In A Name?
>
> You may have noticed that all of Nelle's files are named 'something dot
> something', and in this part of the lesson, we always used the extension
> `.txt`.  This is just a convention: we can call a file `mythesis` or
> almost anything else we want. However, most people use two-part names
> most of the time to help them (and their programs) tell different kinds
> of files apart. The second part of such a name is called the
> **filename extension**, and indicates
> what type of data the file holds: `.txt` signals a plain text file, `.pdf`
> indicates a PDF document, `.cfg` is a configuration file full of parameters
> for some program or other, `.png` is a PNG image, and so on.
>
> This is just a convention, albeit an important one. Files contain
> bytes: it's up to us and our programs to interpret those bytes
> according to the rules for plain text files, PDF documents, configuration
> files, images, and so on.
>
> Naming a PNG image of a whale as `whale.mp3` doesn't somehow
> magically turn it into a recording of whalesong, though it *might*
> cause the operating system to try to open it with a music player
> when someone double-clicks it.
{: .callout}

## Moving files and directories
Returning to the `MarineGenomics` directory,

```
cd ~/MarineGenomics
```
{: .language-bash}

In our `thesis` directory we have a file `draft.txt`
which isn't a particularly informative name,
so let's change the file's name using `mv`,
which is short for 'move':

~~~
$ mv thesis/draft.txt thesis/quotes.txt
~~~
{: .language-bash}

The first argument tells `mv` what we're 'moving',
while the second is where it's to go.
In this case,
we're moving `thesis/draft.txt` to `thesis/quotes.txt`,
which has the same effect as renaming the file.
Sure enough,
`ls` shows us that `thesis` now contains one file called `quotes.txt`:

~~~
$ ls thesis
~~~
{: .language-bash}

~~~
quotes.txt
~~~
{: .output}

One has to be careful when specifying the target file name, since `mv` will
silently overwrite any existing file with the same name, which could
lead to data loss. An additional option, `mv -i` (or `mv --interactive`),
can be used to make `mv` ask you for confirmation before overwriting.

Note that `mv` also works on directories.

Let's move `quotes.txt` into the current working directory.
We use `mv` once again,
but this time we'll use just the name of a directory as the second argument
to tell `mv` that we want to keep the filename,
but put the file somewhere new.
(This is why the command is called 'move'.)
In this case,
the directory name we use is the special directory name `.` that we mentioned earlier.

~~~
$ mv thesis/quotes.txt .
~~~
{: .language-bash}

The effect is to move the file from the directory it was in to the current working directory.
`ls` now shows us that `thesis` is empty:

~~~
$ ls thesis
~~~
{: .language-bash}

Further,
`ls` with a filename or directory name as an argument only lists that file or directory.
We can use this to see that `quotes.txt` is still in our current directory:

~~~
$ ls quotes.txt
~~~
{: .language-bash}

~~~
quotes.txt
~~~
{: .output}

> ## Moving Files to a new folder
>
> After running the following commands,
> Jamie realizes that she put the files `sucrose.dat` and `maltose.dat` into the wrong folder. 
> The files should have been placed in the `raw` folder.
>
> ~~~
> $ ls -F
>  analyzed/ raw/
> $ ls -F analyzed
> fructose.dat glucose.dat maltose.dat sucrose.dat
> $ cd analyzed
> ~~~
> {: .language-bash}
>
> Fill in the blanks to move these files to the `raw/` folder
> (i.e. the one she forgot to put them in) 
>
> ~~~
> $ mv sucrose.dat maltose.dat ____/____
> ~~~
> {: .language-bash}
> > ## Solution
> > ```
> > $ mv sucrose.dat maltose.dat ../raw
> > ```
> > {: .language-bash}
> > Recall that `..` refers to the parent directory (i.e. one above the current directory)
> > and that `.` refers to the current directory.
> {: .solution}
{: .challenge}

## Copying files and directories

The `cp` command works very much like `mv`,
except it copies a file instead of moving it.
We can check that it did the right thing using `ls`
with two paths as arguments --- like most Unix commands,
`ls` can be given multiple paths at once:

~~~
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
~~~
{: .language-bash}

~~~
quotes.txt   thesis/quotations.txt
~~~
{: .output}

We can also copy a directory and all its contents by using the
[recursive](https://en.wikipedia.org/wiki/Recursion) option `-r`,
e.g. to back up a directory:

```
$ cp -r thesis thesis_backup
```
{: .language-bash}

We can check the result by listing the contents of both the `thesis` and `thesis_backup` directory:

```
$ ls thesis thesis_backup
```
{: .language-bash}

```
thesis:
quotations.txt

thesis_backup:
quotations.txt
```
{: .output}


> ## Renaming Files
>
> Suppose that you created a plain-text file in your current directory to contain a list of the
> statistical tests you will need to do to analyze your data, and named it: `statstics.txt`
>
> After creating and saving this file you realize you misspelled the filename! You want to
> correct the mistake, which of the following commands could you use to do so?
>
> 1. `cp statstics.txt statistics.txt`
> 2. `mv statstics.txt statistics.txt`
> 3. `mv statstics.txt .`
> 4. `cp statstics.txt .`
>
> > ## Solution
> > 1. No.  While this would create a file with the correct name, the incorrectly named file still exists in the directory
> > and would need to be deleted.
> > 2. Yes, this would work to rename the file.
> > 3. No, the period(.) indicates where to move the file, but does not provide a new file name; identical file names
> > cannot be created.
> > 4. No, the period(.) indicates where to copy the file, but does not provide a new file name; identical file names
> > cannot be created.
> {: .solution}
{: .challenge}

> ## Moving and Copying
>
> What is the output of the closing `ls` command in the sequence shown below?
>
> ~~~
> $ pwd
> ~~~
> {: .language-bash}
> ~~~
> /Users/jamie/data
> ~~~
> {: .output}
> ~~~
> $ ls
> ~~~
> {: .language-bash}
> ~~~
> proteins.dat
> ~~~
> {: .output}
> ~~~
> $ mkdir recombined
> $ mv proteins.dat recombined/
> $ cp recombined/proteins.dat ../proteins-saved.dat
> $ ls
> ~~~
> {: .language-bash}
>
>
> 1.   `proteins-saved.dat recombined`
> 2.   `recombined`
> 3.   `proteins.dat recombined`
> 4.   `proteins-saved.dat`
>
> > ## Solution
> > We start in the `/Users/jamie/data` directory, and create a new folder called `recombined`.
> > The second line moves (`mv`) the file `proteins.dat` to the new folder (`recombined`).
> > The third line makes a copy of the file we just moved.  The tricky part here is where the file was
> > copied to.  Recall that `..` means 'go up a level', so the copied file is now in `/Users/jamie`.
> > Notice that `..` is interpreted with respect to the current working
> > directory, **not** with respect to the location of the file being copied.
> > So, the only thing that will show using ls (in `/Users/jamie/data`) is the recombined folder.
> >
> > 1. No, see explanation above.  `proteins-saved.dat` is located at `/Users/jamie`
> > 2. Yes
> > 3. No, see explanation above.  `proteins.dat` is located at `/Users/jamie/data/recombined`
> > 4. No, see explanation above.  `proteins-saved.dat` is located at `/Users/jamie`
> {: .solution}
{: .challenge}

## Removing files and directories

Returning to the `MarineGenomics` directory,
let's tidy up this directory by removing the `quotes.txt` file we created.
The Unix command we'll use for this is `rm` (short for 'remove'):

~~~
$ rm quotes.txt
~~~
{: .language-bash}

We can confirm the file has gone using `ls`:

~~~
$ ls quotes.txt
~~~
{: .language-bash}

```
ls: cannot access 'quotes.txt': No such file or directory
```
{: .output}

> ## Deleting Is Forever
>
> The Unix shell doesn't have a trash bin that we can recover deleted
> files from (though most graphical interfaces to Unix do).  Instead,
> when we delete files, they are unlinked from the file system so that
> their storage space on disk can be recycled. Tools for finding and
> recovering deleted files do exist, but there's no guarantee they'll
> work in any particular situation, since the computer may recycle the
> file's disk space right away.
{: .callout}


> ## Using `rm` Safely
>
> What happens when we execute `rm -i thesis_backup/quotations.txt`?
> Why would we want this protection when using `rm`?
>
> > ## Solution
> > ```
> > $ rm: remove regular file 'thesis_backup/quotations.txt'? y
> > ```
> > {: .language-bash}
> > The `-i` option will prompt before (every) removal (use <kbd>Y</kbd> to confirm deletion or <kbd>N</kbd> to keep the file).
> > The Unix shell doesn't have a trash bin, so all the files removed will disappear forever.
> > By using the `-i` option, we have the chance to check that we are deleting only the files that we want to remove.
> {: .solution}
{: .challenge}


If we try to remove the `thesis` directory using `rm thesis`,
we get an error message:

~~~
$ rm thesis
~~~
{: .language-bash}

~~~
rm: cannot remove `thesis': Is a directory
~~~
{: .error}

This happens because `rm` by default only works on files, not directories.

`rm` can remove a directory *and all its contents* if we use the
recursive option `-r`, and it will do so *without any confirmation prompts*:

~~~
$ rm -r thesis
~~~
{: .language-bash}

Given that there is no way to retrieve files deleted using the shell,
`rm -r` *should be used with great caution* (you might consider adding the interactive option `rm -r -i`).

## Operations with multiple files and directories

Oftentimes one needs to copy or move several files at once. This can be done by providing a list of individual filenames, or specifying a naming pattern using wildcards.

> ## Copy with Multiple Filenames
>
> For this exercise, you can test the commands in the `data-shell/data` directory.
>
> In the example below, what does `cp` do when given several filenames and a directory name?
>
> ~~~
> $ mkdir backup
> $ cp amino-acids.txt animals.txt backup/
> ~~~
> {: .language-bash}
>
> In the example below, what does `cp` do when given three or more file names?
>
> ~~~
> $ ls -F
> ~~~
> {: .language-bash}
> ~~~
> amino-acids.txt  animals.txt  backup/  elements/  morse.txt  pdb/  planets.txt  salmon.txt  sunspot.txt
> ~~~
> {: .output}
> ~~~
> $ cp amino-acids.txt animals.txt morse.txt
> ~~~
> {: .language-bash}
>
> > ## Solution
> > If given more than one file name followed by a directory name (i.e. the destination directory must
> > be the last argument), `cp` copies the files to the named directory.
> >
> > If given three file names, `cp` throws an error such as the one below, because it is expecting a directory
> > name as the last argument.
> >
> > ```
> > cp: target ‘morse.txt’ is not a directory
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

### Using wildcards for accessing multiple files at once

> ## Wildcards
>
> `*` is a **wildcard**, which matches zero or more  characters.
> Let's consider the `data-shell/molecules` directory:
> `*.pdb` matches `ethane.pdb`, `propane.pdb`, and every
> file that ends with '.pdb'. On the other hand, `p*.pdb` only matches
> `pentane.pdb` and `propane.pdb`, because the 'p' at the front only
> matches filenames that begin with the letter 'p'.
>
> `?` is also a wildcard, but it matches exactly one character.
> So `?ethane.pdb` would match `methane.pdb` whereas
> `*ethane.pdb` matches both `ethane.pdb`, and `methane.pdb`.
>
> Wildcards can be used in combination with each other
> e.g. `???ane.pdb` matches three characters followed by `ane.pdb`,
> giving `cubane.pdb  ethane.pdb  octane.pdb`.
>
> When the shell sees a wildcard, it expands the wildcard to create a
> list of matching filenames *before* running the command that was
> asked for. As an exception, if a wildcard expression does not match
> any file, Bash will pass the expression as an argument to the command
> as it is. For example typing `ls *.pdf` in the `molecules` directory
> (which contains only files with names ending with `.pdb`) results in
> an error message that there is no file called `*.pdf`.
> However, generally commands like `wc` and `ls` see the lists of
> file names matching these expressions, but not the wildcards
> themselves. It is the shell, not the other programs, that deals with
> expanding wildcards, and this is another example of orthogonal design.
{: .callout}

> ## List filenames matching a pattern
>
> When run in the `molecules` directory, which `ls` command(s) will
> produce this output?
>
> `ethane.pdb   methane.pdb`
>
> 1. `ls *t*ane.pdb`
> 2. `ls *t?ne.*`
> 3. `ls *t??ne.pdb`
> 4. `ls ethane.*`
>
> > ## Solution
>>  The solution is `3.`
>>
>> `1.` shows all files whose names contain zero or more characters (`*`) followed by the letter `t`, then zero or more characters (`*`) followed by `ane.pdb`. This gives `ethane.pdb  methane.pdb  octane.pdb  pentane.pdb`.
>>
>> `2.` shows all files whose names start with zero or more characters (`*`) followed by the letter `t`, then a single character (`?`), then `ne.` followed by zero or more characters (`*`). This will give us `octane.pdb` and `pentane.pdb` but doesn't match anything which ends in `thane.pdb`.
>>
>> `3.` fixes the problems of option 2 by matching two characters (`??`) between `t` and `ne`. This is the solution.
>>
>> `4.` only shows files starting with `ethane.`.
> {: .solution}
{: .challenge}

> ## More on Wildcards
>
> Sam has a directory containing calibration data, datasets, and descriptions of
> the datasets:
>
> ~~~
> .
> ├── 2015-10-23-calibration.txt
> ├── 2015-10-23-dataset1.txt
> ├── 2015-10-23-dataset2.txt
> ├── 2015-10-23-dataset_overview.txt
> ├── 2015-10-26-calibration.txt
> ├── 2015-10-26-dataset1.txt
> ├── 2015-10-26-dataset2.txt
> ├── 2015-10-26-dataset_overview.txt
> ├── 2015-11-23-calibration.txt
> ├── 2015-11-23-dataset1.txt
> ├── 2015-11-23-dataset2.txt
> ├── 2015-11-23-dataset_overview.txt
> ├── backup
> │   ├── calibration
> │   └── datasets
> └── send_to_bob
>     ├── all_datasets_created_on_a_23rd
>     └── all_november_files
> ~~~
> {: .language-bash}
>
> Before heading off to another field trip, she wants to back up her data and
> send some datasets to her colleague Bob. Sam uses the following commands
> to get the job done:
>
> ~~~
> $ cp *dataset* backup/datasets
> $ cp ____calibration____ backup/calibration
> $ cp 2015-____-____ send_to_bob/all_november_files/
> $ cp ____ send_to_bob/all_datasets_created_on_a_23rd/
> ~~~
> {: .language-bash}
>
> Help Sam by filling in the blanks.
>
> The resulting directory structure should look like this
> ```
> .
> ├── 2015-10-23-calibration.txt
> ├── 2015-10-23-dataset1.txt
> ├── 2015-10-23-dataset2.txt
> ├── 2015-10-23-dataset_overview.txt
> ├── 2015-10-26-calibration.txt
> ├── 2015-10-26-dataset1.txt
> ├── 2015-10-26-dataset2.txt
> ├── 2015-10-26-dataset_overview.txt
> ├── 2015-11-23-calibration.txt
> ├── 2015-11-23-dataset1.txt
> ├── 2015-11-23-dataset2.txt
> ├── 2015-11-23-dataset_overview.txt
> ├── backup
> │   ├── calibration
> │   │   ├── 2015-10-23-calibration.txt
> │   │   ├── 2015-10-26-calibration.txt
> │   │   └── 2015-11-23-calibration.txt
> │   └── datasets
> │       ├── 2015-10-23-dataset1.txt
> │       ├── 2015-10-23-dataset2.txt
> │       ├── 2015-10-23-dataset_overview.txt
> │       ├── 2015-10-26-dataset1.txt
> │       ├── 2015-10-26-dataset2.txt
> │       ├── 2015-10-26-dataset_overview.txt
> │       ├── 2015-11-23-dataset1.txt
> │       ├── 2015-11-23-dataset2.txt
> │       └── 2015-11-23-dataset_overview.txt
> └── send_to_bob
>     ├── all_datasets_created_on_a_23rd
>     │   ├── 2015-10-23-dataset1.txt
>     │   ├── 2015-10-23-dataset2.txt
>     │   ├── 2015-10-23-dataset_overview.txt
>     │   ├── 2015-11-23-dataset1.txt
>     │   ├── 2015-11-23-dataset2.txt
>     │   └── 2015-11-23-dataset_overview.txt
>     └── all_november_files
>         ├── 2015-11-23-calibration.txt
>         ├── 2015-11-23-dataset1.txt
>         ├── 2015-11-23-dataset2.txt
>         └── 2015-11-23-dataset_overview.txt
> ```
> {: .language-bash}
>
> > ## Solution
> > ```
> > $ cp *calibration.txt backup/calibration
> > $ cp 2015-11-* send_to_bob/all_november_files/
> > $ cp *-23-dataset* send_to_bob/all_datasets_created_on_a_23rd/
> > ```
> > {: .language-bash}
> {: .solution}
{: .challenge}

> ## Organizing Directories and Files
>
> Jamie is working on a project and she sees that her files aren't very well
> organized:
>
> ~~~
> $ ls -F
> ~~~
> {: .language-bash}
> ~~~
> analyzed/  fructose.dat    raw/   sucrose.dat
> ~~~
> {: .output}
>
> The `fructose.dat` and `sucrose.dat` files contain output from her data
> analysis. What command(s) covered in this lesson does she need to run so that the commands below will
> produce the output shown?
>
> ~~~
> $ ls -F
> ~~~
> {: .language-bash}
> ~~~
> analyzed/   raw/
> ~~~
> {: .output}
> ~~~
> $ ls analyzed
> ~~~
> {: .language-bash}
> ~~~
> fructose.dat    sucrose.dat
> ~~~
> {: .output}
>
> > ## Solution
> > ```
> > mv *.dat analyzed
> > ```
> > {: .language-bash}
> > Jamie needs to move her files `fructose.dat` and `sucrose.dat` to the `analyzed` directory.
> > The shell will expand *.dat to match all .dat files in the current directory.
> > The `mv` command then moves the list of .dat files to the 'analyzed' directory.
> {: .solution}
{: .challenge}

> ## Reproduce a folder structure
>
> You're starting a new experiment, and would like to duplicate the directory
> structure from your previous experiment so you can add new data.
>
> Assume that the previous experiment is in a folder called '2016-05-18',
> which contains a `data` folder that in turn contains folders named `raw` and
> `processed` that contain data files.  The goal is to copy the folder structure
> of the `2016-05-18-data` folder into a folder called `2016-05-20`
> so that your final directory structure looks like this:
>
>	2016-05-20/
>	└── data
>	    ├── processed
>	    └── raw
>
> Which of the following set of commands would achieve this objective?
> What would the other commands do?
>
> ~~~
> $ mkdir 2016-05-20
> $ mkdir 2016-05-20/data
> $ mkdir 2016-05-20/data/processed
> $ mkdir 2016-05-20/data/raw
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir 2016-05-20
> $ cd 2016-05-20
> $ mkdir data
> $ cd data
> $ mkdir raw processed
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir 2016-05-20/data/raw
> $ mkdir 2016-05-20/data/processed
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir -p 2016-05-20/data/raw
> $ mkdir -p 2016-05-20/data/processed
> ~~~
> {: .language-bash}
> ~~~
> $ mkdir 2016-05-20
> $ cd 2016-05-20
> $ mkdir data
> $ mkdir raw processed
> ~~~
> {: .language-bash}
> >
> > ## Solution
> > The first two sets of commands achieve this objective.
> > The first set uses relative paths to create the top level directory before
> > the subdirectories.
> >
> > The third set of commands will give an error because the default behavior of `mkdir` won't create a subdirectory
> > of a non-existant directory: the intermediate level folders must be created first.
> >
> > The fourth set of commands achieve this objective. Remember, the `-p` option, followed by a path of one or more 
> > directories, will cause `mkdir` to create any intermediate subdirectories as required.
> >
> > The final set of commands generates the 'raw' and 'processed' directories at the same level
> > as the 'data' directory.
> {: .solution}
{: .challenge}

---
title: "Pipes and Filters"
teaching: 25
exercises: 10
questions:
- "How can I combine existing commands to do new things?"
objectives:
- "Redirect a command's output to a file."
- "Process a file instead of keyboard input using redirection."
- "Construct command pipelines with two or more stages."
- "Explain what usually happens if a program or pipeline isn't given any input to process."
- "Explain Unix's 'small pieces, loosely joined' philosophy."
keypoints:
- "`cat` displays the contents of its inputs."
- "`head` displays the first 10 lines of its input."
- "`tail` displays the last 10 lines of its input."
- "`sort` sorts its inputs."
- "`wc` counts lines, words, and characters in its inputs."
- "`command > [file]` redirects a command's output to a file (overwriting any existing content)."
- "`command >> [file]` appends a command's output to a file."
- "`[first] | [second]` is a pipeline: the output of the first command is used as the input to the second."
- "The best way to use the shell is to use pipes to combine simple single-purpose programs (filters)."
---

Now that we know a few basic commands,
we can finally look at the shell's most powerful feature:
the ease with which it lets us combine existing programs in new ways.
We'll start with the directory called `data-shell/molecules`
that contains six files describing some simple organic molecules.
The `.pdb` extension indicates that these files are in Protein Data Bank format,
a simple text format that specifies the type and position of each atom in the molecule.

~~~
$ ls molecules
~~~
{: .language-bash}

~~~
cubane.pdb    ethane.pdb    methane.pdb
octane.pdb    pentane.pdb   propane.pdb
~~~
{: .output}

Let's go into that directory with `cd` and run an example  command `wc cubane.pdb`:

~~~
$ cd molecules
$ wc cubane.pdb 
~~~
{: .language-bash}

~~~
20  156 1158 cubane.pdb
~~~
{: .output}

`wc` is the 'word count' command:
it counts the number of lines, words, and characters in files (from left to right, in that order).

If we run the command `wc *.pdb`, the `*` in `*.pdb` matches zero or more characters,
so the shell turns `*.pdb` into a list of all `.pdb` files in the current directory:

~~~
$ wc *.pdb
~~~
{: .language-bash}

~~~
  20  156  1158  cubane.pdb
  12  84   622   ethane.pdb
   9  57   422   methane.pdb
  30  246  1828  octane.pdb
  21  165  1226  pentane.pdb
  15  111  825   propane.pdb
 107  819  6081  total
~~~
{: .output}

Note that `wc *.pdb` also shows the total number of all lines in the last line of the output.

If we run `wc -l` instead of just `wc`,
the output shows only the number of lines per file:

~~~
$ wc -l *.pdb
~~~
{: .language-bash}

~~~
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
~~~
{: .output}

The `-m` and `-w` options can also be used with the `wc` command, to show 
only the number of characters or the number of words in the files.

> ## Why Isn't It Doing Anything?
>
> What happens if a command is supposed to process a file, but we
> don't give it a filename? For example, what if we type:
>
> ~~~
> $ wc -l
> ~~~
> {: .language-bash}
>
> but don't type `*.pdb` (or anything else) after the command?
> Since it doesn't have any filenames, `wc` assumes it is supposed to
> process input given at the command prompt, so it just sits there and waits for us to give
> it some data interactively. From the outside, though, all we see is it
> sitting there: the command doesn't appear to do anything.
>
> If you make this kind of mistake, you can escape out of this state by holding down
> the control key (<kbd>Ctrl</kbd>) and typing the letter <kbd>C</kbd> once and letting go of the <kbd>Ctrl</kbd> key.
> <kbd>Ctrl</kbd>+<kbd>C</kbd>
{: .callout}

Which of these files contains the fewest lines?
It's an easy question to answer when there are only six files,
but what if there were 6000?
Our first step toward a solution is to run the command:

~~~
$ wc -l *.pdb > lengths.txt
~~~
{: .language-bash}

The greater than symbol, `>`, tells the shell to **redirect** the command's output
to a file instead of printing it to the screen. (This is why there is no screen output:
everything that `wc` would have printed has gone into the
file `lengths.txt` instead.)  The shell will create
the file if it doesn't exist. If the file exists, it will be
silently overwritten, which may lead to data loss and thus requires
some caution.
`ls lengths.txt` confirms that the file exists:

~~~
$ ls lengths.txt
~~~
{: .language-bash}

~~~
lengths.txt
~~~
{: .output}

We can now send the content of `lengths.txt` to the screen using `cat lengths.txt`.
The `cat` command gets its name from 'concatenate' i.e. join together,
and it prints the contents of files one after another.
There's only one file in this case,
so `cat` just shows us what it contains:

~~~
$ cat lengths.txt
~~~
{: .language-bash}

~~~
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
~~~
{: .output}

> ## Output Page by Page
>
> We'll continue to use `cat` in this lesson, for convenience and consistency,
> but it has the disadvantage that it always dumps the whole file onto your screen.
> More useful in practice is the command `less`,
> which you use with `less lengths.txt`.
> This displays a screenful of the file, and then stops.
> You can go forward one screenful by pressing the spacebar,
> or back one by pressing `b`.  Press `q` to quit.
{: .callout}

Now let's use the `sort` command to sort its contents.

> ## What Does `sort -n` Do?
>
> If we run `sort` on a file containing the following lines:
>
> ~~~
> 10
> 2
> 19
> 22
> 6
> ~~~
> {: .source}
>
> the output is:
>
> ~~~
> 10
> 19
> 2
> 22
> 6
> ~~~
> {: .output}
>
> If we run `sort -n` on the same input, we get this instead:
>
> ~~~
> 2
> 6
> 10
> 19
> 22
> ~~~
> {: .output}
>
> Explain why `-n` has this effect.
>
> > ## Solution
> > The `-n` option specifies a numerical rather than an alphanumerical sort.
> {: .solution}
{: .challenge}

We will also use the `-n` option to specify that the sort is
numerical instead of alphanumerical.
This does *not* change the file;
instead, it sends the sorted result to the screen:

~~~
$ sort -n lengths.txt
~~~
{: .language-bash}

~~~
  9  methane.pdb
 12  ethane.pdb
 15  propane.pdb
 20  cubane.pdb
 21  pentane.pdb
 30  octane.pdb
107  total
~~~
{: .output}

We can put the sorted list of lines in another temporary file called `sorted-lengths.txt`
by putting `> sorted-lengths.txt` after the command,
just as we used `> lengths.txt` to put the output of `wc` into `lengths.txt`.
Once we've done that,
we can run another command called `head` to get the first few lines in `sorted-lengths.txt`:

~~~
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n 1 sorted-lengths.txt
~~~
{: .language-bash}

~~~
  9  methane.pdb
~~~
{: .output}

Using `-n 1` with `head` tells it that
we only want the first line of the file;
`-n 20` would get the first 20,
and so on.
Since `sorted-lengths.txt` contains the lengths of our files ordered from least to greatest,
the output of `head` must be the file with the fewest lines.

> ## Redirecting to the same file
>
> It's a very bad idea to try redirecting
> the output of a command that operates on a file
> to the same file. For example:
>
> ~~~
> $ sort -n lengths.txt > lengths.txt
> ~~~
> {: .language-bash}
>
> Doing something like this may give you
> incorrect results and/or delete
> the contents of `lengths.txt`.
{: .callout}

> ## What Does `>>` Mean?
>
> We have seen the use of `>`, but there is a similar operator `>>` which works slightly differently.
> We'll learn about the differences between these two operators by printing some strings.
> We can use the `echo` command to print strings e.g.
>
> ~~~
> $ echo The echo command prints text
> ~~~
> {: .language-bash}
> ~~~
> The echo command prints text
> ~~~
> {: .output}
>
> Now test the commands below to reveal the difference between the two operators:
>
> ~~~
> $ echo hello > testfile01.txt
> ~~~
> {: .language-bash}
>
> and:
>
> ~~~
> $ echo hello >> testfile02.txt
> ~~~
> {: .language-bash}
>
> Hint: Try executing each command twice in a row and then examining the output files.
>
> > ## Solution
> > In the first example with `>`, the string 'hello' is written to `testfile01.txt`,
> > but the file gets overwritten each time we run the command.
> >
> > We see from the second example that the `>>` operator also writes 'hello' to a file
> > (in this case`testfile02.txt`),
> > but appends the string to the file if it already exists (i.e. when we run it for the second time).
> {: .solution}
{: .challenge}

> ## Appending Data
>
> We have already met the `head` command, which prints lines from the start of a file.
> `tail` is similar, but prints lines from the end of a file instead.
>
> Consider the file `data-shell/data/animals.txt`.
> After these commands, select the answer that
> corresponds to the file `animals-subset.txt`:
>
> ~~~
> $ head -n 3 animals.txt > animals-subset.txt
> $ tail -n 2 animals.txt >> animals-subset.txt
> ~~~
> {: .language-bash}
>
> 1. The first three lines of `animals.txt`
> 2. The last two lines of `animals.txt`
> 3. The first three lines and the last two lines of `animals.txt`
> 4. The second and third lines of `animals.txt`
>
> > ## Solution
> > Option 3 is correct.
> > For option 1 to be correct we would only run the `head` command.
> > For option 2 to be correct we would only run the `tail` command.
> > For option 4 to be correct we would have to pipe the output of `head` into `tail -n 2` by doing `head -n 3 animals.txt | tail -n 2 > animals-subset.txt`
> {: .solution}
{: .challenge}

If you think this is confusing,
you're in good company:
even once you understand what `wc`, `sort`, and `head` do,
all those intermediate files make it hard to follow what's going on.
We can make it easier to understand by running `sort` and `head` together:

~~~
$ sort -n lengths.txt | head -n 1
~~~
{: .language-bash}

~~~
  9  methane.pdb
~~~
{: .output}

The vertical bar, `|`, between the two commands is called a **pipe**.
It tells the shell that we want to use
the output of the command on the left
as the input to the command on the right.

Nothing prevents us from chaining pipes consecutively.
That is, we can for example send the output of `wc` directly to `sort`,
and then the resulting output to `head`.
Thus we first use a pipe to send the output of `wc` to `sort`:

~~~
$ wc -l *.pdb | sort -n
~~~
{: .language-bash}

~~~
   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
 107 total
~~~
{: .output}

And now we send the output of this pipe, through another pipe, to `head`, so that the full pipeline becomes:

~~~
$ wc -l *.pdb | sort -n | head -n 1
~~~
{: .language-bash}

~~~
   9  methane.pdb
~~~
{: .output}

This is exactly like a mathematician nesting functions like *log(3x)*
and saying 'the log of three times *x*'.
In our case,
the calculation is 'head of sort of line count of `*.pdb`'.


The redirection and pipes used in the last few commands are illustrated below:

![Redirects and Pipes of different commands: "wc -l *.pdb" will direct the 
output to the shell. "wc -l *.pdb > lengths" will direct output to the file
"lengths". "wc -l *.pdb | sort -n | head -n 1" will build a pipeline where the
output of the "wc" command is the input to the "sort" command, the output of
the "sort" command is the input to the "head" command and the output of the
"head" command is directed to the shell](../fig/redirects-and-pipes.svg)

> ## Piping Commands Together
>
> In our current directory, we want to find the 3 files which have the least number of
> lines. Which command listed below would work?
>
> 1. `wc -l * > sort -n > head -n 3`
> 2. `wc -l * | sort -n | head -n 1-3`
> 3. `wc -l * | head -n 3 | sort -n`
> 4. `wc -l * | sort -n | head -n 3`
>
> > ## Solution
> > Option 4 is the solution.
> > The pipe character `|` is used to connect the output from one command to
> > the input of another.
> > `>` is used to redirect standard output to a file.
> > Try it in the `data-shell/molecules` directory!
> {: .solution}
{: .challenge}


This idea of linking programs together is why Unix has been so successful.
Instead of creating enormous programs that try to do many different things,
Unix programmers focus on creating lots of simple tools that each do one job well,
and that work well with each other.
This programming model is called 'pipes and filters'.
We've already seen pipes;
a **filter** is a program like `wc` or `sort`
that transforms a stream of input into a stream of output.
Almost all of the standard Unix tools can work this way:
unless told to do otherwise,
they read from standard input,
do something with what they've read,
and write to standard output.

The key is that any program that reads lines of text from standard input
and writes lines of text to standard output
can be combined with every other program that behaves this way as well.
You can *and should* write your programs this way
so that you and other people can put those programs into pipes to multiply their power.


> ## Pipe Reading Comprehension
>
> A file called `animals.txt` (in the `data-shell/data` folder) contains the following data:
>
> ~~~
> 2012-11-05,deer
> 2012-11-05,rabbit
> 2012-11-05,raccoon
> 2012-11-06,rabbit
> 2012-11-06,deer
> 2012-11-06,fox
> 2012-11-07,rabbit
> 2012-11-07,bear
> ~~~
> {: .source}
>
> What text passes through each of the pipes and the final redirect in the pipeline below?
>
> ~~~
> $ cat animals.txt | head -n 5 | tail -n 3 | sort -r > final.txt
> ~~~
> {: .language-bash}
> Hint: build the pipeline up one command at a time to test your understanding
> > ## Solution
> > The `head` command extracts the first 5 lines from `animals.txt`.
> > Then, the last 3 lines are extracted from the previous 5 by using the `tail` command.
> > With the `sort -r` command those 3 lines are sorted in reverse order and finally,
> > the output is redirected to a file `final.txt`.
> > The content of this file can be checked by executing `cat final.txt`.
> > The file should contain the following lines:
> > ```
> > 2012-11-06,rabbit
> > 2012-11-06,deer
> > 2012-11-05,raccoon
> > ```
> > {: .source}
> {: .solution}
{: .challenge}

> ## Pipe Construction
>
> For the file `animals.txt` from the previous exercise, consider the following command:
>
> ~~~
> $ cut -d , -f 2 animals.txt
> ~~~
> {: .language-bash}
>
> The `cut` command is used to remove or 'cut out' certain sections of each line in the file,
> and `cut` expects the lines to be separated into columns by a <kbd>Tab</kbd> character.
> A character used in this way is a called a **delimiter**.
> In the example above we use the `-d` option to specify the comma as our delimiter character.
> We have also used the `-f` option to specify that we want to extract the second field (column).
> This gives the following output:
>
> ~~~
> deer
> rabbit
> raccoon
> rabbit
> deer
> fox
> rabbit
> bear
> ~~~
> {: .output}
>
> The `uniq` command filters out adjacent matching lines in a file.
> How could you extend this pipeline (using `uniq` and another command) to find
> out what animals the file contains (without any duplicates in their
> names)?
>
> > ## Solution
> > ```
> > $ cut -d , -f 2 animals.txt | sort | uniq
> > ```
> > {: .language-bash}
> {: .solution}
{: .challenge}

> ## Which Pipe?
>
> The file `animals.txt` contains 8 lines of data formatted as follows:
>
> ~~~
> 2012-11-05,deer
> 2012-11-05,rabbit
> 2012-11-05,raccoon
> 2012-11-06,rabbit
> ...
> ~~~
> {: .output}
>
> The `uniq` command has a `-c` option which gives a count of the
> number of times a line occurs in its input.  Assuming your current
> directory is `data-shell/data/`, what command would you use to produce
> a table that shows the total count of each type of animal in the file?
>
> 1.  `sort animals.txt | uniq -c`
> 2.  `sort -t, -k2,2 animals.txt | uniq -c`
> 3.  `cut -d, -f 2 animals.txt | uniq -c`
> 4.  `cut -d, -f 2 animals.txt | sort | uniq -c`
> 5.  `cut -d, -f 2 animals.txt | sort | uniq -c | wc -l`
>
> > ## Solution
> > Option 4. is the correct answer.
> > If you have difficulty understanding why, try running the commands, or sub-sections of
> > the pipelines (make sure you are in the `data-shell/data` directory).
> {: .solution}
{: .challenge}

## Nelle's Pipeline: Checking Files

Nelle has run her samples through the assay machines
and created 17 files in the `north-pacific-gyre/2012-07-03` directory described earlier.
As a quick check, starting from her home directory, Nelle types:

~~~
$ cd north-pacific-gyre/2012-07-03
$ wc -l *.txt
~~~
{: .language-bash}

The output is 18 lines that look like this:

~~~
300 NENE01729A.txt
300 NENE01729B.txt
300 NENE01736A.txt
300 NENE01751A.txt
300 NENE01751B.txt
300 NENE01812A.txt
... ...
~~~
{: .output}

Now she types this:

~~~
$ wc -l *.txt | sort -n | head -n 5
~~~
{: .language-bash}

~~~
 240 NENE02018B.txt
 300 NENE01729A.txt
 300 NENE01729B.txt
 300 NENE01736A.txt
 300 NENE01751A.txt
~~~
{: .output}

Whoops: one of the files is 60 lines shorter than the others.
When she goes back and checks it,
she sees that she did that assay at 8:00 on a Monday morning --- someone
was probably in using the machine on the weekend,
and she forgot to reset it.
Before re-running that sample,
she checks to see if any files have too much data:

~~~
$ wc -l *.txt | sort -n | tail -n 5
~~~
{: .language-bash}

~~~
 300 NENE02040B.txt
 300 NENE02040Z.txt
 300 NENE02043A.txt
 300 NENE02043B.txt
5040 total
~~~
{: .output}

Those numbers look good --- but what's that 'Z' doing there in the third-to-last line?
All of her samples should be marked 'A' or 'B';
by convention,
her lab uses 'Z' to indicate samples with missing information.
To find others like it, she does this:

~~~
$ ls *Z.txt
~~~
{: .language-bash}

~~~
NENE01971Z.txt    NENE02040Z.txt
~~~
{: .output}

Sure enough,
when she checks the log on her laptop,
there's no depth recorded for either of those samples.
Since it's too late to get the information any other way,
she must exclude those two files from her analysis.
She could delete them using `rm`,
but there are actually some analyses she might do later where depth doesn't matter,
so instead, she'll have to be careful later on to select files using the wildcard expression `*[AB].txt`.
As always,
the `*` matches any number of characters;
the expression `[AB]` matches either an 'A' or a 'B',
so this matches all the valid data files she has.

> ## Wildcard Expressions
>
> Wildcard expressions can be very complex, but you can sometimes write
> them in ways that only use simple syntax, at the expense of being a bit
> more verbose.
> Consider the directory `data-shell/north-pacific-gyre/2012-07-03` :
> the wildcard expression `*[AB].txt`
> matches all files ending in `A.txt` or `B.txt`. Imagine you forgot about
> this.
>
> 1.  Can you match the same set of files with basic wildcard expressions
>     that do not use the `[]` syntax? *Hint*: You may need more than one
>     command, or two arguments to the `ls` command.
>
> 2.  If you used two commands, the files in your output will match the
>     same set of files in this example. What is the small difference between the
>     outputs?
>
> 3.  If you used two commands, under what circumstances would your new
>     expression produce an error message where the original one would not?
>
> > ## Solution
> > 1. A solution using two wildcard commands:
> >     ~~~
> >     $ ls *A.txt
> >     $ ls *B.txt
> >     ~~~
> >     A solution using one command but with two arguments:
> >     ~~~
> >     $ ls *A.txt *B.txt
> >     ~~~
> >     {: .language-bash}
> > 2. The output from the two new commands is separated because there are two commands.
> > 3. When there are no files ending in `A.txt`, or there are no files ending in
> > `B.txt`, then one of the two commands will fail.
> {: .solution}
{: .challenge}

> ## Removing Unneeded Files
>
> Suppose you want to delete your processed data files, and only keep
> your raw files and processing script to save storage.
> The raw files end in `.dat` and the processed files end in `.txt`.
> Which of the following would remove all the processed data files,
> and *only* the processed data files?
>
> 1. `rm ?.txt`
> 2. `rm *.txt`
> 3. `rm * .txt`
> 4. `rm *.*`
>
> > ## Solution
> > 1. This would remove `.txt` files with one-character names
> > 2. This is correct answer
> > 3. The shell would expand `*` to match everything in the current directory,
> > so the command would try to remove all matched files and an additional
> > file called `.txt`
> > 4. The shell would expand `*.*` to match all files with any extension,
> > so this command would delete all files
> {: .solution}
{: .challenge}

---
title: "Loops"
teaching: 40
exercises: 10
questions:
- "How can I perform the same actions on many different files?"
objectives:
- "Write a loop that applies one or more commands separately to each file in a set of files."
- "Trace the values taken on by a loop variable during execution of the loop."
- "Explain the difference between a variable's name and its value."
- "Explain why spaces and some punctuation characters shouldn't be used in file names."
- "Demonstrate how to see what commands have recently been executed."
- "Re-run recently executed commands without retyping them."
keypoints:
- "A `for` loop repeats commands once for every thing in a list."
- "Every `for` loop needs a variable to refer to the thing it is currently operating on."
- "Use `$name` to expand a variable (i.e., get its value). `${name}` can also be used."
- "Do not use spaces, quotes, or wildcard characters such as '*' or '?' in filenames, as it complicates variable expansion."
- "Give files consistent names that are easy to match with wildcard patterns to make it easy to select them for looping."
- "Use the up-arrow key to scroll up through previous commands to edit and repeat them."
- "Use <kbd>Ctrl</kbd>+<kbd>R</kbd> to search through the previously entered commands."
- "Use `history` to display recent commands, and `![number]` to repeat a command by number."
---

**Loops** are a programming construct which allow us to repeat a command or set of commands
for each item in a list.
As such they are key to productivity improvements through automation.
Similar to wildcards and tab completion, using loops also reduces the
amount of typing required (and hence reduces the number of typing mistakes).

Suppose we have several hundred genome data files named `basilisk.dat`, `minotaur.dat`, and
`unicorn.dat`.
For this example, we'll use the `creatures` directory which only has three example files,
but the principles can be applied to many many more files at once.

The structure of these files is the same: the common name, classification, and updated date are
presented on the first three lines, with DNA sequences on the following lines.
Let's look at the files:

```
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```
{: .language-bash}

We would like to print out the classification for each species, which is given on the second
line of each file.
For each file, we would need to execute the command `head -n 2` and pipe this to `tail -n 1`.
We’ll use a loop to solve this problem, but first let’s look at the general form of a loop:

```
for thing in list_of_things
do
    operation_using $thing    # Indentation within the loop is not required, but aids legibility
done
```
{: .language-bash}

and we can apply this to our example like this:

```
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $filename | tail -n 1
> done
```
{: .language-bash}

```
CLASSIFICATION: basiliscus vulgaris
CLASSIFICATION: bos hominus
CLASSIFICATION: equus monoceros
```
{: .output}


> ## Follow the Prompt
>
> The shell prompt changes from `$` to `>` and back again as we were
> typing in our loop. The second prompt, `>`, is different to remind
> us that we haven't finished typing a complete command yet. A semicolon, `;`,
> can be used to separate two commands written on a single line.
{: .callout}

When the shell sees the keyword `for`,
it knows to repeat a command (or group of commands) once for each item in a list.
Each time the loop runs (called an iteration), an item in the list is assigned in sequence to
the **variable**, and the commands inside the loop are executed, before moving on to
the next item in the list.
Inside the loop,
we call for the variable's value by putting `$` in front of it.
The `$` tells the shell interpreter to treat
the variable as a variable name and substitute its value in its place,
rather than treat it as text or an external command.

In this example, the list is three filenames: `basilisk.dat`, `minotaur.dat`, and `unicorn.dat`.
Each time the loop iterates, it will assign a file name to the variable `filename`
and run the `head` command.
The first time through the loop,
`$filename` is `basilisk.dat`.
The interpreter runs the command `head` on `basilisk.dat`
and pipes the first two lines to the `tail` command,
which then prints the second line of `basilisk.dat`.
For the second iteration, `$filename` becomes
`minotaur.dat`. This time, the shell runs `head` on `minotaur.dat`
and pipes the first two lines to the `tail` command,
which then prints the second line of `minotaur.dat`.
For the third iteration, `$filename` becomes
`unicorn.dat`, so the shell runs the `head` command on that file,
and `tail` on the output of that.
Since the list was only three items, the shell exits the `for` loop.

> ## Same Symbols, Different Meanings
>
> Here we see `>` being used a shell prompt, whereas `>` is also
> used to redirect output.
> Similarly, `$` is used as a shell prompt, but, as we saw earlier,
> it is also used to ask the shell to get the value of a variable.
>
> If the *shell* prints `>` or `$` then it expects you to type something,
> and the symbol is a prompt.
>
> If *you* type `>` or `$` yourself, it is an instruction from you that
> the shell should redirect output or get the value of a variable.
{: .callout}

When using variables it is also
possible to put the names into curly braces to clearly delimit the variable
name: `$filename` is equivalent to `${filename}`, but is different from
`${file}name`. You may find this notation in other people's programs.

We have called the variable in this loop `filename`
in order to make its purpose clearer to human readers.
The shell itself doesn't care what the variable is called;
if we wrote this loop as:

~~~
$ for x in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $x | tail -n 1
> done
~~~
{: .language-bash}

or:

~~~
$ for temperature in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $temperature | tail -n 1
> done
~~~
{: .language-bash}

it would work exactly the same way.
*Don't do this.*
Programs are only useful if people can understand them,
so meaningless names (like `x`) or misleading names (like `temperature`)
increase the odds that the program won't do what its readers think it does.

> ## Variables in Loops
>
> This exercise refers to the `data-shell/molecules` directory.
> `ls` gives the following output:
>
> ~~~
> cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> ~~~
> {: .output}
>
> What is the output of the following code?
>
> ~~~
> $ for datafile in *.pdb
> > do
> >     ls *.pdb
> > done
> ~~~
> {: .language-bash}
>
> Now, what is the output of the following code?
>
> ~~~
> $ for datafile in *.pdb
> > do
> >	ls $datafile
> > done
> ~~~
> {: .language-bash}
>
> Why do these two loops give different outputs?
>
> > ## Solution
> > The first code block gives the same output on each iteration through
> > the loop.
> > Bash expands the wildcard `*.pdb` within the loop body (as well as
> > before the loop starts) to match all files ending in `.pdb`
> > and then lists them using `ls`.
> > The expanded loop would look like this:
> > ```
> > $ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > > do
> > >     ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > > done
> > ```
> > {: .language-bash}
> >
> > ```
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > ```
> > {: .output}
> >
> > The second code block lists a different file on each loop iteration.
> > The value of the `datafile` variable is evaluated using `$datafile`,
> > and then listed using `ls`.
> >
> > ```
> > cubane.pdb
> > ethane.pdb
> > methane.pdb
> > octane.pdb
> > pentane.pdb
> > propane.pdb
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

> ## Limiting Sets of Files
>
> What would be the output of running the following loop in the `data-shell/molecules` directory?
>
> ~~~
> $ for filename in c*
> > do
> >     ls $filename
> > done
> ~~~
> {: .language-bash}
>
> 1.  No files are listed.
> 2.  All files are listed.
> 3.  Only `cubane.pdb`, `octane.pdb` and `pentane.pdb` are listed.
> 4.  Only `cubane.pdb` is listed.
>
> > ## Solution
> > 4 is the correct answer. `*` matches zero or more characters, so any file name starting with
> > the letter c, followed by zero or more other characters will be matched.
> {: .solution}
>
> How would the output differ from using this command instead?
>
> ~~~
> $ for filename in *c*
> > do
> >     ls $filename
> > done
> ~~~
> {: .language-bash}
>
> 1.  The same files would be listed.
> 2.  All the files are listed this time.
> 3.  No files are listed this time.
> 4.  The files `cubane.pdb` and `octane.pdb` will be listed.
> 5.  Only the file `octane.pdb` will be listed.
>
> > ## Solution
> > 4 is the correct answer. `*` matches zero or more characters, so a file name with zero or more
> > characters before a letter c and zero or more characters after the letter c will be matched.
> {: .solution}
{: .challenge}

> ## Saving to a File in a Loop - Part One
>
> In the `data-shell/molecules` directory, what is the effect of this loop?
>
> ~~~
> for alkanes in *.pdb
> do
>     echo $alkanes
>     cat $alkanes > alkanes.pdb
> done
> ~~~
> {: .language-bash}
>
> 1.  Prints `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` and `propane.pdb`,
>     and the text from `propane.pdb` will be saved to a file called `alkanes.pdb`.
> 2.  Prints `cubane.pdb`, `ethane.pdb`, and `methane.pdb`, and the text from all three files would be
>     concatenated and saved to a file called `alkanes.pdb`.
> 3.  Prints `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, and `pentane.pdb`, and the text
>     from `propane.pdb` will be saved to a file called `alkanes.pdb`.
> 4.  None of the above.
>
> > ## Solution
> > 1. The text from each file in turn gets written to the `alkanes.pdb` file.
> > However, the file gets overwritten on each loop interation, so the final content of `alkanes.pdb`
> > is the text from the `propane.pdb` file.
> {: .solution}
{: .challenge}

> ## Saving to a File in a Loop - Part Two
>
> Also in the `data-shell/molecules` directory, what would be the output of the following loop?
>
> ~~~
> for datafile in *.pdb
> do
>     cat $datafile >> all.pdb
> done
> ~~~
> {: .language-bash}
>
> 1.  All of the text from `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, and
>     `pentane.pdb` would be concatenated and saved to a file called `all.pdb`.
> 2.  The text from `ethane.pdb` will be saved to a file called `all.pdb`.
> 3.  All of the text from `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb`
>     and `propane.pdb` would be concatenated and saved to a file called `all.pdb`.
> 4.  All of the text from `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb`
>     and `propane.pdb` would be printed to the screen and saved to a file called `all.pdb`.
>
> > ## Solution
> > 3 is the correct answer. `>>` appends to a file, rather than overwriting it with the redirected
> > output from a command.
> > Given the output from the `cat` command has been redirected, nothing is printed to the screen.
> {: .solution}
{: .challenge}

Let's continue with our example in the `data-shell/creatures` directory.
Here's a slightly more complicated loop:

~~~
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
~~~
{: .language-bash}

The shell starts by expanding `*.dat` to create the list of files it will process.
The **loop body**
then executes two commands for each of those files.
The first command, `echo`, prints its command-line arguments to standard output.
For example:

~~~
$ echo hello there
~~~
{: .language-bash}

prints:

~~~
hello there
~~~
{: .output}

In this case,
since the shell expands `$filename` to be the name of a file,
`echo $filename` prints the name of the file.
Note that we can't write this as:

~~~
$ for filename in *.dat
> do
>     $filename
>     head -n 100 $filename | tail -n 20
> done
~~~
{: .language-bash}

because then the first time through the loop,
when `$filename` expanded to `basilisk.dat`, the shell would try to run `basilisk.dat` as a program.
Finally,
the `head` and `tail` combination selects lines 81-100
from whatever file is being processed
(assuming the file has at least 100 lines).

> ## Spaces in Names
>
> Spaces are used to separate the elements of the list
> that we are going to loop over. If one of those elements
> contains a space character, we need to surround it with
> quotes, and do the same thing to our loop variable.
> Suppose our data files are named:
>
> ~~~
> red dragon.dat
> purple unicorn.dat
> ~~~
> {: .source}
>
> To loop over these files, we would need to add double quotes like so:
>
> ~~~
> $ for filename in "red dragon.dat" "purple unicorn.dat"
> > do
> >     head -n 100 "$filename" | tail -n 20
> > done
> ~~~
> {: .language-bash}
>
> It is simpler to avoid using spaces (or other special characters) in filenames.
>
> The files above don't exist, so if we run the above code, the `head` command will be unable
> to find them, however the error message returned will show the name of the files it is
> expecting:
> ```
> head: cannot open ‘red dragon.dat’ for reading: No such file or directory
> head: cannot open ‘purple unicorn.dat’ for reading: No such file or directory
> ```
> {: .output}
> Try removing the quotes around `$filename` in the loop above to see the effect of the quote
> marks on spaces. Note that we get a result from the loop command for unicorn.dat when we run this code in the `creatures` directory:
> ```
> head: cannot open ‘red’ for reading: No such file or directory
> head: cannot open ‘dragon.dat’ for reading: No such file or directory
> head: cannot open ‘purple’ for reading: No such file or directory
> CGGTACCGAA
> AAGGGTCGCG
> CAAGTGTTCC
> ```
> {: . output}
{: .callout}

We would like to modify each of the files in `data-shell/creatures`, but also save a version
of the original files, naming the copies `original-basilisk.dat` and `original-unicorn.dat`.
We can't use:

~~~
$ cp *.dat original-*.dat
~~~
{: .language-bash}

because that would expand to:

~~~
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
~~~
{: .language-bash}

This wouldn't back up our files, instead we get an error:

~~~
cp: target `original-*.dat' is not a directory
~~~
{: .error}

This problem arises when `cp` receives more than two inputs. When this happens, it
expects the last input to be a directory where it can copy all the files it was passed.
Since there is no directory named `original-*.dat` in the `creatures` directory we get an
error.

Instead, we can use a loop:
~~~
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
~~~
{: .language-bash}

This loop runs the `cp` command once for each filename.
The first time,
when `$filename` expands to `basilisk.dat`,
the shell executes:

~~~
cp basilisk.dat original-basilisk.dat
~~~
{: .language-bash}

The second time, the command is:

~~~
cp minotaur.dat original-minotaur.dat
~~~
{: .language-bash}

The third and last time, the command is:

~~~
cp unicorn.dat original-unicorn.dat
~~~
{: .language-bash}

Since the `cp` command does not normally produce any output, it's hard to check
that the loop is doing the correct thing.
However, we learned earlier how to print strings using `echo`, and we can modify the loop
to use `echo` to print our commands without actually executing them.
As such we can check what commands *would be* run in the unmodified loop.

The following diagram
shows what happens when the modified loop is executed, and demonstrates how the
judicious use of `echo` is a good debugging technique.

![The for loop "for filename in *.dat; do echo cp $filename original-$filename;
done" will successively assign the names of all "*.dat" files in your current
directory to the variable "$filename" and then execute the command. With the
files "basilisk.dat", "minotaur.dat" and "unicorn.dat" in the current directory
the loop will successively call the echo command three times and print three
lines: "cp basislisk.dat original-basilisk.dat", then "cp minotaur.dat
original-minotaur.dat" and finally "cp unicorn.dat 
original-unicorn.dat"](../fig/shell_script_for_loop_flow_chart.svg)

## Nelle's Pipeline: Processing Files

Nelle is now ready to process her data files using `goostats` --- a shell script written by her supervisor.
This calculates some statistics from a protein sample file, and takes two arguments:

1. an input file (containing the raw data)
2. an output file (to store the calculated statistics)

Since she's still learning how to use the shell,
she decides to build up the required commands in stages.
Her first step is to make sure that she can select the right input files --- remember,
these are ones whose names end in 'A' or 'B', rather than 'Z'. Starting from her home directory, Nelle types:

~~~
$ cd north-pacific-gyre/2012-07-03
$ for datafile in NENE*[AB].txt
> do
>     echo $datafile
> done
~~~
{: .language-bash}

~~~
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
NENE02043A.txt
NENE02043B.txt
~~~
{: .output}

Her next step is to decide
what to call the files that the `goostats` analysis program will create.
Prefixing each input file's name with 'stats' seems simple,
so she modifies her loop to do that:

~~~
$ for datafile in NENE*[AB].txt
> do
>     echo $datafile stats-$datafile
> done
~~~
{: .language-bash}

~~~
NENE01729A.txt stats-NENE01729A.txt
NENE01729B.txt stats-NENE01729B.txt
NENE01736A.txt stats-NENE01736A.txt
...
NENE02043A.txt stats-NENE02043A.txt
NENE02043B.txt stats-NENE02043B.txt
~~~
{: .output}

She hasn't actually run `goostats` yet,
but now she's sure she can select the right files and generate the right output filenames.

Typing in commands over and over again is becoming tedious,
though,
and Nelle is worried about making mistakes,
so instead of re-entering her loop,
she presses <kbd>↑</kbd>.
In response,
the shell redisplays the whole loop on one line
(using semi-colons to separate the pieces):

~~~
$ for datafile in NENE*[AB].txt; do echo $datafile stats-$datafile; done
~~~
{: .language-bash}

Using the left arrow key,
Nelle backs up and changes the command `echo` to `bash goostats`:

~~~
$ for datafile in NENE*[AB].txt; do bash goostats $datafile stats-$datafile; done
~~~
{: .language-bash}

When she presses <kbd>Enter</kbd>,
the shell runs the modified command.
However, nothing appears to happen --- there is no output.
After a moment, Nelle realizes that since her script doesn't print anything to the screen any longer,
she has no idea whether it is running, much less how quickly.
She kills the running command by typing <kbd>Ctrl</kbd>+<kbd>C</kbd>,
uses <kbd>↑</kbd> to repeat the command,
and edits it to read:

~~~
$ for datafile in NENE*[AB].txt; do echo $datafile; bash goostats $datafile stats-$datafile; done
~~~
{: .language-bash}

> ## Beginning and End
>
> We can move to the beginning of a line in the shell by typing <kbd>Ctrl</kbd>+<kbd>A</kbd>
> and to the end using <kbd>Ctrl</kbd>+<kbd>E</kbd>.
{: .callout}

When she runs her program now,
it produces one line of output every five seconds or so:

~~~
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
~~~
{: .output}

1518 times 5 seconds,
divided by 60,
tells her that her script will take about two hours to run.
As a final check,
she opens another terminal window,
goes into `north-pacific-gyre/2012-07-03`,
and uses `cat stats-NENE01729B.txt`
to examine one of the output files.
It looks good,
so she decides to get some coffee and catch up on her reading.

> ## Those Who Know History Can Choose to Repeat It
>
> Another way to repeat previous work is to use the `history` command to
> get a list of the last few hundred commands that have been executed, and
> then to use `!123` (where '123' is replaced by the command number) to
> repeat one of those commands. For example, if Nelle types this:
>
> ~~~
> $ history | tail -n 5
> ~~~
> {: .language-bash}
> ~~~
>   456  ls -l NENE0*.txt
>   457  rm stats-NENE01729B.txt.txt
>   458  bash goostats NENE01729B.txt stats-NENE01729B.txt
>   459  ls -l NENE0*.txt
>   460  history
> ~~~
> {: .output}
>
> then she can re-run `goostats` on `NENE01729B.txt` simply by typing
> `!458`.
{: .callout}

> ## Other History Commands
>
> There are a number of other shortcut commands for getting at the history.
>
> - <kbd>Ctrl</kbd>+<kbd>R</kbd> enters a history search mode 'reverse-i-search' and finds the
> most recent command in your history that matches the text you enter next.
> Press <kbd>Ctrl</kbd>+<kbd>R</kbd> one or more additional times to search for earlier matches.
> You can then use the left and right arrow keys to choose that line and edit
> it then hit <kbd>Return</kbd> to run the command.
> - `!!` retrieves the immediately preceding command
> (you may or may not find this more convenient than using <kbd>↑</kbd>)
> - `!$` retrieves the last word of the last command.
> That's useful more often than you might expect: after
> `bash goostats NENE01729B.txt stats-NENE01729B.txt`, you can type
> `less !$` to look at the file `stats-NENE01729B.txt`, which is
> quicker than doing <kbd>↑</kbd> and editing the command-line.
{: .callout}

> ## Doing a Dry Run
>
> A loop is a way to do many things at once --- or to make many mistakes at
> once if it does the wrong thing. One way to check what a loop *would* do
> is to `echo` the commands it would run instead of actually running them.
>
> Suppose we want to preview the commands the following loop will execute
> without actually running those commands:
>
> ~~~
> $ for datafile in *.pdb
> > do
> >     cat $datafile >> all.pdb
> > done
> ~~~
> {: .language-bash}
>
> What is the difference between the two loops below, and which one would we
> want to run?
>
> ~~~
> # Version 1
> $ for datafile in *.pdb
> > do
> >     echo cat $datafile >> all.pdb
> > done
> ~~~
> {: .language-bash}
>
> ~~~
> # Version 2
> $ for datafile in *.pdb
> > do
> >     echo "cat $datafile >> all.pdb"
> > done
> ~~~
> {: .language-bash}
>
> > ## Solution
> > The second version is the one we want to run.
> > This prints to screen everything enclosed in the quote marks, expanding the
> > loop variable name because we have prefixed it with a dollar sign.
> >
> > The first version appends the output from the command `echo cat $datafile` 
> > to the file, `all.pdb`. This file will just contain the list; 
> > `cat cubane.pdb`, `cat ethane.pdb`, `cat methane.pdb` etc.
> >
> > Try both versions for yourself to see the output! Be sure to open the
> > `all.pdb` file to view its contents.
> {: .solution}
{: .challenge}

> ## Nested Loops
>
> Suppose we want to set up a directory structure to organize
> some experiments measuring reaction rate constants with different compounds
> *and* different temperatures.  What would be the
> result of the following code:
>
> ~~~
> $ for species in cubane ethane methane
> > do
> >     for temperature in 25 30 37 40
> >     do
> >         mkdir $species-$temperature
> >     done
> > done
> ~~~
> {: .language-bash}
>
> > ## Solution
> > We have a nested loop, i.e. contained within another loop, so for each species
> > in the outer loop, the inner loop (the nested loop) iterates over the list of
> > temperatures, and creates a new directory for each combination.
> >
> > Try running the code for yourself to see which directories are created!
> {: .solution}
{: .challenge}

---
title: "Shell Scripts"
teaching: 30
exercises: 15
questions:
- "How can I save and re-use commands?"
objectives:
- "Write a shell script that runs a command or series of commands for a fixed set of files."
- "Run a shell script from the command line."
- "Write a shell script that operates on a set of files defined by the user on the command line."
- "Create pipelines that include shell scripts you, and others, have written."
keypoints:
- "Save commands in files (usually called shell scripts) for re-use."
- "`bash [filename]` runs the commands saved in a file."
- "`$@` refers to all of a shell script's command-line arguments."
- "`$1`, `$2`, etc., refer to the first command-line argument, the second command-line argument, etc."
- "Place variables in quotes if the values might have spaces in them."
- "Letting users decide what files to process is more flexible and more consistent with built-in Unix commands."
---

We are finally ready to see what makes the shell such a powerful programming environment.
We are going to take the commands we repeat frequently and save them in files
so that we can re-run all those operations again later by typing a single command.
For historical reasons,
a bunch of commands saved in a file is usually called a **shell script**,
but make no mistake:
these are actually small programs.

Let's start by going back to `molecules/` and creating a new file, `middle.sh` which will
become our shell script:

~~~
$ cd molecules
$ nano middle.sh
~~~
{: .language-bash}

The command `nano middle.sh` opens the file `middle.sh` within the text editor 'nano'
(which runs within the shell).
If the file does not exist, it will be created.
We can use the text editor to directly edit the file -- we'll simply insert the following line:

~~~
head -n 15 octane.pdb | tail -n 5
~~~
{: .source}

This is a variation on the pipe we constructed earlier:
it selects lines 11-15 of the file `octane.pdb`.
Remember, we are *not* running it as a command just yet:
we are putting the commands in a file.

Then we save the file (`Ctrl-O` in nano),
 and exit the text editor (`Ctrl-X` in nano).
Check that the directory `molecules` now contains a file called `middle.sh`.

Once we have saved the file,
we can ask the shell to execute the commands it contains.
Our shell is called `bash`, so we run the following command:

~~~
$ bash middle.sh
~~~
{: .language-bash}

~~~
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
~~~
{: .output}

Sure enough,
our script's output is exactly what we would get if we ran that pipeline directly.

> ## Text vs. Whatever
>
> We usually call programs like Microsoft Word or LibreOffice Writer "text
> editors", but we need to be a bit more careful when it comes to
> programming. By default, Microsoft Word uses `.docx` files to store not
> only text, but also formatting information about fonts, headings, and so
> on. This extra information isn't stored as characters, and doesn't mean
> anything to tools like `head`: they expect input files to contain
> nothing but the letters, digits, and punctuation on a standard computer
> keyboard. When editing programs, therefore, you must either use a plain
> text editor, or be careful to save files as plain text.
{: .callout}

What if we want to select lines from an arbitrary file?
We could edit `middle.sh` each time to change the filename,
but that would probably take longer than typing the command out again
in the shell and executing it with a new file name.
Instead, let's edit `middle.sh` and make it more versatile:

~~~
$ nano middle.sh
~~~
{: .language-bash}

Now, within "nano", replace the text `octane.pdb` with the special variable called `$1`:

~~~
head -n 15 "$1" | tail -n 5
~~~
{: .output}

Inside a shell script,
`$1` means 'the first filename (or other argument) on the command line'.
We can now run our script like this:

~~~
$ bash middle.sh octane.pdb
~~~
{: .language-bash}

~~~
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
~~~
{: .output}

or on a different file like this:

~~~
$ bash middle.sh pentane.pdb
~~~
{: .language-bash}

~~~
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
~~~
{: .output}

> ## Double-Quotes Around Arguments
>
> For the same reason that we put the loop variable inside double-quotes,
> in case the filename happens to contain any spaces,
> we surround `$1` with double-quotes.
{: .callout}

Currently, we need to edit `middle.sh` each time we want to adjust the range of 
lines that is returned. 
Let's fix that by configuring our script to instead use three command-line arguments. 
After the first command-line argument (`$1`), each additional argument that we 
provide will be accessible via the special variables `$1`, `$2`, `$3`, 
which refer to the first, second, third command-line arguments, respectively.

Knowing this, we can use additional arguments to define the range of lines to 
be passed to `head` and `tail` respectively:

~~~
$ nano middle.sh
~~~
{: .language-bash}

~~~
head -n "$2" "$1" | tail -n "$3"
~~~
{: .output}

We can now run:

~~~
$ bash middle.sh pentane.pdb 15 5
~~~
{: .language-bash}

~~~
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
~~~
{: .output}

By changing the arguments to our command we can change our script's
behaviour:

~~~
$ bash middle.sh pentane.pdb 20 5
~~~
{: .language-bash}

~~~
ATOM     14  H           1      -1.259   1.420   0.112  1.00  0.00
ATOM     15  H           1      -2.608  -0.407   1.130  1.00  0.00
ATOM     16  H           1      -2.540  -1.303  -0.404  1.00  0.00
ATOM     17  H           1      -3.393   0.254  -0.321  1.00  0.00
TER      18              1
~~~
{: .output}

This works,
but it may take the next person who reads `middle.sh` a moment to figure out what it does.
We can improve our script by adding some **comments** at the top:

~~~
$ nano middle.sh
~~~
{: .language-bash}

~~~
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
head -n "$2" "$1" | tail -n "$3"
~~~
{: .output}

A comment starts with a `#` character and runs to the end of the line.
The computer ignores comments,
but they're invaluable for helping people (including your future self) understand and use scripts.
The only caveat is that each time you modify the script,
you should check that the comment is still accurate:
an explanation that sends the reader in the wrong direction is worse than none at all.

What if we want to process many files in a single pipeline?
For example, if we want to sort our `.pdb` files by length, we would type:

~~~
$ wc -l *.pdb | sort -n
~~~
{: .language-bash}

because `wc -l` lists the number of lines in the files
(recall that `wc` stands for 'word count', adding the `-l` option means 'count lines' instead)
and `sort -n` sorts things numerically.
We could put this in a file,
but then it would only ever sort a list of `.pdb` files in the current directory.
If we want to be able to get a sorted list of other kinds of files,
we need a way to get all those names into the script.
We can't use `$1`, `$2`, and so on
because we don't know how many files there are.
Instead, we use the special variable `$@`,
which means,
'All of the command-line arguments to the shell script'.
We also should put `$@` inside double-quotes
to handle the case of arguments containing spaces
(`"$@"` is special syntax and is equivalent to `"$1"` `"$2"` ...).

Here's an example:

~~~
$ nano sorted.sh
~~~
{: .language-bash}

~~~
# Sort files by their length.
# Usage: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n
~~~
{: .output}

~~~
$ bash sorted.sh *.pdb ../creatures/*.dat
~~~
{: .language-bash}

~~~
9 methane.pdb
12 ethane.pdb
15 propane.pdb
20 cubane.pdb
21 pentane.pdb
30 octane.pdb
163 ../creatures/basilisk.dat
163 ../creatures/minotaur.dat
163 ../creatures/unicorn.dat
596 total
~~~
{: .output}

> ## List Unique Species
>
> Leah has several hundred data files, each of which is formatted like this:
>
> ~~~
> 2013-11-05,deer,5
> 2013-11-05,rabbit,22
> 2013-11-05,raccoon,7
> 2013-11-06,rabbit,19
> 2013-11-06,deer,2
> 2013-11-06,fox,1
> 2013-11-07,rabbit,18
> 2013-11-07,bear,1
> ~~~
> {: .source}
>
> An example of this type of file is given in `data-shell/data/animal-counts/animals.txt`.
>
> We can use the command `cut -d , -f 2 animals.txt | sort | uniq` to produce the unique species in `animals.txt`. In order to avoid having to type out this series of commands every time, a scientist may choose to write a shell script instead.
>
> Write a shell script called `species.sh` that takes any number of
> filenames as command-line arguments, and uses a variation of the above command to print a list of the unique species appearing in each of those files separately.
>
> > ## Solution
> >
> > ```
> > # Script to find unique species in csv files where species is the second data field
> > # This script accepts any number of file names as command line arguments
> >
> > # Loop over all files
> > for file in $@
> > do
> > 	echo "Unique species in $file:"
> > 	# Extract species names
> > 	cut -d , -f 2 $file | sort | uniq
> > done
> > ```
> > {: .source}
> {: .solution}
{: .challenge}


Suppose we have just run a series of commands that did something useful --- for example,
that created a graph we'd like to use in a paper.
We'd like to be able to re-create the graph later if we need to,
so we want to save the commands in a file.
Instead of typing them in again
(and potentially getting them wrong)
we can do this:

~~~
$ history | tail -n 5 > redo-figure-3.sh
~~~
{: .language-bash}

The file `redo-figure-3.sh` now contains:

~~~
297 bash goostats NENE01729B.txt stats-NENE01729B.txt
298 bash goodiff stats-NENE01729B.txt /data/validated/01729.txt > 01729-differences.txt
299 cut -d ',' -f 2-3 01729-differences.txt > 01729-time-series.txt
300 ygraph --format scatter --color bw --borders none 01729-time-series.txt figure-3.png
301 history | tail -n 5 > redo-figure-3.sh
~~~
{: .source}

After a moment's work in an editor to remove the serial numbers on the commands,
and to remove the final line where we called the `history` command,
we have a completely accurate record of how we created that figure.

> ## Why Record Commands in the History Before Running Them?
>
> If you run the command:
>
> ~~~
> $ history | tail -n 5 > recent.sh
> ~~~
> {: .language-bash}
>
> the last command in the file is the `history` command itself, i.e.,
> the shell has added `history` to the command log before actually
> running it. In fact, the shell *always* adds commands to the log
> before running them. Why do you think it does this?
>
> > ## Solution
> > If a command causes something to crash or hang, it might be useful
> > to know what that command was, in order to investigate the problem.
> > Were the command only be recorded after running it, we would not
> > have a record of the last command run in the event of a crash.
> {: .solution}
{: .challenge}

In practice, most people develop shell scripts by running commands at the shell prompt a few times
to make sure they're doing the right thing,
then saving them in a file for re-use.
This style of work allows people to recycle
what they discover about their data and their workflow with one call to `history`
and a bit of editing to clean up the output
and save it as a shell script.

## Nelle's Pipeline: Creating a Script


Nelle's supervisor insisted that all her analytics must be reproducible. The easiest way to capture all the steps is in a script.

First we return to Nelle's data directory:
```
$ cd ../north-pacific-gyre/2012-07-03/
```
{: .language-bash}

She runs the editor and writes the following:

~~~
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datafile
    bash goostats $datafile stats-$datafile
done
~~~
{: .language-bash}

She saves this in a file called `do-stats.sh`
so that she can now re-do the first stage of her analysis by typing:

~~~
$ bash do-stats.sh NENE*[AB].txt
~~~
{: .language-bash}

She can also do this:

~~~
$ bash do-stats.sh NENE*[AB].txt | wc -l
~~~
{: .language-bash}

so that the output is just the number of files processed
rather than the names of the files that were processed.

One thing to note about Nelle's script is that
it lets the person running it decide what files to process.
She could have written it as:

~~~
# Calculate stats for Site A and Site B data files.
for datafile in NENE*[AB].txt
do
    echo $datafile
    bash goostats $datafile stats-$datafile
done
~~~
{: .language-bash}

The advantage is that this always selects the right files:
she doesn't have to remember to exclude the 'Z' files.
The disadvantage is that it *always* selects just those files --- she can't run it on all files
(including the 'Z' files),
or on the 'G' or 'H' files her colleagues in Antarctica are producing,
without editing the script.
If she wanted to be more adventurous,
she could modify her script to check for command-line arguments,
and use `NENE*[AB].txt` if none were provided.
Of course, this introduces another tradeoff between flexibility and complexity.

> ## Variables in Shell Scripts
>
> In the `molecules` directory, imagine you have a shell script called `script.sh` containing the
> following commands:
>
> ~~~
> head -n $2 $1
> tail -n $3 $1
> ~~~
> {: .language-bash}
>
> While you are in the `molecules` directory, you type the following command:
>
> ~~~
> bash script.sh '*.pdb' 1 1
> ~~~
> {: .language-bash}
>
> Which of the following outputs would you expect to see?
>
> 1. All of the lines between the first and the last lines of each file ending in `.pdb`
>    in the `molecules` directory
> 2. The first and the last line of each file ending in `.pdb` in the `molecules` directory
> 3. The first and the last line of each file in the `molecules` directory
> 4. An error because of the quotes around `*.pdb`
>
> > ## Solution
> > The correct answer is 2.
> >
> > The special variables $1, $2 and $3 represent the command line arguments given to the
> > script, such that the commands run are:
> >
> > ```
> > $ head -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
> > $ tail -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
> > ```
> > {: .language-bash}
> > The shell does not expand `'*.pdb'` because it is enclosed by quote marks.
> > As such, the first argument to the script is `'*.pdb'` which gets expanded within the
> > script by `head` and `tail`.
> {: .solution}
{: .challenge}

> ## Find the Longest File With a Given Extension
>
> Write a shell script called `longest.sh` that takes the name of a
> directory and a filename extension as its arguments, and prints
> out the name of the file with the most lines in that directory
> with that extension. For example:
>
> ~~~
> $ bash longest.sh /tmp/data pdb
> ~~~
> {: .language-bash}
>
> would print the name of the `.pdb` file in `/tmp/data` that has
> the most lines.
>
> > ## Solution
> >
> > ```
> > # Shell script which takes two arguments:
> > #    1. a directory name
> > #    2. a file extension
> > # and prints the name of the file in that directory
> > # with the most lines which matches the file extension.
> >
> > wc -l $1/*.$2 | sort -n | tail -n 2 | head -n 1
> > ```
> > {: .source}
> >
> > The first part of the pipeline, `wc -l $1/*.$2 | sort -n`, counts
> > the lines in each file and sorts them numerically (largest last). When
> > there's more than one file, `wc` also outputs a final summary line,
> > giving the total number of lines across _all_ files.  We use `tail
> > -n 2 | head -n 1` to throw away this last line.
> >
> > With `wc -l $1/*.$2 | sort -n | tail -n 1` we'll see the final summary
> > line: we can build our pipeline up in pieces to be sure we understand
> > the output.
> >
> {: .solution}
{: .challenge}

> ## Script Reading Comprehension
>
> For this question, consider the `data-shell/molecules` directory once again.
> This contains a number of `.pdb` files in addition to any other files you
> may have created.
> Explain what each of the following three scripts would do when run as
> `bash script1.sh *.pdb`, `bash script2.sh *.pdb`, and `bash script3.sh *.pdb` respectively.
>
> ~~~
> # Script 1
> echo *.*
> ~~~
> {: .language-bash}
>
> ~~~
> # Script 2
> for filename in $1 $2 $3
> do
>     cat $filename
> done
> ~~~
> {: .language-bash}
>
> ~~~
> # Script 3
> echo $@.pdb
> ~~~
> {: .language-bash}
>
> > ## Solutions
> > In each case, the shell expands the wildcard in `*.pdb` before passing the resulting
> > list of file names as arguments to the script.
> >
> > Script 1 would print out a list of all files containing a dot in their name.
> > The arguments passed to the script are not actually used anywhere in the script.
> >
> > Script 2 would print the contents of the first 3 files with a `.pdb` file extension.
> > `$1`, `$2`, and `$3` refer to the first, second, and third argument respectively.
> >
> > Script 3 would print all the arguments to the script (i.e. all the `.pdb` files),
> > followed by `.pdb`.
> > `$@` refers to *all* the arguments given to a shell script.
> > ```
> > cubane.pdb ethane.pdb methane.pdb octane.pdb pentane.pdb propane.pdb.pdb
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

> ## Debugging Scripts
>
> Suppose you have saved the following script in a file called `do-errors.sh`
> in Nelle's `north-pacific-gyre/2012-07-03` directory:
>
> ~~~
> # Calculate stats for data files.
> for datafile in "$@"
> do
>     echo $datfile
>     bash goostats $datafile stats-$datafile
> done
> ~~~
> {: .language-bash}
>
> When you run it:
>
> ~~~
> $ bash do-errors.sh NENE*[AB].txt
> ~~~
> {: .language-bash}
>
> the output is blank.
> To figure out why, re-run the script using the `-x` option:
>
> ~~~
> bash -x do-errors.sh NENE*[AB].txt
> ~~~
> {: .language-bash}
>
> What is the output showing you?
> Which line is responsible for the error?
>
> > ## Solution
> > The `-x` option causes `bash` to run in debug mode.
> > This prints out each command as it is run, which will help you to locate errors.
> > In this example, we can see that `echo` isn't printing anything. We have made a typo
> > in the loop variable name, and the variable `datfile` doesn't exist, hence returning
> > an empty string.
> {: .solution}
{: .challenge}

---
title: "Finding Things"
teaching: 25
exercises: 20
questions:
- "How can I find files?"
- "How can I find things in files?"
objectives:
- "Use `grep` to select lines from text files that match simple patterns."
- "Use `find` to find files and directories whose names match simple patterns."
- "Use the output of one command as the command-line argument(s) to another command."
- "Explain what is meant by 'text' and 'binary' files, and why many common tools don't handle the latter well."
keypoints:
- "`find` finds files with specific properties that match patterns."
- "`grep` selects lines in files that match patterns."
- "`--help` is an option supported by many bash commands, and programs that can be run from within Bash, to display more information on how to use these commands or programs."
- "`man [command]` displays the manual page for a given command."
- "`$([command])` inserts a command's output in place."
---

In the same way that many of us now use 'Google' as a
verb meaning 'to find', Unix programmers often use the
word 'grep'.
'grep' is a contraction of 'global/regular expression/print',
a common sequence of operations in early Unix text editors.
It is also the name of a very useful command-line program.

`grep` finds and prints lines in files that match a pattern.
For our examples,
we will use a file that contains three haikus taken from a
1998 competition in *Salon* magazine. For this set of examples,
we're going to be working in the writing subdirectory:

~~~
$ cd
$ cd Desktop/data-shell/writing
$ cat haiku.txt
~~~
{: .language-bash}

~~~
The Tao that is seen
Is not the true Tao, until
You bring fresh toner.

With searching comes loss
and the presence of absence:
"My Thesis" not found.

Yesterday it worked
Today it is not working
Software is like that.
~~~
{: .output}

> ## Forever, or Five Years
>
> We haven't linked to the original haikus because they don't appear to be on *Salon*'s site any longer.
> As [Jeff Rothenberg said](https://www.clir.org/wp-content/uploads/sites/6/ensuring.pdf),
> 'Digital information lasts forever --- or five years, whichever comes first.'
> Luckily, popular content often [has backups](http://wiki.c2.com/?ComputerErrorHaiku).
{: .callout}

Let's find lines that contain the word 'not':

~~~
$ grep not haiku.txt
~~~
{: .language-bash}

~~~
Is not the true Tao, until
"My Thesis" not found
Today it is not working
~~~
{: .output}

Here, `not` is the pattern we're searching for. The grep command searches through the file, looking for matches to the pattern specified. To use it type `grep`, then the pattern we're searching for and finally the name of the file (or files) we're searching in.

The output is the three lines in the file that contain the letters 'not'.

By default, grep searches for a pattern in a case-sensitive way. In addition, the search pattern we have selected does not have to form a complete word, as we will see in the next example.

Let's search for the pattern: 'The'.

~~~
$ grep The haiku.txt
~~~
{: .language-bash}

~~~
The Tao that is seen
"My Thesis" not found.
~~~
{: .output}

This time, two lines that include the letters 'The' are outputted,
one of which contained our search pattern within a larger word, 'Thesis'.

To restrict matches to lines containing the word 'The' on its own,
we can give `grep` with the `-w` option.
This will limit matches to word boundaries.

Later in this lesson, we will also see how we can change the search behavior of grep with respect to its case sensitivity.

~~~
$ grep -w The haiku.txt
~~~
{: .language-bash}

~~~
The Tao that is seen
~~~
{: .output}

Note that a 'word boundary' includes the start and end of a line, so not
just letters surrounded by spaces.
Sometimes we don't
want to search for a single word, but a phrase. This is also easy to do with
`grep` by putting the phrase in quotes.

~~~
$ grep -w "is not" haiku.txt
~~~
{: .language-bash}

~~~
Today it is not working
~~~
{: .output}

We've now seen that you don't have to have quotes around single words,
but it is useful to use quotes when searching for multiple words.
It also helps to make it easier to distinguish between the search term or phrase
and the file being searched.
We will use quotes in the remaining examples.

Another useful option is `-n`, which numbers the lines that match:

~~~
$ grep -n "it" haiku.txt
~~~
{: .language-bash}

~~~
5:With searching comes loss
9:Yesterday it worked
10:Today it is not working
~~~
{: .output}

Here, we can see that lines 5, 9, and 10 contain the letters 'it'.

We can combine options (i.e. flags) as we do with other Unix commands.
For example, let's find the lines that contain the word 'the'. We can combine
the option `-w` to find the lines that contain the word 'the' and `-n` to number the lines that match:

~~~
$ grep -n -w "the" haiku.txt
~~~
{: .language-bash}

~~~
2:Is not the true Tao, until
6:and the presence of absence:
~~~
{: .output}

Now we want to use the option `-i` to make our search case-insensitive:

~~~
$ grep -n -w -i "the" haiku.txt
~~~
{: .language-bash}

~~~
1:The Tao that is seen
2:Is not the true Tao, until
6:and the presence of absence:
~~~
{: .output}

Now, we want to use the option `-v` to invert our search, i.e., we want to output
the lines that do not contain the word 'the'.

~~~
$ grep -n -w -v "the" haiku.txt
~~~
{: .language-bash}

~~~
1:The Tao that is seen
3:You bring fresh toner.
4:
5:With searching comes loss
7:"My Thesis" not found.
8:
9:Yesterday it worked
10:Today it is not working
11:Software is like that.
~~~
{: .output}


If we use the `-r` (recursive) option,
`grep` can search for a pattern recursively through a set of files in subdirectories.

Let's search recursively for `Yesterday` in the `data-shell/writing` directory:

```
$ grep -r Yesterday .
```
{: .language-bash}

```
data/LittleWomen.txt:"Yesterday, when Aunt was asleep and I was trying to be as still as a
data/LittleWomen.txt:Yesterday at dinner, when an Austrian officer stared at us and then
data/LittleWomen.txt:Yesterday was a quiet day spent in teaching, sewing, and writing in my
haiku.txt:Yesterday it worked
```
{: .output}

`grep` has lots of other options. To find out what they are, we can type:

~~~
$ grep --help
~~~
{: .language-bash}

~~~
Usage: grep [OPTION]... PATTERN [FILE]...
Search for PATTERN in each FILE or standard input.
PATTERN is, by default, a basic regular expression (BRE).
Example: grep -i 'hello world' menu.h main.c

Regexp selection and interpretation:
  -E, --extended-regexp     PATTERN is an extended regular expression (ERE)
  -F, --fixed-strings       PATTERN is a set of newline-separated fixed strings
  -G, --basic-regexp        PATTERN is a basic regular expression (BRE)
  -P, --perl-regexp         PATTERN is a Perl regular expression
  -e, --regexp=PATTERN      use PATTERN for matching
  -f, --file=FILE           obtain PATTERN from FILE
  -i, --ignore-case         ignore case distinctions
  -w, --word-regexp         force PATTERN to match only whole words
  -x, --line-regexp         force PATTERN to match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline

Miscellaneous:
...        ...        ...
~~~
{: .output}

> ## Using `grep`
>
> Which command would result in the following output:
>
> ~~~
> and the presence of absence:
> ~~~
> {: .output}
>
> 1. `grep "of" haiku.txt`
> 2. `grep -E "of" haiku.txt`
> 3. `grep -w "of" haiku.txt`
> 4. `grep -i "of" haiku.txt`
>
> > ## Solution
> > The correct answer is 3, because the `-w` option looks only for whole-word matches.
> > The other options will also match 'of' when part of another word.
> {: .solution}
{: .challenge}

> ## Wildcards
>
> `grep`'s real power doesn't come from its options, though; it comes from
> the fact that patterns can include wildcards. (The technical name for
> these is **regular expressions**, which
> is what the 're' in 'grep' stands for.) Regular expressions are both complex
> and powerful; if you want to do complex searches, please look at the lesson
> on [our website](http://v4.software-carpentry.org/regexp/index.html). As a taster, we can
> find lines that have an 'o' in the second position like this:
>
> ~~~
> $ grep -E "^.o" haiku.txt
> ~~~
> {: .language-bash}
>
> ~~~
> You bring fresh toner.
> Today it is not working
> Software is like that.
> ~~~
> {: .output}
>
> We use the `-E` option and put the pattern in quotes to prevent the shell
> from trying to interpret it. (If the pattern contained a `*`, for
> example, the shell would try to expand it before running `grep`.) The
> `^` in the pattern anchors the match to the start of the line. The `.`
> matches a single character (just like `?` in the shell), while the `o`
> matches an actual 'o'.
{: .callout}

> ## Tracking a Species
>
> Leah has several hundred
> data files saved in one directory, each of which is formatted like this:
>
> ~~~
> 2013-11-05,deer,5
> 2013-11-05,rabbit,22
> 2013-11-05,raccoon,7
> 2013-11-06,rabbit,19
> 2013-11-06,deer,2
> ~~~
> {: .source}
>
> She wants to write a shell script that takes a species as the first command-line argument
> and a directory as the second argument. The script should return one file called `species.txt`
> containing a list of dates and the number of that species seen on each date.
> For example using the data shown above, `rabbit.txt` would contain:
>
> ~~~
> 2013-11-05,22
> 2013-11-06,19
> ~~~
> {: .source}
>
> Put these commands and pipes in the right order to achieve this:
>
> ~~~
> cut -d : -f 2
> >
> |
> grep -w $1 -r $2
> |
> $1.txt
> cut -d , -f 1,3
> ~~~
> {: .language-bash}
>
> Hint: use `man grep` to look for how to grep text recursively in a directory
> and `man cut` to select more than one field in a line.
>
> An example of such a file is provided in `data-shell/data/animal-counts/animals.txt`
>
> > ## Solution
> >
> > ```
> > grep -w $1 -r $2 | cut -d : -f 2 | cut -d , -f 1,3  > $1.txt
> > ```
> > {: .source}
> >
> > You would call the script above like this:
> >
> > ```
> > $ bash count-species.sh bear .
> > ```
> > {: .language-bash}
> {: .solution}
{: .challenge}

> ## Little Women
>
> You and your friend, having just finished reading *Little Women* by
> Louisa May Alcott, are in an argument.  Of the four sisters in the
> book, Jo, Meg, Beth, and Amy, your friend thinks that Jo was the
> most mentioned.  You, however, are certain it was Amy.  Luckily, you
> have a file `LittleWomen.txt` containing the full text of the novel
> (`data-shell/writing/data/LittleWomen.txt`).
> Using a `for` loop, how would you tabulate the number of times each
> of the four sisters is mentioned?
>
> Hint: one solution might employ
> the commands `grep` and `wc` and a `|`, while another might utilize
> `grep` options.
> There is often more than one way to solve a programming task, so a
> particular solution is usually chosen based on a combination of
> yielding the correct result, elegance, readability, and speed.
>
> > ## Solutions
> > ```
> > for sis in Jo Meg Beth Amy
> > do
> > 	echo $sis:
> >	grep -ow $sis LittleWomen.txt | wc -l
> > done
> > ```
> > {: .source}
> >
> > Alternative, slightly inferior solution:
> > ```
> > for sis in Jo Meg Beth Amy
> > do
> > 	echo $sis:
> >	grep -ocw $sis LittleWomen.txt
> > done
> > ```
> > {: .source}
> >
> > This solution is inferior because `grep -c` only reports the number of lines matched.
> > The total number of matches reported by this method will be lower if there is more
> > than one match per line.
> >
> > Perceptive observers may have noticed that character names sometimes appear in all-uppercase
> > in chapter titles (e.g. 'MEG GOES TO VANITY FAIR').
> > If you wanted to count these as well, you could add the `-i` option for case-insensitivity
> > (though in this case, it doesn't affect the answer to which sister is mentioned most frequently).
> {: .solution}
{: .challenge}

While `grep` finds lines in files,
the `find` command finds files themselves.
Again,
it has a lot of options;
to show how the simplest ones work, we'll use the directory tree shown below.

![A file tree under the directory "writing" contians several sub-directories and
files such that "writing" contains directories "data", "thesis", "tools" and a
file "haiku.txt"; "writing/data" contains the files "Little Women.txt",
"one.txt" and "two.txt"; "writing/thesis" contains the file "empty-draft.md";
"writing/tools" contains the directory "old" and the files "format" and "stats";
and "writing/tools/old" contains a file "oldtool"](../fig/find-file-tree.svg)

Nelle's `writing` directory contains one file called `haiku.txt` and three subdirectories:
`thesis` (which contains a sadly empty file, `empty-draft.md`);
`data` (which contains three files `LittleWomen.txt`, `one.txt` and `two.txt`);
and a `tools` directory that contains the programs `format` and `stats`,
and a subdirectory called `old`, with a file `oldtool`.

For our first command,
let's run `find .` (remember to run this command from the `data-shell/writing` folder).

~~~
$ find .
~~~
{: .language-bash}

~~~
.
./data
./data/one.txt
./data/LittleWomen.txt
./data/two.txt
./tools
./tools/format
./tools/old
./tools/old/oldtool
./tools/stats
./haiku.txt
./thesis
./thesis/empty-draft.md
~~~
{: .output}

As always,
the `.` on its own means the current working directory,
which is where we want our search to start.
`find`'s output is the names of every file **and** directory
under the current working directory.
This can seem useless at first but `find` has many options
to filter the output and in this lesson we will discover some
of them.

The first option in our list is
`-type d` that means 'things that are directories'.
Sure enough,
`find`'s output is the names of the five directories in our little tree
(including `.`):

~~~
$ find . -type d
~~~
{: .language-bash}

~~~
./
./data
./thesis
./tools
./tools/old
~~~
{: .output}

Notice that the objects `find` finds are not listed in any particular order.
If we change `-type d` to `-type f`,
we get a listing of all the files instead:

~~~
$ find . -type f
~~~
{: .language-bash}

~~~
./haiku.txt
./tools/stats
./tools/old/oldtool
./tools/format
./thesis/empty-draft.md
./data/one.txt
./data/LittleWomen.txt
./data/two.txt
~~~
{: .output}

Now let's try matching by name:

~~~
$ find . -name *.txt
~~~
{: .language-bash}

~~~
./haiku.txt
~~~
{: .output}

We expected it to find all the text files,
but it only prints out `./haiku.txt`.
The problem is that the shell expands wildcard characters like `*` *before* commands run.
Since `*.txt` in the current directory expands to `haiku.txt`,
the command we actually ran was:

~~~
$ find . -name haiku.txt
~~~
{: .language-bash}

`find` did what we asked; we just asked for the wrong thing.

To get what we want,
let's do what we did with `grep`:
put `*.txt` in quotes to prevent the shell from expanding the `*` wildcard.
This way,
`find` actually gets the pattern `*.txt`, not the expanded filename `haiku.txt`:

~~~
$ find . -name "*.txt"
~~~
{: .language-bash}

~~~
./data/one.txt
./data/LittleWomen.txt
./data/two.txt
./haiku.txt
~~~
{: .output}

> ## Listing vs. Finding
>
> `ls` and `find` can be made to do similar things given the right options,
> but under normal circumstances,
> `ls` lists everything it can,
> while `find` searches for things with certain properties and shows them.
{: .callout}

As we said earlier,
the command line's power lies in combining tools.
We've seen how to do that with pipes;
let's look at another technique.
As we just saw,
`find . -name "*.txt"` gives us a list of all text files in or below the current directory.
How can we combine that with `wc -l` to count the lines in all those files?

The simplest way is to put the `find` command inside `$()`:

~~~
$ wc -l $(find . -name "*.txt")
~~~
{: .language-bash}

~~~
11 ./haiku.txt
300 ./data/two.txt
21022 ./data/LittleWomen.txt
70 ./data/one.txt
21403 total
~~~
{: .output}

When the shell executes this command,
the first thing it does is run whatever is inside the `$()`.
It then replaces the `$()` expression with that command's output.
Since the output of `find` is the four filenames `./data/one.txt`, `./data/LittleWomen.txt`, `./data/two.txt`, and `./haiku.txt`,
the shell constructs the command:

~~~
$ wc -l ./data/one.txt ./data/LittleWomen.txt ./data/two.txt ./haiku.txt
~~~
{: .language-bash}

which is what we wanted.
This expansion is exactly what the shell does when it expands wildcards like `*` and `?`,
but lets us use any command we want as our own 'wildcard'.

It's very common to use `find` and `grep` together.
The first finds files that match a pattern;
the second looks for lines inside those files that match another pattern.
Here, for example, we can find PDB files that contain iron atoms
by looking for the string 'FE' in all the `.pdb` files above the current directory:

~~~
$ grep "FE" $(find .. -name "*.pdb")
~~~
{: .language-bash}

~~~
../data/pdb/heme.pdb:ATOM     25 FE           1      -0.924   0.535  -0.518
~~~
{: .output}

> ## Matching and Subtracting
>
> The `-v` option to `grep` inverts pattern matching, so that only lines
> which do *not* match the pattern are printed. Given that, which of
> the following commands will find all files in `/data` whose names
> end in `s.txt` but whose names also do *not* contain the string `net`?
> (For example, `animals.txt` or `amino-acids.txt` but not `planets.txt`.)
> Once you have thought about your answer, you can test the commands in the `data-shell`
> directory.
>
> 1.  `find data -name "*s.txt" | grep -v net`
> 2.  `find data -name *s.txt | grep -v net`
> 3.  `grep -v "net" $(find data -name "*s.txt")`
> 4.  None of the above.
>
> > ## Solution
> > The correct answer is 1. Putting the match expression in quotes prevents the shell
> > expanding it, so it gets passed to the `find` command.
> >
> > Option 2 is incorrect because the shell expands `*s.txt` instead of passing the wildcard
> > expression to `find`.
> >
> > Option 3 is incorrect because it searches the contents of the files for lines which
> > do not match 'net', rather than searching the file names.
> {: .solution}
{: .challenge}

> ## Binary Files
>
> We have focused exclusively on finding patterns in text files. What if
> your data is stored as images, in databases, or in some other format?
>
> A handful of tools extend `grep` to handle a few non text formats. But a
> more generalizable approach is to convert the data to text, or
> extract the text-like elements from the data. On the one hand, it makes simple
> things easy to do. On the other hand, complex things are usually impossible. For
> example, it's easy enough to write a program that will extract X and Y
> dimensions from image files for `grep` to play with, but how would you
> write something to find values in a spreadsheet whose cells contained
> formulas?
>
> A last option is to recognize that the shell and text processing have
> their limits, and to use another programming language.
> When the time comes to do this, don't be too hard on the shell: many
> modern programming languages have borrowed a lot of
> ideas from it, and imitation is also the sincerest form of praise.
{: .callout}

The Unix shell is older than most of the people who use it. It has
survived so long because it is one of the most productive programming
environments ever created --- maybe even *the* most productive. Its syntax
may be cryptic, but people who have mastered it can experiment with
different commands interactively, then use what they have learned to
automate their work. Graphical user interfaces may be better at the
first, but the shell is still unbeaten at the second. And as Alfred
North Whitehead wrote in 1911, 'Civilization advances by extending the
number of important operations which we can perform without thinking
about them.'

> ## `find` Pipeline Reading Comprehension
>
> Write a short explanatory comment for the following shell script:
>
> ~~~
> wc -l $(find . -name "*.dat") | sort -n
> ~~~
> {: .language-bash}
>
> > ## Solution
> > 1. Find all files with a `.dat` extension recursively from the current directory
> > 2. Count the number of lines each of these files contains
> > 3. Sort the output from step 2. numerically
> {: .solution}
{: .challenge}
