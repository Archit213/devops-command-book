# Vi Editor Management
------------------------------------------------------------------------

# Table of Contents

-   What is Vi?
-   Vi Modes
-   Command Reference
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# What is Vi?

**Vi** is a terminal-based text editor available on almost every Unix
and Linux system. It is commonly used by system administrators and
DevOps engineers to edit configuration files, shell scripts, service
definitions, and application settings directly on servers.

------------------------------------------------------------------------

# Why Learn Vi?

-   Installed by default on most Linux distributions.
-   Ideal for remote server administration over SSH.
-   Lightweight and does not require a graphical interface.
-   Commonly used to edit files under `/etc`, `/var`, and other system
    locations.

------------------------------------------------------------------------

# Vi Modes

  -----------------------------------------------------------------------
  Mode                         Purpose
  ---------------------------- ------------------------------------------
  Command Mode                 Default mode used for navigation and
                               editing commands.

  Insert Mode                  Used to type and modify text.

  Last-Line Mode               Used to save, quit, search, and execute
                               editor commands beginning with `:`.
  -----------------------------------------------------------------------

Mode transitions:

``` text
Command Mode
   │
   ├── i ─────────► Insert Mode
   │                  │
   │                  └── ESC ─────► Command Mode
   │
   └── :w / :q / :wq ─► Last-Line Commands
```

------------------------------------------------------------------------

# Command Reference

## 1. Open or Create a File

``` bash
vi file.html
```

**Description:** Opens an existing file or creates a new file if it does
not exist.

**Example**

``` bash
vi index.html
```

------------------------------------------------------------------------

## 2. Enter Insert Mode

``` text
i
```

**Description:** Switches from Command Mode to Insert Mode so you can
type text.

------------------------------------------------------------------------

## 3. Return to Command Mode

``` text
ESC
```

**Description:** Exits Insert Mode and returns to Command Mode.

------------------------------------------------------------------------

## 4. Delete Current Line

``` text
dd
```

**Description:** Deletes the entire line where the cursor is positioned.

------------------------------------------------------------------------

## 5. Delete a Word

``` text
dit
```

**Description:** Deletes the current word or targeted text object (as
referenced in your notes).

------------------------------------------------------------------------

## 6. Copy a Line

``` text
yy
```

**Description:** Copies (yanks) the current line into memory.

------------------------------------------------------------------------

## 7. Paste

``` text
p
```

**Description:** Pastes copied or deleted text below the cursor.

------------------------------------------------------------------------

## 8. Scroll Pages

``` text
Ctrl + f
Ctrl + b
```

**Description:** Scroll forward or backward one full page.

------------------------------------------------------------------------

## 9. Save File

``` text
:w
```

**Description:** Saves the current file without exiting.

------------------------------------------------------------------------

## 10. Quit Editor

``` text
:q
```

**Description:** Exits Vi if there are no unsaved changes.

------------------------------------------------------------------------

## 11. Save and Quit

``` text
:wq
```

**Description:** Saves all changes and exits the editor.

------------------------------------------------------------------------

## 12. Save with a New Name

``` text
:w filename
```

**Description:** Saves the current buffer to a different filename.

**Example**

``` text
:w backup.conf
```

------------------------------------------------------------------------

# Practical Exercises

## Exercise 1 -- Create a File

``` bash
vi notes.txt
```

Press:

``` text
i
```

Type:

``` text
Linux Commands
Vi Editor Basics
```

Press:

``` text
ESC
```

Save and quit:

``` text
:wq
```

------------------------------------------------------------------------

## Exercise 2 -- Delete and Paste

1.  Open a file with multiple lines.
2.  Move to a line.
3.  Press:

``` text
dd
```

4.  Paste it below:

``` text
p
```

------------------------------------------------------------------------

## Exercise 3 -- Save As

``` text
:w backup.txt
```

This creates another file with the same contents.

------------------------------------------------------------------------

# Best Practices

-   Always press `ESC` before entering command sequences.
-   Save frequently with `:w`.
-   Use `:wq` when finished editing.
-   Practice navigation before editing production files.

------------------------------------------------------------------------

# Common Mistakes

-   Forgetting to press `i` before typing.
-   Trying to type while still in Command Mode.
-   Attempting `:q` when unsaved changes exist.
-   Forgetting `ESC` before issuing editor commands.

------------------------------------------------------------------------

# Interview Questions

### Why is Vi important for DevOps?

Because it is available on nearly every Linux server and is commonly
used to edit configuration files over SSH.

### Difference between `:q` and `:wq`

-   `:q` quits the editor.
-   `:wq` saves changes and then quits.

### What does `yy` do?

Copies the current line into the editor buffer.

------------------------------------------------------------------------

# Summary

You learned:

-   Vi editor basics
-   Command, Insert, and Last-Line modes
-   Opening, editing, saving, and quitting files
-   Copying, deleting, and pasting text
-   Practical editing workflows
-   Best practices and interview concepts
