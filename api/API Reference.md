---
tags: api, stimstore
---
NOTE: If this file is not rendering a full table of APIs, please ensure [dataview](https://github.com/blacksmithgu/obsidian-dataview) is correctly installed and enabled. The easiest way to do this is by trusting the vault and enabling its plugins. This will also give you access to correctly viewing the embedded excalidraw [[highlevel.excalidraw|architecture]] 

I have no idea why the tables are rendered differently, I need to look into that #todo

```dataviewjs

const cols = ["File", "Route", "Desc"]

const rows = dv.pages("#api")
	.sort(api => api.file.frontmatter.route)
	.sort(api => api.file.name)
	.filter(api => api.file.name !== "API Reference" && api.file.name !== "API Template")
	.array()

const data = rows.reduce((acc, current) => {
	if (acc[current.file.frontmatter.service] == undefined){
		acc[current.file.frontmatter.service] = []
	}
	acc[current.file.frontmatter.service].push(current)

	return acc
}, {}) 

const rowTransformer = (rows) => {
	return rows.map(api => [
		api.file.link,
		api.file.frontmatter.route,
		api.file.frontmatter.desc,
	])
}

dv.header(2, "All Routes")
dv.table(
    ["File", "Route", "Desc"],
	rowTransformer(rows)
    );

for (const [service, files] of Object.entries(data)){
	dv.header(2, service)
	dv.table(cols, rowTransformer(files))
}

```