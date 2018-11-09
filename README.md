# CSS Grid Layout Generator

> A Vue.js project

# [Demo](http://vuejs.github.io/vue-loader)
[Grid layout trenager](http://vuejs-templates.github.io/webpack/)

# How to use

``` bash
# step 1
Write the container fields:
	grid-template-columns: ;
	grid-template-rows: ;
	grid-gap: ;
Use [px, %, fr, em, auto, min-content, max-content, minmax] props.

Warning! Do not use repeat(n, %) props.

# step 2
Write the number of blocks

Warning! Do not write more than the maximum number.

# step 3
Manipulate children by choosing green blocks.

write the items№ fields:
	grid-column: ;
	gird-row: ;
	order: ;
Use [n-start/n-end] props and number odder.

# step 4 
Get code.
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
