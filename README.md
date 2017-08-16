# Playlist To Links

This bash script allows to extract video links from a YouTube playlist.

# Dependencies
The script requires [wget](https://www.gnu.org/software/wget/) or [curl](http://curl.haxx.se/).

# Usage
Playlist: `https://www.youtube.com/playlist?list=123CODEOFPLAYLIST`

    ./playlist2links 123CODEOFPLAYLIST

or

    ./playlist2links 123CODEOFPLAYLIST withnames

The list of YouTube playlist's links is now saved in `playlist_123CODEOFPLAYLIST.txt`.

If the `withnames` argument is used, then each link will be preceeded by the video's name.
