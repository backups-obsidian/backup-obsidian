---
created: 2022-04-13 22:02
updated: 2022-04-13 22:48
---
## What will I do?
For syncing notes I will be creating a hard link and then initialising a git repository in the folder containing the hard link.
## Why?
- I don't want to initialise a `.git` repository in my `.obsidian` folder. 
- Further more I want to sync `.obsidian` folder as a whole and not its individual components so that it will be easier for my to just replace the folder
- Even though my notes will be backed up with Google Drive which will also backup the `.obsidian` folder, it won't be easy to share my settings with others.

## Step/Commands
- Clone the new git repository
- Run the following command to create a hard link
```bash
cp -a "/Users/sarthaknarayan/Documents/Obsidian vault/main/.obsidian/." obsidian-settings/
```

- test
- 
- [ ] this 
- [ ] sdfs

