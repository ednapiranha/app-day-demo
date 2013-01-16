# Playlist App!


## Setup Instructions

1. Create a Github account [http://github.com](http://github.com)
2. Install a github client

        http://windows.github.com/ (Windows)
        http://mac.github.com/ (Mac)

3. Create a new repository called 'playlist' in Github
4. Clone the repository to your local machine
1. Open Firefox
2. Install the Firefox OS Simulator at [https://addons.mozilla.org/en-US/firefox/addon/firefox-os-simulator/](https://addons.mozilla.org/en-US/firefox/addon/firefox-os-simulator/)
3. Install node at [http://nodejs.org](http://nodejs.org)
4. Install volo

        > npm install -g volo

5. Change into a project directory

        > volo create playlist mozilla/mortar-list-detail

6. You'll get two prompts, just press enter for both
7. Open the main html file in Firefox /path/to/your/playlist/www/index.html
8. Run your code editor and open this playlist directory


## Coding the JavaScript part

1. Open playlist/js/app.js and on line 23 paste the following:

        // Match a Youtube url pattern
        var YOUTUBE = /(youtube.com(?:\/#)?\/watch\?)|(youtu\.be\/[A-Z0-9-_]+)/i;

        function generateVideo(url) {
            var youtubeId;

            // If a url pattern is matched, return the iframe - otherwise, return the string
            if (url.match(YOUTUBE)) {
              url = url.split('/');

              // Find the Youtube video id
              if (url.indexOf('youtu.be') > -1) {
                youtubeId = url[url.length - 1];
              } else {
                youtubeId = url[url.length - 1].split('v=')[1].split('&')[0];
              }

              url = '<div class="video-wrapper"><iframe width="560" height="349" ' +
                    'src="http://www.youtube.com/embed/' + youtubeId +
                    '?wmode=transparent" frameborder="0" allowfullscreen></iframe></div>'
            }
            return (url);
        }

2. Around line 49-50 of that same file, you will see three list.add calls. Delete them or comment them out.

3. Do a search for detail.render and change this line:

        $('.title', this).html(item.get('title'));

        to

        $('.title', this).html(generateVideo(item.get('title')));

## Coding the CSS part

1. Open playlist/www/css/app.css
2. Change line 24 to this:

        x-view .contents {
            padding: 1em;
            margin: 0 auto;
            max-width: 560px;
        }

3. Add the following at the end of the file:

        .video-wrapper {
            position: relative;
            padding-bottom: 56.25%; /* 16:9 */
            padding-top: 25px;
            height: 0;
        }

        .video-wrapper iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }


## Update your manifest file

1. Open playlist/www/manifest.webapp
2. Change the name to whatever you want (I have it set to Playlist App), and change the developer information to your name.


## Testing it out in the Firefox OS Simulator

1. Load up the Firefox OS Simulator in Firefox by going to Tools -> Web Developer -> Firefox OS Simulator
2. Click on 'Add Directory' and select playlist/www/manifest.webapp


## Current Known Limitations

Firefox is in the process of supporting h264 so the videos will only play in desktop Firefox if you have Flash installed (for the time being).

## Additional Resources

* [https://developer.mozilla.org/en-US/docs/Apps/App_templates](https://developer.mozilla.org/en-US/docs/Apps/App_templates)
