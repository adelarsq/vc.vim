# vc.vim

VIM (VIM 7 and up) plugin for subversion (svn), GIT, HG and BZR repositories.
Support for browsing the repository, working copy, bookmarks.
Autocompletes command options, file(s), dir(s), repo url(s)

**NOTE**: svnj.vim users, replace all settings from svnj_ to vc_ 

![Animation][1]
   
[1]: http://i.imgur.com/i5B696t.gif?1

##Supported Operations

* **VCAdd[!] [Arguments]**
    Add and Commit File(s)/Directories to repository. VCAdd is supported as a command and also as an
    operation from VCStatus and VCBrowse output. Available options are to add or add and then commit.

    **For:** SVN, GIT, HG, BZR

* **VCCommit[!] [Arguments]**
    Performs commit. A new buffer will be opened to accept comments. The buffer will list
    the files which are candidates for commit. Files/Directories can also be updated in this buffer. 
    A commit can be forced with no comments with a bang. VCCommit is supported as a command and 
    also as an operation from the VCStatus|VCBrowseWorkingCopy|VCBrowseBuffer output window. 

    **For:** SVN, GIT, HG, BZR

* **VCBlame [Arguments]**
    Vertically splits the blame info for the file in bufffer. Scrollbinds to the file.
    
    **For:** SVN, GIT, HG, BZR

* **VCStatus [Arguments]**
    Get the output of status command. With the listed files in the split buffer which states the filename
    and status, the following are few of the operations supported

      - Open file under cursor or all 
      - Info,  Diff, Log
      - Commit selected/marked files
      - Add selected/marked files 
      - Bookmark
      
    **For:** SVN, GIT, HG, BZR

* **VCLog [Arguments]**
    Lists the log for the current file in buffer.  The output displays the revision, author, comments 
    and the revision when the branch was created. With the revisions listed, diff the required 
    revisions with the file in buffer. Also provides mechanism to diff the file across branches/trunk. 
    A menu will be displayed to list revisions from available branches and trunk. 

    - Diff revision(s) from current working copy or across branches/trunk
    - List Affected/Modified files for the revision or across revisions (most useful with dirs)
    - Diff :HEAD | :PREV  with selected revision (most useful with dirs only SVN)
    - Open marked revisons or revison under cursor as new file - newbuffer or vspilt
    - View Info and Log of revision
    
    **For:** SVN, GIT, HG, BZR

* **VCDiff [Arguments]**
    Immediate diff the file in buffer with the previous/specified revision. If there are more than one file in 
    buffer Ctrl-n/Ctrl-p will close the current diff and move to the next/prev file in buffer. 
    Ctrl-Up and Ctrl-Dowm will move across revisions for the same file

    **For:** SVN, GIT, HG, BZR

* **VCInfo [Arguments]**
    Will display repository info.
    **For:** SVN, GIT, HG, BZR

* **VCCopy[!] [Arguments]**
    Copy files (repo or local)

    **For:** SVN, HG

* **VCMove [Arguments]**
     Move files. The buffer will be auto reloaded

     **For:** SVN, GIT, HG

* **VCRevert[!]**
     Revert to the latest revision, operates on the file in buffer. ! causes the buffer to auto reload
     
     **For:** SVN, GIT, HG, BZR

* **VCFetch**
     Fetch from repo (applicable for git only), auto completes available branches and options
     
     **For:** GIT, HG, BZR

* **VCPull**
     Pull from repo (applicabe for git, hg, bzr), auto completes available branches and options
     
     **For:** GIT, HG, BZR
      
* **VCPush**
     Push to repo (applicabe for git, hg, bzr), auto completes available branches and options
     
     **For:** GIT, HG, BZR
     
* **VCIncoming**
     HG Incoming

     **For:** applicable for HG only

* **VCOutgoing**
     HG Outgoing

     **For:** applicable for HG only

* **VCDefaultrepo**
    Set a default repo when a project belongs in more than one repository

* **VCBrowse**
   Browse the working copy files (files, buffers, favorites, bookmarks) and **repository(SVN only)**

     - VCBrowse
         This command brings up a menu of available options for browsing.
     - VCBrowseRepo [Arguments[
         Only on **SVN repo**
         This command lists files/directories from the repository. The current directory should be 
         a working copy for the plugin to pick up the SVN path or pass SVN url or autocomplete from
         the SVN urls from within the working dir
     - VCBrowseWorkingCopy [<dir>]
         This command lists files/directories from the current directory. 
     - VCBrowseMyList
         This command lists files/directories specified using g:vc_browse_mylist see 
         :help g:vc_browse_mylist 
     - VCBrowseBookMarks
           While browsing the repo/working copy you can bookmarks the dir/files 
           All of the book marked files will be listed as output. 
           These bookmarked files/dirs are available only for the current vim session unless caching 
           is enabled, Once vim is closed all bookmarks are lost if caching is not enabled.
     -VCBrowseBuffer
           List the files from Buffer

     Cache for browsing:
         The caching feature is **off by default**, On enabling the caching the listing of files for 
     VCBrowseRepo and VCBrowseWorkingCopy will be faster. There are many levels at which the caching
     can be enabled **see help:g:vc_cache_dir**

    Some of the operations supported are
      - Recursive/Non-recursive listing of files from directory
      - Navigate up/down the directory, Jump to Respository Root/Working Root/Home where applicable
      - Open file(s) in new buffer or vertical split
      - Copy/Move files/dirs , (Repo or Local)
      - View Info, Log
      - Add, Commit
      - Checkout **(svn only)**
    
      - Bookmark the dir/file. To persist the bookmarks across sessions see :help g:vc_browse_bookmarks_cache

* **VCClearCache**
     The cache/persistency is not enabled by default. please see :help VCClearCache for more info.

##Filter/PROMPT

Has following modes, see help vc-filter for examples

1. **FUZZY** : Performs fuzzy search by default.
           Toggle using global options or on the fly using & as suffix. See examples in help

2. **ARGS**   : Accepts arguments to command executed from browse output, 
            Toggle using key, use ? at filter to see the key

3. **VER**    : When opening files for affected mode, when on, opens corresponding
            versioned file, when off opens local file
            Toggle using key, use ? at filter to see the key

4. **STICKY** : Have the filter/prompt as sticky when enabled
            Toggle using key, use ? at filter to see the key

Operations:

1. **Sort**  : Sort the ouput on key <F8>, If o/p has date will sort on date else the contents

##Global Options  :help vc-options and :help vc-customize

 +  g:vc_max_logs, g:vc_max_open_files, g:vc_max_diff,
    g:vc_window_max_size, g:vc_warn_branch_log, g:vc_browse_max_files_cnt,
    g:vc_browse_repo_max_files, g:vc_send_soc_command
    g:vc_donot_confirm_cmd, 

 + g:vc_browse_cache_all, g:vc_browse_bookmarks_cache, g:vc_browse_repo_cache,
   g:vc_browse_workingcopy_cache, g:vc_browse_cache_max_cnt, g:vc_cache_dir

 + g:vc_signs, g:vc_ignore_files, g:vc_ignore_repos

 + g:vc_browse_mylist
 + g:vc_log_name, g:Hvc_default_repo

 + g:vc_branch_url, g:vc_trunk_url (svn only)
 + g:vc_username, g:vc_password (svn only)
 
 + g:vc_prompt_args, g:vc_sticky_on_start, 
 
 + g:vc_fuzzy_search, g:vc_fuzzy_search_result_max

 + g:vc_custom_fuzzy_match_hl, g:vc_custom_menu_color, g:vc_custom_error_color,
   g:vc_custom_prompt_color, g:vc_custom_statusbar_hl, g:vc_custom_statusbar_title
   g:vc_custom_statusbar_title, g:vc_custom_statusbar_ops_hl, 
   g:vc_custom_statusbar_sel_hl, g:vc_custom_info_color
   g:vc_custom_sticky_hl, g:vc_custom_commit_files_hl, g:vc_custom_commit_header_hl


##Recomended settings at .vimrc

let g:vc_browse_cache_all = 1
    This enables caching, Listing of files will be faster, On MAC/Unix the default location is $HOME/.cache.
    A new directory vc will be created in the specified directory.

    For windows this option must be specified along with the cache dir
    let g:vc_cache_dir="C:/Users/user1"

let g:vc_branch_url = ["svn://127.0.0.1/Path/until/branches/", "svn://127.0.0.1/Path/until/tags/"]
    This settings when available will provide menu's to navigate available branches and tags for VCLog

let g:vc_trunk_url = "svn://127.0.0.1/Path/until/trunk";
    This settings when available will provide menu's to navigate trunk files for VCLog

##Installation

###Options 1:  (Pathogen Users)

1. cd ~/.vim/bundle
2. git clone https://github.com/juneedahamed/vc.vim


##Basic Usage

Run from vim commandline

- `:VCBlame`
- `:VCDiff`
- `:VCLog`
- `:VCStatus`
- `:VCCopy`
- `:VCMove`
- `:VCRevert`
- `:VCCommit`
- `:VCCommits`
- `:VCAdd`
- `:VCIncoming`
- `:VCOutgoing`
- `:VCFetch`
- `:VCPull`
- `:VCPush`
- `:VCBrowse`
- `:VCBrowseWorkingCopy`
- `:VCBrowseRepo`
- `:VCBrowseBookMarks`
- `:VCBrowseMyList`
- `:VCBrowseBuffer`
- **`:help vc`**




