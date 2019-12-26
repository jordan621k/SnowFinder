# snow-finder

## deploy to GitHub.io
1) Find and open the file `.gitignore` located in root directory of your project. Next, find and comment the line which has the text `/dist`.
NOTE: this folder it’s ignored by default that’s why we have to comment it.

2) Run `npm run build`, and wait for it to finish.

3) IMPORTANT!! Before you run the next command make sure you don’t commit the `.gitignore` and `vue.config.js`.
- Run the command: `git add dist && git commit -m "Initial dist subtree commit"`
- Run the command: `git subtree push --prefix dist origin gh-pages`

**Force Push** git push origin `git subtree split --prefix dist master`:gh-pages --force

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
