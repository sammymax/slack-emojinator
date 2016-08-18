# Slack Emojinator

*Bulk upload emoji into Slack*

Want to create a custom Slack emoji for every pokemon? Slack doesn't currently expose an API endpoint for creating emoji, probably to prevent users from doing exactly what I'm doing, but here's a way to do it anyway.

## Creating Emoji

You'll need Python and `pip` to get started. I recommend using [virtualenv](https://virtualenv.pypa.io/en/latest/) and possibly [virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/) as well. Standard best-practice Python stuff.

Prepare a directory that contains an image for each emoji you want to create. Remember to respect Slack's specifications for valid emoji images: no greater than 128px in width or height, no greater than 64K in image size. The base filename of each image file should be the name of the emoji (the bit you'll type inside `:` to display it).

Clone the project, create a new virtualenv, and install the prereqs:

```bash
git clone https://github.com/sammymax/slack-emojinator.git
cd slack-emojinator
mkvirtualenv slack-emojinator
pip install -r requirements.txt
```

Now, you need to get your Slack session cookie, needed for the python script to authenticate and upload emojis:
* Go to https://{teamname}.slack.com/customize/emoji and then [open your browser's dev tools](http://webmasters.stackexchange.com/a/77337)
* Go to the Network tab, then reload the page
* Find call to `emoji` (it is most likely the very top request)
* Scroll to `Request-Headers` and copy the value of Cookie

Now, you're ready to run the python script. `TEAM_NAME` is the bit before ".slack.com" in the url, and `SESSION_COOKIE` is what you just copied.


```bash
python upload.py ${TEAM_NAME} ${SESSION_COOKIE} ${EMOJI_DIR}/*.png
```

Remember to put quotes around the cookie! Otherwise spaces in the cookie string will screw up python.
:sparkles:
