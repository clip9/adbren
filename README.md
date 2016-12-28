# Description
Hash and renames files based on information from the AniDB API and a user
defined format string. Can also add files to MyList. Run adbren.pl without
arguments for full usage information. 

# URL
adbren has a permanent home on github:
[http://github.com/clip9/adbren](http://github.com/clip9/adbren "Github adbren")

# Install / Configuration
Clone the git repository or download a copy, then execute the adbren.pl script. 
It will ask you for your user name and password to [anidb](http://anidb.net/ "AniDB"). 
This configuration is stored in *~/.adbren.config*. Delete this file and 
execute adbren.pl to rerun the configuration.

# Usage
	adbren.pl [options] <file1/dir1> [file2/dir2] ...

# Options
        --format        Format. Default is preset 0
        --preset        Format preset number. See list below;
        --strict        Use stricter cleaning. Only allow [a-Z0-9._]
        --noclean       Do not clean values of format vars. 
                        (Don't remove spaces, etc.7)
        --norename      Do not rename files. Just print the new names.
        --mylist        Add hashed files to mylist.
        --onlyhash      Only print ed2k hashes. 
        --nocorrupt     Don't rename "corrupt" files. (Files not found in AniDB)
        --logfile       Log files renamed to this file. Default: ~/adbren.log
                        This log is used to avoid hashing files already processed.
        --noskip        Do not skip files found in the log.
        --nolog         Do not do any logging.
        --debug         Debug mode.

# Format variables
        %fid%, %aid%, %eid%, %gid%, %lid%, %status%, %size%, %ed2k%, 
        %md5%, %sha1%, %crc32%, %lang_dub%, %lang_sub%, %quaility%, %source%, 
        %audio_codec%, %audio_bitrate%, %video_codec%, %video_bitrate%,
        %resolution%, %filetype%, %length%, %description%, %group%, 
        %group_short%, %episode%, %episode_name%, %episode_name_romaji%,
        %episode_name_kanji%, %episode_total%, %episode_last%, %anime_year%,
        %anime_type%, %anime_name_romaji%, %anime_name_kanji%, 
        %anime_name_english%, %anime_name_other%, %anime_name_short%, 
        %anime_synonyms%, %anime_category%, %version%, %censored%,
        %orginal_name%

# Notes
Directories on the command line are scanned recursively. Files are renamed in the same directory.

# Format Presets
	0. %anime_name_english%_%episode%%version%-%group_short%.%filetype%
	1. %anime_name_english%_%episode%%version%_%episode_name%-%group_short%.%filetype%
	2. %anime_name_english%_%episode%%version%_%episode_name%-%group_short%(%crc32%).%filetype%
	3. %anime_name_english% - %episode% - %episode_name% - [%group_short%](%crc32%).%filetype%

# Tips & Tricks
You can use an absolute or relative path in the format parameter like this:
```shell
	./adbren.pl --format /mnt/raid/%anime_name_english%/%episode%.%filetype%
	./adbren.pl --format %anime_name_english%/%episode%.%filetype%
```
In the second example the target path is relative to the current 
directory not the the directory where the file currently is.
