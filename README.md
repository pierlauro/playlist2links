# Playlist To Links

This bash script allows to extract video links from a YouTube playlist.

# Dependencies
The script requires [wget](https://www.gnu.org/software/wget/) or [curl](http://curl.haxx.se/) and the basic GNU utils.

# Usage
Playlist: `https://www.youtube.com/playlist?list=123CODEOFPLAYLIST`

    ./playlist2links 123CODEOFPLAYLIST

or

    ./playlist2links 123CODEOFPLAYLIST withnames

The list of YouTube playlist's links is now saved in `playlist_123CODEOFPLAYLIST.txt` (one per line).

If the `withnames` argument is used, each link will be followed the video's name.

(Due to recent Youtube changes, `Playlist2Links v4.0-beta` is supporting up to 100 videos. Support for longer playlists will be added in the future stable version).
