# Start using a Jekyll theme in your website

## Step 1: clone your website files

In a terminal, go to where you store your projects. For example to go to "Documents", do

```bash
cd ~/Documents
```

Then you will clone your website into your home computer. You can make changes, but not push (publish) until we set up permissions with SSH keys later.

```bash
git clone git@github.com:NAHLN/ngs-resources.git
```

The will create "ngs-resources" inside "Documents".

## Step 2: Download the starter files for the theme.

Go to https://github.com/mmistakes/mm-github-pages-starter and find the green button. Click to reveal a pulldown box with the selected
tab as "Local". Click the link at the bottom "Download ZIP".  You can put it anywhere, just make sure you can find it in Finder!

Once downloaded, unzip by double clicking. This will expand a new folder with the name *mm-github-pages-starter-master*.

## Step 3: copy the starter files into your website folder

In a new Finder window, go to your website folder, e.g. "Documents/ngs-resources" if you put it in your Documents folder. Now, drag and drop all of the files from *mm-github-pages-starter-master* into ngs-resources. It will ask about replacing or skipping _config.yml and README.md.  It's OK to replace them.

## Step 4: Use VS Code

Open VS-Code, then do File -> Open Folder and find *ngs-resources*. Use the terminal pane to continue.

## Step 5: Build the template site

In the terminal pane, do these commands:

```bash
  gem install bundler
  bundle install
  bundle exec jekyll serve
```
If successful, the site will be live on your computer. Go to ` http://127.0.0.1:4000/ngs-resources/` to view it.

## Step 6: Make your first change

In VS Code, open _config.yml. This is a YAML file (Yet Another Markdown Language).

Find the fields `title`, `url`, `baseurl`, and `repository` and change them like so (they won't be grouped together):

```yaml
  title: "NGS Resources"
  url: "https://NAHLN.github.io"
  baseurl: "/ngs-resources"
  repository: "NAHLN/ngs-resources"
```

## Step 7: Restart server

When changes are made to configuration files, we need to restart the server. When changes are made to content documents you won't need to restart.

### To stop:

```bash
ctrl-c
```

### To restart

(you can use the arrow keys <kbd>↑</kbd> to scroll through previous commands)

```bash
bundle exec jekyll serve
```

## Ready!

You should see your new title in the upper left of the website!