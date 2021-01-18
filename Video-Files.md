There are a few methods for accessing video files.

Files remain on the comma device until they are uploaded or automatically deleted.
Use the following links to gain an understanding of what video segment(s) are needed:
* [Comma Explorer](https://my.comma.ai)
* [Comma Explorer User Admin](https://my.comma.ai/useradmin)   (for preserving segments)
Use the Download Camera Segment and/or Copy Current Segment buttons to identify the segment timestamp info.
The timestamp is copied to your clipboard as text.

[FTP](#FTP)  
[SSH](#SSH)  
[Cabana](#Cabana)  

# FTP
Requires a Github account, making encryption keys, enabled SSH on the device, and installing a SFTP client on your computer

Software SFTP Clients (Host Name = IP Address, Port 8022, Username root)
* [Filezilla](https://filezilla-project.org/)
* [WinSCP](https://sourceforge.net/projects/winscp/)

Once connected, start in path
```
/sdcard/realdata/
```
The segment timestamp identified above will match a subfolder name. Download the target .hevc file, and surrounding .hevc files as desired. Name them in some sensical manner. They can be drag-and-dropped into a VLC window to play, but each file's timestamps/tracking may be incorrect until processed.

To combine multiple segments (if needed), use this linux command:
```
cat fcamera1.hevc fcamera2.hevc fcamera3.hevc > output.hevc 
```
or this Windows command
```
copy /b fcamera1.hevc+fcamera2.hevc+fcamera3.hevc output.hevc
```
The output.hevc file can be uploaded to YouTube straight away for processing, or played in VLC. But many others won’t know what to do with a .hevc file. So if sending, then [download ffmpeg](https://ffmpeg.org/download.html) and convert it first. To make a .mpg copy for emailing etc., put the output.hevc file in the same folder as the ffmpeg program, then run a command like 
```
ffmpeg -I output.hevc -qscale:v 1 output.mpg
```
After which, the .hevc file could be used for YouTube or some limited purposes in VLC, else can be shared as a more recognizable .mpg file.

# SSH

# Cabana